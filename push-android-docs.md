# App Center Push

App Center Push enables you to send push notifications to users of your app from the App Center portal. App Center portal and the Push SDK is integrated with [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/).

Note that only devices having the [Google Play](https://play.google.com/) store application or emulators with Google APIs images can receive the notifications.

> Note
>
> A notification appears in the system notification center only if the application is in the background at the moment the Push is received.

## Prerequisites

### 1. Connect your app to Firebase

Before using App Center Push service, you need to connect your application to Firebase. Please learn about [Prerequisites](https://firebase.google.com/docs/android/setup#prerequisites).

### 2. Obtain your Android API Key and Sender ID

In the [Firebase Console](https://console.firebase.google.com/), go to **Project Settings**. Navigate to the **Cloud Messaging** tab. Copy the **Server Key**. This will be the Android API Key that you will need to set in the App Center Push portal. Also make a note of the **Sender ID**, as you will need it later.

## Add App Center Push to your app

Please follow the [Get started_TODO]() section if you haven't set up and started the SDK in your application, yet. The App Center SDK is designed with a modular approach – you only need to integrate the services that you're interested in.

To add App Center Push to your app open a Terminal and navigate to the root of your Cordova project, then enter the following to add App Center Push to the app:

```js
cordova plugin add cordova-plugin-appcenter-push
```

## Set the Sender ID

TODO implement in cordova then update this section

## Intercept push notifications

You can set up a listener to be notified whenever a push notification is received in foreground or a background push notification has been clicked by the user.

> Note
>
> A notification is not generated when your application receives a push in the foreground.

> Note
>
> If the push is received in background, the event is **NOT** triggered at receive time. The event is triggered when you click on the notification.

> Note
>
> The background notification click callback does **NOT** expose **title** and **message**. **Title** and **message** are only available in **foreground** pushes.

You need to register the listener when your app starts. A convenient place to do that is at `app.initialize` method of your `js/index.js:

**TODO CHECK EXAMPLE IS RIGHT**

```js
var app = {

  // store app state here
  state: 'active',

  initialize: function() {
  
    document.addEventListener("pause", function() { app.state = 'background' }, false);
    document.addEventListener("resume", function() { app.state = 'active' }, false);
    
    AppCenter.Push.addEventListener('notificationReceived', function(pushNotification) {
      var message = pushNotification.message;
      var title = pushNotification.title;

      if (message === null || message === undefined) {
        // Android messages received in the background don't include a message. On Android, that fact can be used to
        // check if the message was received in the background or foreground. For iOS the message is always present.
        title = 'Android background';
        message = '<empty>';
      }
  
      // Custom name/value pairs set in the App Center web portal are in customProperties
      if (pushNotification.customProperties && Object.keys(pushNotification.customProperties).length > 0) {
        message += '\nCustom properties:\n' + JSON.stringify(pushNotification.customProperties);
      }  
  
      if (AppState.currentState === 'active') {
        // you can alternatively use notification.alert from cordova-plugin-dialogs or something else
        console.log(title, message);
      }  
      else {
        // Sometimes the push callback is received shortly before the app is fully active in the foreground.
        // In this case you'll want to save off the notification info and wait until the app is fully shown
        // in the foreground before displaying any UI. You could use 
        // document.addEventListener("pause") and document.addEventListener("resume") to be notified
        // when the app is fully in the foreground.
      }
    });      
    },
  
    // ...

};

app.initialize();
```

## Enable or disable App Center Push at runtime

You can enable and disable App Center Push at runtime. If you disable it, the SDK will stop updating the Google registration identifier used to push but the existing one will continue working. In other words, disabling the App Center Push in the SDK will **NOT** stop your application from receiving push notifications.

```js
var enableSuccess = function() {
    console.log("push notifications enabled");
}

var disableSuccess = function() {
    console.log("push notifications disabled");
}

var error = function(error) {
    console.error(error);
}

AppCenter.Push.setEnabled(false, disableSuccess, error); // Disable push
AppCenter.Push.setEnabled(true, enableSuccess, error); // Re-enable it
```

## Check if App Center Push is enabled

You can also check if App Center Push is enabled or not:

```js
var success = function(result) {
    console.log("push notifications " + (result) ? "enabled" : "disabled");
}

var error = function(error) {
    console.error(error);
}
AppCenter.Push.isEnabled(success, error);
```


