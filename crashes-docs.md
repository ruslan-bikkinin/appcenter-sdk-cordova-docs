# App Center Crashes

App Center Crashes will automatically generate a crash log every time your app crashes. The log is first written to the device's storage and when the user starts the app again, the crash report will be sent to App Center. Collecting crashes works for both beta and live apps, i.e. those submitted to the App Store. Crash logs contain valuable information for you to help fix the crash.

Please follow the [Getting Started_TODO]() section if you haven't set up the SDK in your application yet.

## Generate a test crash

App Center Crashes provides you with an API to generate a test crash for easy testing of the SDK. This API can only be used in test/beta apps and won't do anything in production apps.

```js
Appcenter.Crashes.generateTestCrash();
```

It's also easy to generate a JavaScript crash. Add the following line to your code, which throws a JavaScript error and causes a crash.

```js
throw new Error('This is a test javascript crash!');
```

> Tip
>
> Your Cordova app needs to be compiled in release mode for this crash to be sent to App Center.

## Get more information about a previous crash

App Center Crashes has two APIs that give you more information in case your app has crashed.

### Did the app crash in the previous session?

At any time after starting the SDK, you can check if the app crashed in the previous launch:

```js
var success = function(didCrash) {
    console.log("there was " + (didCrash ? "a" : "no") + " crash");
}

var error = function(error) {
    console.error(error);
}
Appcenter.Crashes.hasCrashedInLastSession(success, error);
```

This comes in handy in case you want to adjust the behavior or UI of your app after a crash has occured. Some developers chose to show additional UI to apologize to their users, or want way to get in touch after a crash has occured.

### Details about the last crash

If your app crashed previously, you can get details about the last crash.

```js
var success = function(crashReport) {
    //do something with crash report
}

var error = function(error) {
    console.error(error);
}
Appcenter.Crashes.lastSessionCrashReport(success, error);
```

## Customize your usage of App Center Crashes

App Center Crashes provides callbacks for developers to perform additional actions before and when sending crash logs to App Center.

### Processing crashes in JavaScript

You can configure SDK whether or not to send crash reports automatically or process crashes in JavaScript by changing preference `APPCENTER_CRASHES_ALWAYS_SEND` value in `config.xml`. To process crashes in JavaScript set it to `false` so any of the `Crash.setListener` methods will be working as expected.

```xml
<preference name="APPCENTER_CRASHES_ALWAYS_SEND" value="false" />
```

All the different callbacks of the event listener are discussed one by one in this document, but you need to set one event listener that define all callbacks at once.

### Should the crash be processed?

TODO - check if it was implemented for cordova

Implement this callback if you'd like to decide if a particular crash needs to be processed or not. For example, there could be a system level crash that you'd want to ignore and that you don't want to send to App Center.

```js
Crashes.setListener({

    shouldProcess: function (report) {
        return true; // return true if the crash report should be processed, otherwise false.
    },

    // Other callbacks must also be defined at the same time if used.
    // Default values are used if a method with return parameter is not defined.
});
```

### Ask for the users' consent to send a crash log

TODO - check if it was implemented for cordova

### Get information about the sending status for a crash log

TODO - check if it was implemented for cordova

### Add attachments to a crash report

TODO - check if it was implemented for cordova

## Enable or disable App Center Crashes at runtime

You can enable and disable App Center Crashes at runtime. If you disable it, the SDK will not do any crash reporting for the app.

```js
var success = function() {
    console.log("crashes disabled");
}

var error = function(error) {
    console.error(error);
}
AppCenter.Crashes.setEnabled(false, success, error);
```

To enable App Center Crashes again, use the same API but pass `true` as a parameter.

```js
var success = function() {
    console.log("crashes enabled");
}

var error = function(error) {
    console.error(error);
}
AppCenter.Crashes.setEnabled(true, success, error);
```

## Check if App Center Crashes is enabled

You can also check if App Center Crashes is enabled or not:

```js
var success = function(result) {
    console.log("crashes " + (result) ? "enabled" : "disabled");
}

var error = function(error) {
    console.error(error);
}
AppCenter.Crashes.isEnabled(success, error);
```









