# [App Configuration](../) > [Server](README.md) > AWS Lambda

[AWS Lambda](https://aws.amazon.com/lambda/) is a serverless hosting solution by Amazon Web Services. Find the [official documentation here](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html).

* [Lambda Configuration](#lambda-configuration)
* [Creating a Lambda Function](#creating-a-lambda-function)
* [Things to Consider](#things-to-consider)
* [Troubleshooting](#troubleshooting)

## Lambda Configuration

Here is how the part of `index.js`, which is used to run the app on AWS Lambda, looks like: 

```javascript
'use strict';

const {app} = require('./app/app.js');

exports.handler = (event, context, callback) => {
    app.handleLambda(event, context, callback);
};
```

## Creating a Lambda Function

While for Alexa, the process of hosting a Skill on Lambda is straightforward, for a Google Action there are additional steps that need to be taken to create an API Gateway. To learn more about how to run your voice app on Lambda, please take a look at our step-by-step tutorials:

* [Run your Alexa Skill on Lambda](https://www.jovo.tech/blog/alexa-skill-tutorial-nodejs/#aws-lambda)
* [Run your Google Action on Lambda with an API Gateway](https://www.jovo.tech/blog/google-action-tutorial-nodejs/#aws-lambda)

## Things to Consider

The [FilePersistence](.../07_integrations/databases/#filepersistence) database integration does not work on AWS Lambda. It is encouraged to switch to [DynamoDB](.../07_integrations/databases/#dynamodb) before uploading to Lambda.

## Troubleshooting

If your `tell` or `ask` responses aren't firing inside callbacks or promises on Lambda, try to add the following to your `exports.handler`:

```javascript
context.callbackWaitsForEmptyEventLoop = false;
```
