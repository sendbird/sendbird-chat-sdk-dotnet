# Change Log

## 4.1.4 (Feb 4, 2026)
### Bug Fixes
- Fixed WebGL memory issue by optimizing JSON parsing for message deserialization

## 4.1.3 (Nov 3, 2025)
### Improvements
- Removed unnecessary URL encoding from SB-SDK-User-Agent header

## 4.1.2 (Oct 27, 2024)
### Improvements
- Enhanced stability and performance

## 4.1.1 (Jul 14, 2025)
### Bug Fixes
- Resolved WebSocket connection failure due to User-Agent header on .NET Framework

## 4.1.0 (Nov 29, 2024)
### Features
- Added `SetPushTriggerOption` to `SendbirdChatClient`
- Added `GetPushTriggerOption` to `SendbirdChatClient`
- Added `SetMyPushTriggerOption` to `SbGroupChannel`
- Added `GetMyPushTriggerOption` to `SbGroupChannel`
- Added `SbPushTriggerOption`
### Bug Fixes
- Fixed an issue with `SendbirdChat.BlockUser` where 'User not found error' occurs due to URL encoding

## 4.0.1 (Sep 25, 2024)
### Improvements
 - Improved WebSocket connection

## 4.0.0 (Sep 3, 2024)
### Features
- Added group channel collection
- Added message collection
- Added message threading
- Added support for using a session token
- Added support for message reactions
- Added support for message resending
- Added support for pinned messages
- Added support for extra data in a message
- Support for NuGet
