
# Get Started with Cordova

The App Center SDK uses a modular architecture so you can use any or all of the services.

Let's get started with setting up App Center Cordova SDK in your app to use App Center Analytics and App Center Crashes.

## 1. Prerequisites

Before you begin, please make sure that the following prerequisites are met:

* You are using a Cordova project that runs the following:
	* `cordova` engine 6.4.0 or later
	* `cordova-android` engine 4.1.0 or later
	* `cordova-ios` engine 4.3.0 or later
* For iOS, the default way to use the SDK requires CocoaPods. If you haven't installed CocoaPods, please follow the [CocoaPods Getting Started](https://guides.cocoapods.org/using/getting-started.html) to do so.

## 2. Create your app in the App Center Portal to obtain the App Secret

If you have already created your app in the App Center portal, you can skip this step.

1. Head over to [appcenter.ms](https://appcenter.ms).
2. Sign up or log in and hit the blue button on the top right corner of the portal that says **Add new** and select **Add new app** from the dropdown menu.
3. Enter a name and an optional desciption for your app.
4. Select the appropriate OS (Android or iOS) and select **Cordova** as the platform.
5. Hit the button at the bottom right that says **Add new app**.

Once you have created an app, you can obtain its **App Secret** on the **Getting Started** page or **Settings** page on the App Center Portal.

> Note
>
> App secret is like an api key for your app, it allows events and telemetry to be sent to App Center backend. It doesn't provide any access to your account. It can't be used to invoke App Center REST APIs (like trigger builds or send push notifications). If your code is open source, we recommend you inject the secret at build or in a similar way.

## 3. Add the App Center SDK modules

1. Open a Terminal and navigate to the root of your Cordova project, then add any of the following plugins using the CLI to access analytics, crash, or push respectively:

	```
    cordova plugin add cordova-plugin-appcenter-analytics
    cordova plugin add cordova-plugin-appcenter-crashes
    cordova plugin add cordova-plugin-appcenter-push
    ```

	The App Center SDK uses a modular approach, where you just add the modules for App Center services that you want to use. **cordova-plugin-appcenter-analytics** and **cordova-plugin-appcenter-crashes** make sense to add to almost every app, as they provide value with no additional setup required. **appcenter** provides general purpose App Center [APIs__REFER_TO_Sdk\Other APIs\Cordova](), useful for multiple services.

2.  Link the plugins to the Cordova app

    To get it working in your app you will need to add some configuration values to your app configuration in `config.xml` file. See list of available parameters below

- `APP_SECRET` - _(required)_ App secret which enables App Center to map this app to the right user account

  Example:

  ```xml
  <platform name="android">
      <preference name="APP_SECRET" value="0000-0000-0000-0000-000000000000" />
  </platform>
  <platform name="ios">
      <preference name="APP_SECRET" value="0000-0000-0000-0000-000000000000" />
  </platform>
  ```

  Notice that it's likely that Android and iOS platforms will be associated with different applications on App Center portal so you would need to add this preference twice - one for Android (as in example above) and another for iOS.

## 4. Configuration Preferences 

- `APPCENTER_ANALYTICS_ENABLE_IN_JS` - _(optional, default is "false")_ This preference controls whether Analytics will be enabled automatically (default option) or will require call to `Analytics.setEnabled()` in JS code before sending any usage data to App Center portal. This might be useful e.g. in case when an application may want to ask users whether they want to share analytics information. [Learn more about sending user events manually__TODO_REFER_TO_Sdk\Anaytics\Cordova]().

  Example:

  ```xml
  <preference name="APPCENTER_ANALYTICS_ENABLE_IN_JS" value="true" />
  ```

- `APPCENTER_CRASHES_ALWAYS_SEND` - _(optional, default is "true")_ Specifies whether crash reports will always be sent automatically or would be available for processing in JavaScript  code. Opting to process crashes first means more work for the developer, but greater control over user privacy and allows you to attach a message with a crash report. [Learn more about processing on crash reports in JS__TODO_REFER_TO_Sdk\Crashes\Cordova]().

  Example:

  ```xml
  <preference name="APPCENTER_CRASHES_ALWAYS_SEND" value="false" />
  ```
  
## 5. Start the SDK

Now you can build and launch your application either from command line or Xcode/Android Studio.

## 5.1 Build and run your application from command line

You may build and launch your iOS application by the following command:

```shell
cordova run ios
```

> Tip
>
> You can launch it on an **iOS simulator** or **iOS device** by specifying the iOS device name in 
>
> `cordova run ios --target="myDeviceName".`

You may build and launch your Android application by the following command:

```shell
cordova run android
```

> Tip
>
> You can launch it on an **android emulator** or **android device** by specifying the device id in 
>
> `cordova run android --target "myDeviceId"` (`deviceId` from `adb devices` command).

## 5.2 Build and run your application from Xcode or Android Studio

For iOS, open your `ios/{appname}.xcworkspace` in Xcode and build from there.

For Android, import your **android** project in Android Studio and build from there.

Great, you are all set to visualize Analytics and Crashes data on the portal that the SDK collects automatically. There is no additional setup required. Look at [Analytics__TODO_REFER_TO_Sdk\Analytics\Cordova]() and [Crashes__TODO_REFER_TO_Sdk\Crashes\Cordova]() section for APIs guides and walkthroughs to learn what App Center can do.
