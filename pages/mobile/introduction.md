---
title: Introduction
last_updated: July 2019
sidebar: primary_sidebar
permalink: mobile_introduction.html
folder: mobile
---

SafeTow is a "hybrid" application, it is not a "native" application.

This means that it is a web application that runs at a specific URL (_https://app.safetow.network_) and then we have a mobile app that opens up that URL and displays it on a phone as if it was an application written natively for a phone.

From the end-user's perspective, everything is essentially working the same. They open an app on their home screen that says "SafeTow" and then they can use all of the features.

This works with the _"UIWebView"_ in iOS and the _"WebView"_ in Android.

## Project files

Each mobile application exists with its own codebase, that is hosted on AWS CodeCommit.

- [Android Application git repository (safetow-android)](https://us-east-1.console.aws.amazon.com/codesuite/codecommit/repositories/safetow-android/browse?region=us-east-1)
- [iOS Application git repository (safetow-ios)](https://us-east-1.console.aws.amazon.com/codesuite/codecommit/repositories/safetow-ios/browse?region=us-east-1)

## Application running on emulators

### iOS

|iOS home screen|Application|
|+-+|
|![iOS Home screen](/images/documentation_images/ios_home_screen.png)|![iOS application](/images/documentation_images/ios_customer_home.png)|

### Android

|Android home screen|Application|
|+-+|
|![Android Home screen](/images/documentation_images/android_home_screeen.png)|![Android application](/images/documentation_images/android_customer_home.png)|

## Sensors and Permissions

The application requires usage of Location data to properly work. The web application takes the location data from the 'webview', where it is passed from the system. Permissions are asked of the user on the application level to allow location services to work.

### iOS

I have yet to find a way to make it only ask one time. \#TODO eliminate the phase two "ask" that has the URL asking for permission.

|Step 1|Step 2|
|+-+|
|![iOS Location Step 1](/images/documentation_images/ios_location_step_1.png)|![iOS Location Step 2](/images/documentation_images/ios_location_step_2.png)|

### Android

On Android, I have successfully set up so that there is only one prompt for location services to be asked for.

|Step 1||
|+-+|
|![iOS Location Step 1](/images/documentation_images/android_location_prompt.png)||