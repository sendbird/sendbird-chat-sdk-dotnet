Changelog
=========
# v3.0.31 (Mar. 25, 2024)
* Fixed Websocket not supporting TLS 1.2

# v3.0.30 (Jun. 7, 2023)
* Support Websocket TLS 1.2

# v3.0.29 (Oct. 12, 2021)
* Fix SetFile() Bug.

# v3.0.28 (July 16, 2021)
* Add Public Interface For Emoji
*  - GetEmoji
*  - GetAllEmoji
*  - GetEmojiCategory
* Bug Fix

# v3.0.27 (Jun 14, 2021)
* Add operator list query.

# v3.0.26 (May 25, 2021)
* Add operator related methods.

# v3.0.25 (May 14, 2021)
* Monior bug fix.

# v3.0.24 (May 7, 2021)
* Add public group channel name search.

# v3.0.23 (Apr 20, 2021)
* Add missing method for UserMessageParams.
* Stability improvement.

# v3.0.22 (Mar 31, 2021)
* Add ApplicationUserListQuery.
* Statbility improvement.

# v3.0.21 (Mar 10, 2021)
* Bug fix.

# v3.0.20 (Mar 9, 2021)
* Bug fix.

# v3.0.19 (Jan 9, 2021)
* Fix FileMessage.GetSender() thrown an exception in some cases.
* UserMessage.Sender property is deprecated. Use UserMessage.GetSender() instead.

# v3.0.18 (Oct 22, 2020)
* File encryption support.

# v3.0.17 (Jun 19, 2020)
* Chat history reset feature added.
* User mention feature added.
* User event handler added.
* Performance improved.

# v3.0.16 (Jun 1, 2020)
* Retrieval of banned/unmuted user list added.
* Channel hide/archive feature added.
* User/message reporting feature added.

# v3.0.15 (May 15, 2020)
* Introduced group channel invitation feature.
* Introduced message update feature.
* Added channel creation custom URL option.

# v3.0.14 (NOV 30, 2019)
* Added `BanUser`, `UnbanUser` in GroupChannel
* Added creating and updating GroupChannel with operators.

# v3.0.13 (JUL 25, 2019)
* Improved ConnectionHandler.  

# v3.0.12 (JUL 28, 2018)
* Improved SendBird server connection.  

# v3.0.11 (JUN 18, 2018)
* Added CustomTypesFilter in GroupChannelListQuery to search channels based on CustomType.  

# v3.0.10 (May 23, 2018)
* Updated WebSocket lib version.

# v3.0.9 (Jan 26, 2018)
* Fixed signing assembly issue on Windows build.

# v3.0.8 (Jan 24, 2018)
* Reconnect() method added for explicit reconnection.
* Application ID re-initialization added.

# v3.0.7 (Jan 18, 2018)
* Improved stability.

# v3.0.6 (Apr 17, 2017)
* Fixed message deletion issue on Unity 3d.

# v3.0.5 (Jan 20, 2017)
* Speed up initial loading on some platforms.

# v3.0.4 (Jan 17, 2017)
* Improved stability.
* Fixed read receipt reset issue.

# v3.0.3 (DEC 14, 2016)
* Improved stability.

# v3.0.2 (Dec 9, 2016)
* Improved performance.
* Improved stability.
* Added user IDs filters and query type to GroupChannelListQuery.
* Added channel custom type for OpenChannel and GroupChannel.
* Fixed to call ChannelHandler.onChannelChanged when unread message count or last message has been updated.
* Fixed to update last message of group channel when UserMessage or FileMessage is successfully sent.
* Added custom type to messages.
* Added group channel list search by member nicknames and user IDs.
* Added creating and updating channel cover image with binary file.

# v3.0.1 (Nov 21, 2016)  
* Faster connection time.
* Improved stability.

# v3.0.0 (Nov 7, 2016)  
* `SendBird .NET SDK v3`.

# v2.3.0 (Jul 27, 2016)  
* Performance Improvement.
* Unity SDK is separated.
* Now you can set `SendBirdSDK.CommonVar.IS_LOGGING` (`true`, `false`) you can see logs from SendBird SDK.

# v2.2.0 (Jun 14, 2016)  
* SDK Internal timer logic is changed.
* Performance Improvement
* Fixed a bug `NullReferenceException` in `SendBirdSDK.SendMessage`

# v2.1.2 (Jun 10, 2016)  
* SendBirdSDK.GetConnectionState() is added.

# v2.1.1 (May 24, 2016)  
* Performance improvement

# v2.0.0 (May 17, 2016)  
* Added routing for getting server address
* `websocket-sharp.dll` file is changed, please update your existing dll.
* Fixed asynchronous API request bugs

# v1.2.1 (Apr 12, 2016)  
* Updated Internal Settings

# v1.2.0 (Apr 7, 2016)  
* Updated All Internal API request(asynchronous)

# v1.1.1 (Mar 21, 2016)
* Fixed a bug that `SendBird.Login` fails to login again with different User ID.
* Fixed `SendBird.Model.SystemEvent` data field parsing error.

# v1.1.0 (Mar 17, 2016)
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
