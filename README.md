
# [Sendbird](https://sendbird.com) Chat SDK for .NET

[![Platform](https://img.shields.io/badge/platform-.NET-orange.svg)](#)
[![Languages](https://img.shields.io/badge/language-C%23-orange.svg)](#)
[![Commercial License](https://img.shields.io/badge/license-Commercial-brightgreen.svg)](https://github.com/sendbird/SendBird-SDK-dotNET/blob/master/LICENSE.md)

## Table of contents

1. [Introduction](#introduction)
2. [Getting started](#getting-started)
3. [Sending your first message](#sending-your-first-message)


## Introduction

The Sendbird Chat SDK for .NET allows you to add real-time chat into your client app with minimal effort. Sendbird offers a feature rich, scalable, and proven chat solution.
<br />

### How it works

The Chat SDK provides the full functionality to provide a rich chat experience, implementing it begins by adding a user login, listing the available channels, selecting or creating an open channel or group channel, and receive messages and other events through channel event delegates and the ability to send a message. Once this basic functionality is in place, congratulations, you now have a chat app!

Once this is in place, take a look at [all the other features](https://sendbird.com/features/chat-messaging/features) that Sendbird supports and add what works best for your users.
<br />


## Getting started

### Step 1: Create a Sendbird application from your dashboard

Before installing Sendbird Chat SDK, you need to create a Sendbird application on the [Sendbird Dashboard](https://dashboard.sendbird.com). You will need the `App ID` of your Sendbird application when initializing the Chat SDK.

> **Note**: Each Sendbird application can be integrated with a single client app. Within the same application, users can communicate with each other across all platforms, whether they are on mobile devices or on the web.

<br />

### Step 2: Install the Chat SDK

To install the Sendbird Chat SDK for .NET, you need to add the `Sendbird.Chat` package from NuGet. Follow the steps below:

1. Open your project in Visual Studio.
2. Go to **Tools** > **NuGet Package Manager** > **Package Manager Console**.
3. Search for `Sendbird.Chat` in the **Browse** tab.
4. Select the package and click **Install**.

Alternatively, you can install the package using the NuGet Package Manager Console with the following command:

```bash
dotnet add package Sendbird.Chat
```

Once the package is installed, you can start integrating Sendbird Chat into your application.

<br />

## Sending your first message

Now that the Chat SDK has been imported, we're ready to start sending a message.

### Authentication

In order to use the features of the Chat SDK, a `SendbirdChat` instance must be initiated through user authentication with Sendbird server. This instance communicates and interacts with the server based on an authenticated user account, and then the user’s client app can use the Chat SDK's features.

Here are the steps to sending your first message using Chat SDK:

<br />

### Step 3: Using the Sendbird.Chat namespace

Once the SDK have been installed, create a new source code file and add the following code at the top to start using Sendbird Chat SDK.
```csharp
using Sendbird.Chat;
```

### Step 4: Initialize the Chat SDK

Now, initialize the Chat SDK in the app to allow the Chat SDK to respond to changes in the connection status in Android client apps.

To initialize the `SendbirdChat` instance, pass the `APP_ID` of your Sendbird application in the [Sendbird Dashboard](https://dashboard.sendbird.com) as an argument to a parameter in the `SendbirdChat.Init()` method.


```csharp
SendbirdChat.Init(new SbInitParams(APP_ID));
```

### Step 5: Connect to Sendbird server

After initialization by use of the `Init()` method, your client app must always be connected to Sendbird server before calling any methods. If you attempt to call a method without connecting, an `ConnectionRequired(800101)` error would return.

Connect a user to Sendbird server either through a unique user ID or in combination with an access token. Sendbird prefers the latter method, as it ensures privacy with the user. The former is useful during the developmental phase or if your service doesn't require additional security.

#### A. Using a unique user ID

Connect a user to Sendbird server using their unique **user ID**. By default, Sendbird server can authenticate a user by a unique user ID. Upon request for a connection, the server queries the database to check for a match. Any untaken user ID is automatically registered as a new user to the Sendbird system, while an existing ID is allowed to log indirectly. The ID must be unique within a Sendbird application, such as a hashed email address or phone number in your service.

This allows you to get up and running without having to go deep into the details of the token registration process, however make sure to enable enforcing tokens before launching as it is a security risk to launch without.

```csharp
SendbirdChat.Connect(USER_ID, (inUser, inError) => { });
```

#### B. Using a combination of unique user ID and token

Sendbird prefers that you pass the APP ID through the use of a token, as it ensures privacy and security for the users. [Create a user](https://sendbird.com/docs/chat/v3/platform-api/guides/user#2-create-a-user) along with their access token, or [issue an session token](https://sendbird.com/docs/chat/v3/platform-api/user/managing-session-tokens/issue-a-session-token) to pass during connection. A comparison between an access token and session token can be found [here](https://sendbird.com/docs/chat/v3/platform-api/user/managing-session-tokens/issue-a-session-token). Once a token is issued, a user is required to provide the issued token in the `SendbirdChat.connect()` method which is used for logging in.

1. Using the Chat Platform API, create a Sendbird user account with the information submitted when a user signs up your service.
2. Save the user ID along with the issued token to your persistent storage which is securely managed.
3. When the user attempts to log in to the Sendbird application, load the user ID and token from the storage, and then pass them to the `SendbirdChat.Connect()` method.
4. Periodically replacing the user's token is recommended to protect the account.

```csharp
SendbirdChat.Connect(USER_ID, AUTH_TOKEN, (inUser, inError) => { });
```

<br />

### Step 6: Create a new open channel

Create an open channel using the following codes. Open channels are where all users in your Sendbird application can easily participate without an invitation.

```csharp
SendbirdChat.OpenChannel.CreateChannel(new SbOpenChannelCreateParams(), (inChannel, inError) => { });
```

### Step 7: Enter the channel

Enter the open channel to send and receive messages.

```csharp
SbOpenChannel openChannel = null;
SendbirdChat.OpenChannel.GetChannel(CHANNEL_URL, (inChannel, inCache, inGetChannelError) =>
{
    if (inGetChannelError != null)
        return; //Error

    openChannel = inChannel;
    openChannel.Enter((inEnterChannelError) =>
    {
        if (inEnterChannelError != null)
            return; //Error
    });
});
```

<br />

### Step 8: Send a message to the channel

Finally, send a message to the channel. There are [three types](https://sendbird.com/docs/chat/v3/platform-api/guides/messages#-3-resource-representation): a user message, which is a plain text, a file message, which is a binary file, such as an image or PDF, and an admin message, which is a plain text also sent through the [dashboard](https://dashboard.sendbird.com/auth/signin) or [Chat Platform API](https://sendbird.com/docs/chat/v3/platform-api/guides/messages#2-send-a-message).

```csharp
openChannel.SendUserMessage(MESSAGE, (inMessage, inError) =>
{
    if (inError != null)
        return; //Error
});
```

<br />
