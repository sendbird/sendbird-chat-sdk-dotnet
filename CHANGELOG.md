Changelog
=========
# v2.3.1 (October, 10, 2016)  
* Improved stability.

# v2.3.0 (July, 27, 2016)  
* Performance Improvement
* Unity SDK is separated
* Now you can set `SendBirdSDK.CommonVar.IS_LOGGING` (`true`, `false`) you can see logs from SendBird SDK

# v2.2.0 (June, 14, 2016)  
* SDK Internal timer logic is changed.
* Performance Improvement
* Fixed a bug `NullReferenceException` in `SendBirdSDK.SendMessage`

# v2.1.2 (June, 10, 2016)  
* SendBirdSDK.GetConnectionState() is added.

# v2.1.1 (May, 24, 2016)  
* Performance improvement

# v2.0.0 (May, 17, 2016)  
* Added routing for getting server address
* `websocket-sharp.dll` file is changed, please update your existing dll.
* Fixed asynchronous API request bugs

# v1.2.1 (April, 12, 2016)  
* Updated Internal Settings

# v1.2.0 (April, 7, 2016)  
* Updated All Internal API request(asynchronous)

# v1.1.1 (March, 21, 2016)
* Fixed a bug that `SendBird.Login` fails to login again with different User ID.
* Fixed `SendBird.Model.SystemEvent` data field parsing error.

# v1.1.0 (March, 17, 2016)
* Added `MemberCountQuery` which returns total member count and online member count.
* Updated `MemberListQuery`. You can select to return all members list or online members list using onlineOnly.
* Added `ChannelMetaDataQuery`
* Added `ChannelMetaCounterQuery`
* Added `isOnline`, `lastSeenAt` to `User` Model
* Added `isSoftMuted` to `Message`, `FileLink`
* Added `isMuted` to `User`, `Member`, `Sender`
* Added `SystemEvent` and `OnSystemEventReceived` to `SendBirdEventHandler` for system events such as `join` or `leave` to/from `channels`.
* Added `OnMutedMessageReceived/OnMutedFileReceived` to `SendBirdEventHandler` for soft muted user's messages and files.
* Deleted `SendBirdNotificationHandler`, all events are moved to `SendBirdEventHandler`

# v1.0.0
* `SendBird .NET SDK` Release
