## Why QA something?

We’ve found that almost every time we QA something, we find something that would have been confusing/annoying to our users. Hence it’s worth doing QA for everything. There are very few excpetions

## What does good QA look like?
- You understand what has changed
- You understand why that change was made, so you have context
- You understand which parts of the system could be affected
    - For example, if a change is made to the way a button on the login form works, that might also appear in the /setup page, so you should check what happens/.
- You should have a high standard -- but be flexible
    - We want to build the best possible product. In terms of priority (most important first), the feature
        - works;
        - is obvious how it works;
        - doesn't have weird glitches or bugs;
        - doesn’t cause bugs elsewhere;


## How to do QA

1. Go to the pull request you want to QA. 

2. Go to the Heroku test environment

    a. If the environment was already deployed, it should say "This branch was successfully deployed"

    b. if it says ‘This branch was not deployed’ go to the Heroku pipeline and click ‘Create review app’

    c. if the PR was submitted from a fork, you'll need to test the change locally. 


3. Open the app, and add create a new account


## Hacking the test environment

### Testing User properties

To test user properties
1. Go to `/demo`
2. Open your developer console (CMD + OPT + I) 
3. Paste `posthog.identify('random-user-id');`
4. Paste `posthog.people.set({email: 'jane@gmail.com'});`
5. You can now go to `/people` and see that the user has an email set
6. You can pass any other property in the `.set` function


