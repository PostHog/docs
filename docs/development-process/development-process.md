## How to test

### Backend
At the moment, we have strong tests on the backend. We expect every backend function to have tests, and to be typed. Running `bin/tests` will run both tests and type-checking.

To run a specific subset of tests
```bash
bin/tests posthog.api.test.test_action
```

You can also pass failfast
```bash
bin/tests --failfast
```

### Frontend
At the moment we do not have good frontend tests. This is something we want, but haven't gotten round to.


## How to QA
[How to QA](/development-process/How-to-QA)


## How to release a new version 
[Release new version](/development-process/Release-new-version)