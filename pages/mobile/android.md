---
title: Android
last_updated: July 2019
sidebar: primary_sidebar
permalink: mobile_android.html
folder: mobile
---

## Development Environment

Android Studio is used as the IDE for Android development. It is built by JetBrains and very similar to RubyMine, utilizing almost all the same shortcuts and UI elements.

iOS applications can be built in either Java or Kotlin. Kotlin is a language with full interoperability with Java, and built on the Java Virtual Machine utilizing all of the same libraries - it is like Java with concise syntax. SafeTow is built in __Kotlin__.

The application project structure is very straightforward. The application is essentially just its "web view" with extra settings applied.

## Folder Structure

![SafeTow Android Folder Structure](/images/documentation_images/safetow_android_folder_structurer.png)

The application is divided up between the __app__ directory and the __Gradle Scripts__. Everything that needs to be edited is within the __app__ directory. 

The __manifests__ contains the main _AndroidManifest.xml_ file: the outline of the application.

The __java__ folder contains all of the classes and "logic" code that is used in the application. 
- Notice how the folder is titled Java, yet code is written in Kotlin, this shows how Kotlin is just Java in new Syntax, and Java code can also be included here together with it. Since May 2019, Google has officially recommended that all Android apps should be written in Kotlin instead of Java.

The __res/drawable__ folder contains the resources, of any images we want to include. There is a _towtruck.png_ file in this folder as an icon to be displayed during startup.

The __res/layout__ folder contains the logic for how the page layout works.

### AndroidManifest.xml

![AndroidManifest.xml](/images/documentation_images/android_manifest.png)

This file is the outline of the application.

It begins in the __uses-permission__ tags to define what the application requires: in our case that is internet and location services. 

Within the __application__ tag, there are listings for __activity__. Each of the activities correspond to a class written in Kotlin in the _app/java/com.example.safetow_ folder. The two activities for our application are:
- __SplashScreenActivity__: This is the loading icon for when the application is starting up, so that users don't just see a blank screen as the webpage loads.
- __WebViewActivity__: This is the WebView container that wraps the webpage hosted at "_app.safetow.network_".

### SplashScreenActivity

This file displays a 'splash screen' with a icon of a tow truck while the webview loads at startup.

Notice on __line 13__ that it is linked to the _app/res/layout/activity_splash_screen.xml_ file.

### WebViewActivity

This file contains all the logic of the Web View. There are a lot of imports required from Android development libraries to manage all of the services involved.

The file contains two types of functions.
 
Some functions such as __isNetworkAvailable()__ are written from scratch. They provide logic and they exist entirely within the scope of this class.

```kotlin
    private fun isNetworkAvailable(): Boolean {
        val connectionManager =
                this@WebViewActivity.getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
        val networkInfo = connectionManager.activeNetworkInfo
        return networkInfo != null && networkInfo.isConnectedOrConnecting
    }
```

Other functions are _overrides_, such as __onResume()__. These functions are included in the libraries that are imported at the top of the application, but we want to change the behavior of the function in some way.

For this particular example, the original function would have just resumed the application from a state where it was "paused" with an error dialog. We only want the application to resume if the error is solved, so if the application is resumed while __isNetworkAvailable()__ is resolving to a null value, it will call the error dialog again.

```kotlin
    override fun onResume() {
        super.onResume()

        if (isAlreadyCreated && !isNetworkAvailable()) {
            isAlreadyCreated = false
            showErrorDialog("Error", "No internet connection. Please check your connection.",
                this@WebViewActivity)
        }
    }
```

Our main function of concern here is __OnCreate__, which will begin as the class loads. It's functionality is as follows:
- Start with __startLoaderAnimate__ to have an animation while the webview loads.
- Create a new __WebViewClient__ object. If the webview is able to load, finish the animation. If the webview cannot load because there is no internet connection, display a prompt to start up the internet.
- Create a new __WebChromeClient__ to hold the logic for the location services. If permissions for locations are not working correctly, call the functions with the associated prompts and display them.
- Finally, assuming the previous steps are overcome, display the _URL_ that resolves to _app.safetow.network_ in the webview.

## Location Permissions

The location permissions are set from the Android Manifest.xml file with the following code:

```xml
<!-- Application can access the internet-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

<!-- Application can access the fine location (latitude and longitude) -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

### Screenshtos

|Settings 1|Settings 2|
|+-+|
|![android safetow settings 1](/images/documentation_images/android_safetow_settings_1.png)|![android safetow settings 2](/images/documentation_images/android_safetow_settings_2.png)|

## Emulator Screenshot

|Android home screen|Application|
|+-+|
|![Android Home screen](/images/documentation_images/android_home_screeen.png)|![Android application](/images/documentation_images/android_customer_home.png)|

## How to put on development device

First you need to make sure that your Android device has developer options enabled. The official guide to do so is [here](https://developer.android.com/studio/debug/dev-options), but it is usually summarized in the following steps:
- Go to your phone's system settings
- Go to __About Phone__
- Select the __Android Build Version Number__ (or similar text) and tap it 7 times
- __Developer Options__ is now available in your main settings menu, go there
- Enable USB debugging
- Plug your phone into your computer through a USB connection

From the top menu bar, select __Run__ > __Run 'app'__.

A pop-over window will appear that has your options on where to load the application.

![select deployment target](/images/documentation_images/android_select_deployment_target.png)

Your __"Connected Devices"__ correspond to physical Android devices plugged into your computer.

The __"Virtual Devices"__ correspond to emulator windows where you can run the phone on your computer.

Select the device you would like to run the application on, and select __OK__.

Now the application will be installed to your phone.

## How to manage on Google Play

\#TODO