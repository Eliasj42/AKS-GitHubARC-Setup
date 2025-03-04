# Creating a github app

## Step 1
to create an app, go to your github profile -> settings -> developer settings -> github apps and create a new app.

## Step 2
you can set the homepage url to whatever you want, this format is fine `https://github.com/apps/<app-name>`

## Step 3
You can disable webhooks

## Step 4: Permissions

### Repository Permissions

Add Actions: Read and Write and Metadata: Read only under Repository Permissions

### Orginization Permissions

Add Administration, Secrets, Self-Hosted Runners, Variables, and Webhook with Read and Write acccess

### Account Permissions

you do not need to add any account permissions

## Step 5

make sure you generate a private key for your app

## Step 6

click install app and install it in your org

Once its installed, find the instilation id

## Step 7: authenticating a runner with your app

create a secret using your app id, instilation id, and private key

```
kubectl create secret generic <secret-name>    --namespace=<runner-namespace>   --from-literal=github_app_id=<app id>    --from-literal=github_app_installation_id=<instillation id>    --from-file=github_app_private_key=<private-key.pem> 
```

then add this at the bottom of your values.yaml file
```
githubConfigUrl: https://github.com/<org-name>
githubConfigSecret: <secret-name>
```