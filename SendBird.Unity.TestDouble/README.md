# SendBird.Unity.TestDouble.dll

## Introduction
**SendBird.Unity.TestDouble.dll** was created to support the SendBirdClient interface.
You can use it if you need an interface like [TestDouble](https://en.wikipedia.org/wiki/Test_double).

## Requirements
- [SendBird.Unity.dll](https://github.com/sendbird/SendBird-SDK-dotNET/blob/master/SendBird.Unity.dll)

## Migration Guide
### Before
```csharp
SendBirdClient.Init(APP_ID);

SendBirdClient.Connect(USER_ID, (User user, SendBirdException e) =>
{
    if(e != null)   // Error
    {
      return;
    }
});
```

### After
```csharp
ISendBirdClientProxy sendBirdClientProxy = new SendBirdClientProxy();

sendBirdClientProxy.Init(APP_ID);
            
sendBirdClientProxy.Connect(USER_ID, (User user, SendBirdException e) =>
{
    if(e != null) // Error
    {
        return;
    }
});
```