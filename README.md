# SAS Conversation Designer SDK

## Overview

The SAS Conversation Designer software development kit (SDK) is a set of JavaScript APIs and web components that enable SAS Conversation Designer chatbots to be easily embedded in a third-party application or web page. This functionality is delivered as the `conversation-designer-components` JavaScript library. This project provides examples of how to use the SDK components in various scenarios.

# Prerequisites

Access to a deployment of SAS Conversation Designer and a bot are required in order to use the SDK. For more information about server set up, see the <a target="_blank" href="https://developer.sas.com/sdk/va/docs/getting-started#sas-viya-setup">SAS Viya setup</a> section. Note that the other sections on the Getting Started page are specific to SAS Visual Analytics and not the SAS Conversation Designer SDK.

# Installation

### npm

The <a target="_blank" href="https://www.npmjs.com/package/@sassoftware/conversation-designer-components">`@sassoftware/conversation-designer-components`</a> library is published to <a target="_blank" href="https://www.npmjs.com/">npm</a> and can be installed by running the `npm install` command as shown below. `conversation-designer-components` does not support ES6 imports. Therefore, the contents of the `conversation-designer-components/dist` folder must be deployed with your page, and then loaded using a `script` tag.

```bash
# From the root directory of your project
npm install @sassoftware/conversation-designer-components

# Copy the contents of the package to an asset folder for deployment
cp -r ./node_modules/@sassoftware/conversation-designer-components ./sdk-assets
```

The library can then be loaded out of the deployed assets folder using a `script` tag.

```html
<script async src="./sdk-assets/conversation-designer-components.js"></script>
```

### CDN (Content Delivery Network)

Accessing the `conversation-designer-components` library from a CDN is easy. It does not require installation or
hosting of the library code and assets. There are several public options for accessing npm content through a CDN, such
as <a target="_blank" href="https://unpkg.com/">UNPKG</a> and <a target="_blank" href="https://www.jsdelivr.com/">jsDelivr</a>. Here is an example of loading the 0.1.0 version of `conversation-designer-components` from UNPKG
using an HTML `script` tag. When used in production, the version should be pinned to the full `major.minor.patch` semantic version.

```html
<script async src="https://unpkg.com/@sassoftware/conversation-designer-components@0.1.0/conversation-designer-components.js"></script>
```

# Getting Started

When using the SAS Conversation Designer SDK, you must provide some information to configure the components. For information on the values you should provide and where they should go, see the [API section](#API). Following is additional information about some of the attributes:

- url - this value points to the base url of your SAS environment (for example, if SAS Conversation Designer was deployed to http://yourcompany.com/SASConversationDesigner, then set this value to http://yourcompany.com)
- botUri - this is the unique identifier for the bot that you want the component to communicate with (for example, /naturalLanguageConversations/bots/e3b1f772-1562-4c8c-a60e-1ee20684ce4b)
- revisionId - this is the unique identifier for the bot revision within your bot that the component will communicate with; this could be a delegate value (for example, @published, @latest) or the universally unique identifier (UUID) (for example, aa1e4567-e89b-12d3-a456-426614158700)

## Examples

Full examples are located in the [examples folder](https://github.com/sassoftware/conversation-designer-sdk/blob/HEAD/examples/) of this repository.

# API

## SASChatElement

The SASChatElement is a custom HTML element that renders a chat window. This element extends the HTMLElement.

To find the correct values for the url, botUri, and revisionId attributes, see the [Getting Started](#Getting-Started) section.

### Custom Element Tag

```html
<sas-chat url="https://my-viya-server.com"
          botUri="/naturalLanguageConversations/bots/ca433b17-157b-46e9-9d60-d91d81991639"
          connectorName="connectorName"
></sas-chat>
```

### Attributes

> authenticationType: string

Choose the method to authenticate requests to the SAS Viya server:

- 'guest' automatically signs in to the SAS Viya server as the guest user (authenticationType="guest").
- 'credentials' uses SAS Logon to establish an authenticated session (authenticationType="credentials").

default value: 'credentials'

> url: string

Specify the URL of the SAS Viya server that hosts the report. This is the full context root, including the protocol, optional port, and host.

> botUri: string

Specify the bot URI ([How do I find the botUri for my bot?](#How-do-I-find-the-botUri-for-my-bot)).

> revisionId: string

Specify the revision ID ([How do I find the revisionId for my bot?](#How-do-I-find-the-revisionId-for-my-bot)). 

default value: '@published'

> userId: string

Specify the user ID. This value is only used when the value of the authenticationType parameter is 'guest'. This is only used for tracking/display and is not related to authorization or security.

default value: the user ID of the authenticated Viya user

> userName: string

Specify the user name. This value is only used when the value of the authenticationType parameter is 'guest'. This is only used for tracking/display and is not related to authorization or security.

default value: user name of the authenticated Viya user

> connectorName: string

Specify the name of the connector that displays session history in the History workspace.

> sessionProperties: Object

Specify a JavaScript Object Notation (JSON) object that contains data to add to the chat session when it is created.

### Properties

> chatEventListener: Function

A  JavaScript function that is called for all chat events.

### Styles

SASChatElement supports styling certain parts of the chat interface via [CSS variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties).

> --sas-chat-bot-avatar-bg

Specify the background color of the bot avatar.

> --sas-chat-bot-avator-bd

Specify the border color of the bot avatar.

> --sas-chat-bot-avator-c

Specify the text color of the bot avatar.

> --sas-chat-user-avatar-bg

Specify the background color of the user avatar.

> --sas-chat-user-avatar-bd

Specify the border color of the user avatar.

> --sas-chat-user-avatar-c

Specify the text color of the user avatar.

> --sas-chat-timestamp-c

Specify the text color of the timestamps.

> --sas-chat-bot-response-bubble-bg

Specify the background color of the bot response bubbles.

> --sas-chat-bot-response-bubble-bd

Specify the border color of the bot response bubbles.

> --sas-chat-bot-response-bubble-c

Specify the text color of the bot response bubbles.

> --sas-chat-user-input-bubble-bg

Specify the background color of the user input bubbles.

> --sas-chat-user-input-bubble-bd

Specify the border color of the user input bubbles.

> --sas-chat-user-input-bubble-c

Specify the text color of the user input bubbles.


# Contributing

The SAS Conversation Designer SDK is not open for external contributions.

# License

This project is licensed under the [Apache 2.0 License](https://github.com/sassoftware/conversation-designer-sdk/blob/HEAD/LICENSE).

# Additional Resources

[SAS Conversation Designer Documentation](https://go.documentation.sas.com/?cdcId=cdesignercdc&cdcVersion=default&docsetId=cdesignerwlcm&docsetTarget=home.htm&locale=en)

# FAQ

## How do I find the botUri for my bot?
To find the botUri for a bot, open SAS Environment Manager. Click SAS Content -> Conversational Flows and open the folder with your bot’s name. Select the Chatbot object to see the URI in the properties pane.

Another option is to use the Natural Language Conversations API to find a bot ID. For example, if SAS Conversation Designer is deployed to http://yourcompany.com/SASConversationDesigner, then the base URL for the API would be http://yourcompany.com/naturalLanguageConversations. Using the base URL, you can call GET on the bot’s endpoint (for example, http://yourcompany.com/naturalLanguageConversations/bots). This URL returns a list of all bots that currently exist and you can then search the list for your bot. Once you find the name of your bot, the bot ID value is shown next to the id parameter.

Here is an example:

    {
    ...
    "items": [
      {
      "id": "7d3137bf-c306-4127-b513-3e3ab816d125",
      "createdBy": "sas",
      "creationTimeStamp": "2020-08-31T14:19:36.136Z",
      "modifiedBy": "sas",
      "modifiedTimeStamp": "2020-08-31T14:19:36.276Z",
      "name": "My bot",
      ...

The value “7d3137bf-c306-4127-b513-3e3ab816d125” should be appended to '/naturalLanguageConversations/bots/' be create the botUri mentioned above. 

## How do I find the revisionId for my bot?
There are three options for the revisionId parameter:

- @published - (recommended) this value points to the published version of your bot. Each time a new bot version is published, the connector automatically updates to use the most recently published bot version.
- @latest - this value points to the latest draft version of your bot. Each time a new bot or draft is created, the connector automatically updates to use the latest draft bot version.
- specific revision ID - this value points to a specific version of the bot and does not change as versions are published or created.

To find a specific revision ID, follow the above instructions on how to get a bot ID. Then you can use the API to get access to all of the revisions that are available for a bot. This can be done by calling GET on the revisions endpoint (for example, http://yourcompany.com/naturalLanguageConversations/bots/{botId}/revisions). This URL returns a list of all revisions that currently exist for your bot after you replace {botId} with the bot ID value of your bot. Next, find the revision you are interested in. The value to use for the revisionId parameter appears by the id parameter for your bot revision.

Here is an example:

    {
    ...
    "items": [
      {
      "id": "e09881bb-3206-4d73-a9c0-a6280202c188",
      "createdBy": "sas",
      "creationTimeStamp": "2020-08-31T14:19:36.136Z",
      "modifiedBy": "sas",
      "modifiedTimeStamp": "2020-08-31T14:19:36.276Z",
      "name": "My best revision",
      ...

The value “e09881bb-3206-4d73-a9c0-a6280202c188” should be used as the revision ID mentioned above.

## I'm getting a CORS error. How do I fix it?

When the SAS Conversation Designer SDK is deployed in a different domain than SAS Viya, you must update the SAS Viya CORS configuration to allow access. Instructions can be found on [developers.sas.com](https://developer.sas.com/reference/cors).