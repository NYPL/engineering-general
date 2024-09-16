# Using Travis

Travis is a CI/CD provider that facilitates an automated deployment of codebases to host providers like AWS and Pantheon. [DevOps recommends using Github actions rather than Travis](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DOPS/pages/179535874/How+do+I+migrate+from+Travis+CI+to+GitHub+Actions) for CI/CD. But there are many apps that continue to use it.

## Accessing Travis

[Access to Travis](https://app.travis-ci.com) is typically associated with the Github account you use for NYPL. DevOps will facilitate this.

## How to Rotate Travis/AWS Keys

For better security, once every six months DevOps will change the keys that Travis must use to deploy to AWS. There is an ID and a SECRET. Development and QA builds share a pair of ID and SECRET values. Production builds have their own ID and SECRET. To properly rotate keys, you will therefore need to update four values for each app. **All apps share the same four keys.**

The simplest method for updating these keys is via [environment variables](https://docs.travis-ci.com/user/environment-variables/#defining-variables-in-repository-settings) stored in the Travis UI. The values are found in the AWS Parameter Store UI.

### Requirements
1. [Access to AWS](aws-use.md)
2. Access to Travis

### Process

1. [Log into AWS](https://nypl.signin.aws.amazon.com/console) using the NYPL Production account.
2. Go to [AWS Systems Manager > Parameter Store > /production/amazon/access-keys/travis-deployer](https://us-east-1.console.aws.amazon.com/systems-manager/parameters/%252Fproduction%252Famazon%252Faccess-keys%252Ftravis-deployer/description?region=us-east-1&tab=Table#list_parameter_filters=Name:Contains:travis)
3. Click the "Show decrypted value" toggle at the lower left.
4. In a different tab or window [log into Travis](https://app.travis-ci.com/dashboard).
5. Under the "Active Repositories" list, find the repo you wish to update, click the hamburger on the right hand side and select "Settings."
6. Scroll down to find "Environmental Values"
7. In order to update an env var, you must delete the old one and recreate it with the new value. (The key names can be whatever you want, but need to match values you set in the repo, either in the .travis.yml or in a related deploy script.) For example, if you have a key named `AWS_ACCESS_KEY_ID_PRODUCTION`: 
   1. On the right of the `AWS_ACCESS_KEY_ID_PRODUCTION` env var click the trash can.
   2. Underneath the list of env vars there is a form for adding a new one. In the key field type `AWS_ACCESS_KEY_ID_PRODUCTION`. 
   3. In the AWS UI, copy the _value_ for "access-key-id". For example, you would copy `abcdefg1234567890` from `"access-key-id":"abcdefg1234567890"`
   4. Back in the Travis UI, paste the value into the "value" field. 
   5. Click "Add" on the right side.
8. Repeat step 7 for the access key _secret_ variable.
9. Log into the AWS NYPL Dev account Parameter Store to retrieve the values for the Dev/QA servers and repeat steps 7 & 8 for Dev/QA keys.

There is another, older process that involves encrypting the AWS values using the Travis CLI, storing the encrypted values in the `.travis.yml`, and then merging the changes into the repo. But this is not recommended and the encryption command may fail in some cases.

### Testing

To test that the updated keys are correct you can re-run the last Travis build on a dev, QA or production branch of the repo. However, you may wish to avoid re-running builds on production services during business hours. You could wait for the next official deployment. If it builds, the keys are correct. If not, you can double-check them during your maintenance window.
