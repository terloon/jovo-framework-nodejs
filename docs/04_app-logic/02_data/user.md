# [App Logic](../) > [Data](./README.md) > User

In this section, you will learn how to use the Jovo User class to persist user specific data and create contextual experiences for your voice apps.

* [Introduction](#introduction-to-the-user-class)
  * [Configuration](#configuration)
* [User Data](#user-data)
  * [Data Persistence](#data-persistence)
  * [Meta Data](#meta-data)
  * [User ID](#user-id)
  * [Account Linking](#account-linking)


## Introduction to the User Class

The `User` object offers helpful features to build contextual, user specific experiences into your voice applications.

You can access the user object like this:

```javascript
let user = this.user();
```

### Configuration

There are certain configurations that can be changed when dealing with the user object. The following are part of the Jovo default configuration:

```javascript
// Using the constructor
const config = {
    saveUserOnResponseEnabled: true,
    userDataCol: 'userData',
    userMetaData: {
        lastUsedAt: true,
        sessionsCount: true,
        createdAt: true,
        requestHistorySize: 0,
        devices: false,
    },
    // Other configurations
};
```
`saveUserOnResponseEnabled`: You can set this to `false` if you choose not to save any user-specific data.

`userDataCol`: Specifies the name of the column that the user data is saved to.

`userMetaData`: Specifies what and how meta data is saved. [Learn more about meta data here](#meta-data).


## User Data

The User object offers the capability to store and retrieve user specific data, including [meta data](#meta-data).

Data is stored using our [database integrations](../../06_integrations/databases), with a file-based `db.json` structure enabled by default.


### Data Persistence

With our Jovo Persistence Layer, you can store user specific data easily to either a database or a local JSON file.

Just specify a key and a value, and you're good to go: 

```javascript
this.user().data.key = value;

// Example
this.user().data.score = 300;
```

For more information on data persistence, take a look here: [Integrations > Databases](../../06_integrations/databases).


### Meta Data

The user object meta data is the first step towards building more contextual experiences with the Jovo Framework. Right now, the following data is automatically stored (by default on the FilePersistence `db.json`, or DynamoDB if you enable it):

Meta Data | Usage | Description
:--- | :--- | :---
createdAt | `this.user().metaData.createdAt` | Timestamp: When the user first used your app
lastUsedAt | `this.user().metaData.lastUsedAt` | Timestamp: The last time your user interacted with your app
sessionsCount | `this.user().metaData.sessionsCount` | Timestamp: How often your user engaged with your app


You can change the type of meta data to store with the Jovo app constructor. This is the default configuration for it:

```javascript
const config = {
    userMetaData: {
        lastUsedAt: true,
        sessionsCount: true,
        createdAt: true,
        requestHistorySize: 0,
        devices: false,
    }
    // Other configurations
};

```

### User ID

Returns user ID on the particular platform, either Alexa Skill User ID or Google Actions User ID:

```javascript
this.user().getId();

// Alternatively, you can also use this
this.getUserId();
```

This is going to return an ID that looks like this:

```js
// For Amazon Alexa
amzn1.ask.account.AGJCMQPNU2XQWLNJXU2K23R3RWVTWCA6OX7YK7W57E7HVZJSLH4F5U2JOLYELR4PSDSFGSDSD32YHMRG36CUUAY3G5QI5QFNDZ44V5RG6SBN3GUCNTRHAVT5DSDSD334e34I37N3MP2GDCHO7LL2JL2LVN6UFJ6Q2GEVVKL5HNHOWBBD7ZQDQYWNHYR2BPPWJPTBPBXPIPBVFXA

// For Google Assistant
ARke43GoJIqbF8g1vfyDdqL_Sffh
```

### Account Linking

To implement Account Linking in your voice application, you need two core methods.

The first allows you to prompt the user to link their account, by showing a card in the respective companion app:
```javascript
// Alexa Skill:
this.alexaSkill().showAccountLinkingCard();

// Google Actions:
this.googleAction().askForSignIn();
```

The other method returns you the access token, which will be added to every request your skill gets, after the user linked their account:
```javascript
this.getAccessToken();
```

For more information on Account Linking, check out our blogposts:
* [Alexa Skill Account Linking](https://www.jovo.tech/blog/alexa-account-linking-auth0/)
* [Google Actions Account Linking](https://www.jovo.tech/blog/google-action-account-linking-auth0/)