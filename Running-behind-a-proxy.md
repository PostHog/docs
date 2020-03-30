If you're running PostHog behind a proxy, there's a few more things you need to do to make sure PostHog (specifically the toolbar, which runs on your own site) works.

## IS_BEHIND_PROXY

Make sure you have the IS_BEHIND_PROXY environment variable set to true

## NGINX config

You need to make sure your proxy server is sending X-Forwarded-For headers. For NGINX, that config should look something like:

```nginx
    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect off;
        proxy_set_header X-Forwarded-Proto $http_x_forwarded_proto;
        proxy_pass http://127.0.0.1:8000;
    }
```

## Infinite redirect

Some users have reported getting infinite redirects running behind a proxy. You can set the `DISABLE_SECURE_SSL_REDIRECT` variable to make PostHog run using http.