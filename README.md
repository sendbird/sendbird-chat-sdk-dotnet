# [Sendbird](https://sendbird.com) Chat SDK for .NET

[![Platform](https://img.shields.io/badge/platform-Unity%2F.NET%2FMono%2FXamarin-orange.svg)](#)
[![Languages](https://img.shields.io/badge/language-C%23-orange.svg)](#)
[![Commercial License](https://img.shields.io/badge/license-Commercial-brightgreen.svg)](https://github.com/sendbird/SendBird-SDK-dotNET/blob/master/LICENSE.md)

## Table of contents

  1. [Introduction](#introduction)
  1. [Before getting started](#before-getting-started)
  1. [Getting started](#getting-started)
  1. [Send your first message](#send-your-first-message)

<br />

## Introduction

Through Chat SDK for .NET, you can efficiently integrate real-time chat into your client app. On the client-side implementation, you can initialize, configure and build the chat with minimal effort. On the server-side, Sendbird ensures reliable infra-management services for your chat within the app. This read.me provides the Chat SDK’s structure, supplementary features, and the installation steps. 

### For further reference

Find out more about Sendbird Chat for .NET on [Chat SDK for .NET doc](https://sendbird.com/docs/chat/v3/dotnet/getting-started/chat-sdk-setup).

<br />

## Before getting started

### Requirements

The minimum requirements for Chat SDK for .NET are: 

- Our Chat SDK is designed and tested on `Mono/.NET 2.0` platform and `Xamarin Studio 6.1.1`. You can also use our SDK on any platforms which are compatible with `Mono/.NET 2.0`.

### WebSocket library

The Chat SDK for .NET uses `websocket-sharp` for websocket connections. You must include `websocket-sharp.dll` as well as `SendBird.dll` or `SendBird.Unity.dll` and update them together. You can find `websocket-sharp.dll` on the same [Github repository](https://github.com/sendbird/SendBird-SDK-dotNET) as the Chat SDK.

<br />

## Getting started

### Try the sample app

The fastest way to test Chat SDK is to build your chat app on top of our sample app. To create a project for the sample app, download the app from our GitHub repository. The link is provided below.  

- https://github.com/sendbird/Sendbird-Unity

Make sure to input your application ID into the sample app. Go to the [Create a Sendbird application from your dashboard](https://sendbird.com/docs/chat/v3/dotnet/getting-started/chat-sdk-setup#2-step-1-create-a-sendbird-application-from-your-dashboard) section to learn more.

### Step 1: Create a Sendbird application from your dashboard

A Sendbird application comprises everything required in a chat service including users, messages, and channels. A Sendbird application can either be created through the dashboard. To create an application:

1. Go to the [Sendbird Dashboard]() and enter your email and password, and create a new account. You can also sign up with a **Google** account.
2. When prompted by the setup wizard, enter your organization information to manage Sendbird applications.
3. When your dashboard home appears, click **Create +** at the top-right corner.

Regardless of the platform, only one Sendbird application can be integrated per app; however, the application supports communication across allSendbird’s provided platforms without any additional setup. Sendbird currently supports iOS, Android, web, .NET, and Unity client apps.

> Note: All the data is limited to the scope of a single application, thus the users in different Sendbird applications are unable to chat with each other.

### Step 2: Download the latest Chat SDK

- https://github.com/sendbird/SendBird-SDK-dotNET

<br />

## Send your first message

### Authentication

To use the features of the Chat SDK in your client app, a `SendBirdClient` instance must be initiated in each client app before user authentication with Sendbird server. These instances communicate and interact with the server based on an authenticated user account, allowing for the client app to use the Chat SDK features. 

### Step 1: Initialize the Chat SDK 

You need to initialize a Sendbird instance before authentication. Initialization binds the Chat SDK to Android’s context which allows Chat SDK to respond to connection and state changes and also enables client apps to use Chat SDK features. 

To initialize a Sendbird instance, pass the `App_ID` of your Sendbird application in the dashboard to the `SendBirdClient.Init()`. As the `SendBirdClient.Init()` can only be a single instance, call it only a single time across your client app. Typically, initialization is implemented in the user login screen.

```csharp
SendBirdClient.Init(APP_ID);
```

### Step 2: Connect to Sendbird server

Apart from initialization or use of the `init()` method, your client app must always be connected to Sendbird server before calling any methods. If you attempt to call a method without connecting, a [`ERR_CONNECTION_REQUIRED (800101)`](https://sendbird.com/docs/chat/v3/dotnet/guides/error-codes) error would return.

Connect a user to Sendbird server using a unique user ID or in combination with an access token. Sendbird prefers the latter method, as it ensures privacy with the user, but the former method is useful during the developmental phase or if your service doesn't require additional security.

#### A. User ID

Connect a user to Sendbird server using their unique **user ID**. By default, Sendbird server can authenticate a user by a unique user ID. Upon request for a connection, the server queries the database to check for a match. Any untaken user ID is automatically registered as a new user to the Sendbird system, while an existing ID is allowed to log indirectly.  The ID must be unique within a Sendbird application, such as a hashed email address or phone number in your service.

```csharp
SendBirdClient.Connect(USER_ID, (User user, SendBirdException e) =>
{
    if(e != null)   // Error
        {
            return;
        }
});
```

#### B. A combination of user ID and access token ID 

Sendbird prefers that you pass the APP ID through the use of a token, as it ensures privacy for the users. Create a user along with their access token, or issue an access token for an existing user. Once an access token is issued, a user is required to provide the access token in the `SendBirdClient.connect()` method which is used for logging in.

1. Using the [Chat Platform API](https://sendbird.com/docs/chat/v3/platform-api/guides/user#2-create-a-user), create a Sendbird user account with the information submitted when a user signs up your service.
2. Save the user ID along with the issued access token to your persistent storage which is securely managed.
3. When the user attempts to log in to the Sendbird application, load the user ID and access token from the storage, and then pass them to the `SendBirdClient.connect()` method.
4. Periodically replacing the user's access token is recommended to protect the account.

```csharp
SendBirdClient.Connect(USER_ID, ACCESS_TOKEN, (User user, SendBirdException e) =>
{
    if(e != null)    // Error
    {
        return;
    }
});
```

#### Tips for user account security

From **Settings** > **Application** > **Security** > **Access token permission** setting in your dashboard, you can prevent users without an access token from logging in to your Sendbird application or restrict their access to read and write messages.

For security reasons, you can also use a session token when a user logs in to Sendbird server instead of an access token. Go to the [Access token vs. Session token](https://sendbird.com/docs/chat/v3/platform-api/guides/user#2-create-a-user-3-access-token-vs-session-token) section from the [Chat Platform API](https://sendbird.com/docs/chat/v3/platform-api/getting-started/prepare-to-use-api) to learn more.

### Step 3: Create a new open channel

Create an [open channel](https://sendbird.com/docs/chat/v3/dotnet/guides/open-channel#2-create-a-channel). Once created, all users in your Sendbird application can easily participate in the channel. You also can create a [group channel](https://sendbird.com/docs/chat/v3/dotnet/guides/group-channel#2-create-a-channel) by [inviting users](https://sendbird.com/docs/chat/v3/dotnet/guides/group-channel#2-invite-users-as-members) as new members to the channel.

```csharp
OpenChannel.CreateChannel(NAME, COVER_IMAGE_OR_URL, DATA, CUSTOM_TYPE, (OpenChannel openChannel, SendBirdException e) => {
    if(e != null) { // Error.
        return;
    }
});
```

### Step 4: Enter the channel

Enter the channel to send and receive messages.

```csharp
OpenChannel.GetChannel(CHANNEL_URL, (OpenChannel openChannel, SendBirdException e) => {
    if (e != null) {    // Error.
        return;
    }
    
    openChannel.Enter((SendBirdException e) => {
        if (e != null) {    // Error.
            return;
        }
    });
});
```

### Step 5: Send a message to the channel

Finally, send a message to the channel. There are [three types](https://sendbird.com/docs/chat/v3/platform-api/guides/messages#-3-resource-representation): a user message, which is a plain text, a file message, which is a binary file, such as an image or PDF, and an admin message, which is a plain text sent through the [dashboard](https://dashboard.sendbird.com/auth/signin) or [Chat Platform API](https://sendbird.com/docs/chat/v3/platform-api/guides/messages#2-send-a-message).

```csharp
openChannel.SendUserMessage(MESSAGE, DATA, (UserMessage userMessage, SendBirdException e) => {
    if (e != null) {    // Error.
        return;
    }
});
```
