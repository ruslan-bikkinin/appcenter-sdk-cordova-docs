# App Center Push

App Center Push enables you to send push notifications to users of your app from the App Center portal.

## Prerequisite - Enable Apple Push Notifications service (APNs) for your app

Configure Apple Push Notifications service (APNs) for your app from your Apple developer account and App Center portal before adding App Center Push to your app.

### Enable push notifications on your application

In Xcode's project editor, choose your target and click **Capabilities**. In the **Push Notifications** section, click the switch to turn it from OFF to ON.

![enable-push-capability](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/apple-enable-push-capability.png)

### Set up APNs

Log in to the App Center portal, select your application, click on the **Push** button from the left menu then click **Next** to reveal the push notification settings UI:

![app-center-push-settings](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/apple-push-settings-ac-portal.png)

* On the bottom of the page, select **Sandbox** for initial development or **Production** for production version of your application.

* Collect the following information:

  1. **Prefix** and **ID**

      * Go to your Apple developer account and select your application from the [App ID list](https://developer.apple.com/account/ios/identifier/bundle) in **Identifiers**.

      * Copy the **Prefix** value from this window and paste it to the App Center push settings.

      * Do the same with the **ID** value.

      ![apple-dev-center-app-id](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/ios-app-id-apple-portal.png)

  2. **Key ID**

      * In your Apple developer account create a [new key](https://developer.apple.com/account/ios/authkey/create) in **Certificates, Identifiers & Profiles/Keys**.

      * Make sure to check the APNs checkbox.

      * Fill in the key name

      * Press **Continue** then **Confirm**.

      ![apple-dev-center-new-auth-key](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/ios-new-auth-key-apple-portal.png)

      * On the next screen, copy the **Key ID** value and paste it to the App Center push settings.

      * Download the key file.

      ![apple-dev-center-confirm-auth-key](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/ios-confirm-auth-key-apple-portal.png)

  3. Push Token

      * Open your key file with a text editor and copy the authentication token it contains.

      ![auth-key-file](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/apple-auth-key-file.png)

      * On the App Center push settings, paste this token to the Push Token field then click Done to complete this configuration.

For more information, refer to the [Apple documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073).

#### [Optional] Enable silent notifications

Silent notifications give you a way to wake up your app so that it can refresh its data in the background (see [Apple documentation](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/CreatingtheNotificationPayload.html#//apple_ref/doc/uid/TP40008194-CH10-SW8)). To enable silent notifications open Xcode's project editor, choose your target and click **Capabilities**. Turn on **Background Modes** and check the **Remote notifications** checkbox.

![enable-silent-notifications](https://docs.microsoft.com/en-us/appcenter/sdk/push/images/ios-enable-silent-notifications.png)

## Add App Center Push to your app

Please follow the [Get started_TODO]() section if you haven't set up and started the SDK in your application, yet. The App Center SDK is designed with a modular approach – you only need to integrate the services that you're interested in.

To add App Center Push to your app open a Terminal and navigate to the root of your Cordova project, then enter the following to add App Center Push to the app:

```js
cordova plugin add cordova-plugin-appcenter-push
```

## Intercept push notifications

TODO

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

## Disable automatic forwarding of application delegate's methods to App Center services

TODO

