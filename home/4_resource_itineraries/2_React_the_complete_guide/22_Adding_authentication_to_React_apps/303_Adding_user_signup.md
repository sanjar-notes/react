# 303. Adding user sign up
Created Saturday 19 November 2022

We'll be using Firebase's authentication feature as the backend for authorization.

## Firebase setup
1. Open (or create) a Firebase project.
2. Go to Authentication and click 'Get started'.
3. Choose a provider, we're using email/password for now.
4. Enable the provider. Leave the _passwordless_ option disabled.

Then, get the API key:
1. Go to the project's page.
2. Click the gear icon in the sidebar, click "Project settings"
3. Copy the string with label "Web API key".

This API key is needed to access Firebase Authentication's REST API.