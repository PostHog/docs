# Deployment

# One-line docker preview

```bash
docker run -t -i --rm --publish 8000:8000 -v postgres:/var/lib/postgresql posthog/posthog:preview
```

This image has everything you need to try out PostHog locally! It will set up a server on http://127.0.0.1:8000.

!> The preview image is not meant for production.

# Deploy to Heroku

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/posthog/posthog)

Heroku is the quickest way to get a production PostHog environment up-and-running.

We recommend getting at the very least a `hobby-dev` Postgres and Dyno for low volumes of events. If you run on the 'free' tier it will work, but there will be a big lag each time you visit the app if your site hasn't been visited for a while.

[Click here](/upgrading-PostHog) for instructions on upgrading PostHog on Heroku to the latest version.

# Docker

We have [three types of images](https://hub.docker.com/r/posthog/posthog):

 - `posthog/posthog:latest`, which builds straight of master
 - `posthog/posthog:preview`, which is used for the preview image
 - `posthog/posthog:release-[version number]`, so you can pin a specific version.

?> We recommend using `posthog/posthog:latest`, so you always have the latest features and security updates

## Using Docker Compose 

1. [Install Docker](https://docs.docker.com/installation/ubuntulinux/)
2. [Install Docker Compose](https://docs.docker.com/compose/install/)
3. Run the following:
```bash
sudo apt-get install git
git clone https://github.com/posthog/posthog.git
cd posthog
docker-compose up -d
```

If you run your Postgres database somewhere else (like RDS, or just a different server) you can set the DATABASE_URL property, and remove `services -> db` and `depends_on: - db` from your docker-compose file.

If you're running locally, make sure to add `DEBUG: 1` as an environment variable, otherwise you'll get stuck in an infinite loop of SSL redirects.


## Running behind a proxy?

If you're running PostHog behind a proxy, there are a few more things you need to do to make sure PostHog (specifically the toolbar, which runs on your own site) works.

Make sure you have the `IS_BEHIND_PROXY` environment variable set to true

### NGINX config

You need to make sure your proxy server is sending X-Forwarded-For headers. For NGINX, that config should look something like:

```nginx
    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://127.0.0.1:8000;
    }
```

### Infinite redirect

Some users have reported getting infinite redirects running behind a proxy. You can set the `DISABLE_SECURE_SSL_REDIRECT` variable to make PostHog run using http.
See [running behind a proxy](/running-behind-a-proxy) for instructions on how to set that up.

## Secret key

Secret keys are used to encrypt cookies, password reset emails [and other things](https://docs.djangoproject.com/en/3.0/ref/settings/#secret-key). To generate a secret key, run:

```bash
openssl rand -hex 32
```

# K8s

Here's an example configmap you can use
```yaml
kind: Deployment
apiVersion: apps/v1
metadata:
  name: posthog
spec:
  selector:
    matchLabels:
      app: posthog
  template:
    metadata:
      labels:
        app: posthog
    spec:
      containers:
      - name: posthog
        image: posthog/posthog:latest
        ports:
        - containerPort: 8000
        resources:
          limits:
            cpu: 95m
            memory: 285Mi
        env:
        - name: IS_DOCKER
          value: "true"
        - name: SECRET_KEY
          value: "<enter secret key here>"
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              key: database-url
              name: posthog
---
apiVersion: v1
kind: Service
metadata:
  name: posthog
  labels:
    app: posthog
spec:
  type: NodePort
  selector:
    app: posthog
  ports:
  - name: http
    port: 80
    targetPort: 8000
```

# From source
1. Make sure you have Python >= 3.7 and pip installed
2. [Install Yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable)
3. Run the following:
```bash
git clone https://github.com/posthog/posthog.git
yarn build
pip install -r requirements.txt
gunicorn posthog.wsgi --config gunicorn.config.py --log-file -
```


# How much will running PostHog cost me?

## Heroku

Using a hobby-dev instance and hobby-dev postgres database ($14/month), you should be able to handle up to about 100k events/day, with about a 100 day history.

With the next step up, 2-3x hobby-dev instances and standard-0 postgres ($64/month), you should be able to handle about 1M/events/day with over a year's worth of history.

## AWS

If running costs are a concern, AWS is likely to be a cheaper option, especially if you can commit to buy reserved instances for a year. This does come at the cost of ease-of-deployment.

If you've deployed on AWS, let us know how and how much you're spending roughly so we can improve this guide. Submit a PR to the [docs repo](https://github.com/PostHog/docs) :-).


# SMTP credentials

If you want to be able to send password reset emails from your instance, you need to set SMPTP credentials as env variables:

```yaml
EMAIL_HOST: [smtp server]
EMAIL_PORT: 578
EMAIL_HOST_USER: [username]
EMAIL_HOST_PASSWORD: [password]
EMAIL_USE_TLS: false
EMAIL_USE_SSL: false
DEFAULT_FROM_EMAIL: tim@posthog.com
```