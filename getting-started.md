
# Get Started with React Native

> [!div class="op_single_selector"]
> * [Android](android.md)
> * [iOS](ios.md)
> * [React Native](react-native.md)
> * [UWP](uwp.md)
> * [Xamarin](xamarin.md)
> * [macOS](macos.md)
> * [Cordova](cordova.md)

The App Center SDK uses a modular architecture so you can use any or all of the services.

Let's get started with setting up App Center Cordova SDK in your app to use App Center Analytics and App Center Crashes.

## 1. Prerequisites

TO DO

Before you begin, please make sure that the following prerequisites are met:


## 2. Create your app in the App Center Portal to obtain the App Secret

If you have already created your app in the App Center portal, you can skip this step.

1. Head over to [appcenter.ms](https://appcenter.ms).
2. Sign up or log in and hit the blue button on the top right corner of the portal that says **Add new** and select **Add new app** from the dropdown menu.
3. Enter a name and an optional desciption for your app.
4. Select the appropriate OS (Android or iOS) and select **Cordova** as the platform.
5. Hit the button at the bottom right that says **Add new app**.

Once you have created an app, you can obtain its **App Secret** on the **Getting Started** page or **Settings** page on the App Center Portal.

> [!NOTE]
> App secret is like an api key for your app, it allows events and telemetry to be sent to App Center backend. It doesn't provide any access to your account. It can't be used to invoke App Center REST APIs (like trigger builds or send push notifications). If your code is open source, we recommend you inject the secret at build or in a similar way.

## 3. Add the App Center SDK modules

The default integration of the SDK uses CocoaPods for iOS. If you are not using CocoaPods in your app, you need to integrate the Cordova SDK manually for your iOS app.


1. Open a Terminal and navigate to the root of your Cordova project, then add any of the following plugins using the CLI to access analytics, crash, or push respectively:

	```
    cordova plugin add cordova-plugin-appcenter-analytics
    cordova plugin add cordova-plugin-appcenter-crashes
    cordova plugin add cordova-plugin-appcenter-push
    ```

	The App Center SDK uses a modular approach, where you just add the modules for App Center services that you want to use. **appcenter-analytics** and
	**appcenter-crashes** make sense to add to almost every app, as they provide value with no additional setup required. **appcenter** provides general
	purpose App Center [APIs](TODO), useful for multiple services.

2.  Link the plugins to the Cordova app

    To get it working in your app you will need to add some configuration values to your app configuration in `config.xml` file. See list of available parameters below

- `APP_SECRET` - _(required)_ App secret which enables App Center to map this app to the right user account

  Example:

  ```xml
  <platform name="android">
      <preference name="APP_SECRET" value="7a72dae0-f811-451b-8ae8-ecf7973e8359" />
  </platform>
  ```

  Notice that it's likely that Android and iOS platforms will be associated with different applications on App Center portal so you would need to add this preference twice - one for Android (as in example above) and another for iOS.

## 4. Configuration Preferences 

- `APPCENTER_ANALYTICS_ENABLE_IN_JS` - _(optional, default is "false")_ This preference controls whether Analytics will be enabled automatically (default option) or will require call to `Analytics.setEnabled()` in JS code before sending any usage data to App Center portal. This might be useful e.g. in case when an application may want to ask users whether they want to share analytics information.

  Example:

  ```xml
  <preference name="APPCENTER_ANALYTICS_ENABLE_IN_JS" value="true" />
  ```

- `APPCENTER_CRASHES_ALWAYS_SEND` - _(optional, default is "true")_ Specifies whether crash reports will always be sent automatically or would be available for processing in JavaScript  code. Opting to process crashes first means more work for the developer, but greater control over user privacy and allows you to attach a message with a crash report.

  Example:

  ```xml
  <preference name="APPCENTER_CRASHES_ALWAYS_SEND" value="false" />
  ```
