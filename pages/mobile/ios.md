---
title: iOS
last_updated: July 2019
sidebar: primary_sidebar
permalink: mobile_ios.html
folder: mobile
---

## Development Environment

Xcode is used as the IDE for iOS development. 

iOS applications can be built in either Objective C or Swift. SafeTow is built in __Swift__.

The application project structure is very straightforward. The application is essentially just its "web view" with extra settings applied.

## Folder Structure

The "safetowios" includes the main files of the application. Essentially, the logic is all contained in __safetowios/ViewController.swift__ and the settings are found in __safetowios/Info.plist__. The __safetowios/Assets.xcassets__ contains the files for the icons.

The __safetowiosTests__ and __safetowiosUITests__ are used for testing, although this has not yet been built out.

### safetowios/ViewController.swift

This file is the equivalent of the "main" method. The UI View library is imported, and then the permanent URL where the application is hosted (_app.safetow.network_) is loaded in.

![xcode viewcontroller.swift](/images/documentation_images/xcode_viewcontroller_swift.png)

### safetowios/Info.plist

This file contains the main settings. Some important fields are the __"Bundle Display Name"__, and __"Privacy - Location When In Use Usage Description"__. These are the two non-default values here.

![xcode safetowios info.plist](/images/documentation_images/xcode_safetowios_info_plist.png)

### safetowios/Assets.xcassets

This file contains the icons. At this time, only the iPhone app icons have bene filled in, although more alternate icons can be supplied that would be used in notifications, "spotlight" view, and more.

![xcode assets.xcassets](/images/documentation_images/xcode%20assets.xcassets.png)

### safetowios/Main.storyboard

![ios main storyboard](/images/documentation_images/ios_main_storyboard.png)

This file has the visual editor that shows what part of the screen is taken up by the UIWebView. Using the GUI editor, the "My Web View" is dragged across the full width of the screen.

## Location Permissions

The location permissions are requested in the __safetowios/Info.plist__ under the _Privacy - Location When In Use Usage Description_ value.

I have yet to find a way to make it only ask one time. \#TODO eliminate the phase two "ask" that has the URL asking for permission.

### Frameworks and libraries

![ios linked frameworks libraries](/images/documentation_images/ios_linked_frameworks_libraries.png)

In order to get the location services to work, the __"CoreLocation.framework"__ must be loaded in to the application's __"Linked Frameworks and Libraries"__. This is found under the General settings tab of the main application folder.

### Screenshots

|Step 1|Step 2|
|+-+|
|![iOS Location Step 1](/images/documentation_images/ios_location_step_1.png)|![iOS Location Step 2](/images/documentation_images/ios_location_step_2.png)|

|Settings 1|Settings 2|
|+-+|
|![ios safetow settings 1](/images/documentation_images/ios_safetow_settings_1.png)|![ios safetow settings 2](/images/documentation_images/ios_safetow_settings_2.png)|

## Emulator Screenshot

|iOS home screen|Application|
|+-+|
|![iOS Home screen](/images/documentation_images/ios_home_screen.png)|![iOS application](/images/documentation_images/ios_customer_home.png)|

## How to put on development device

Plug your iPhone into your computer through a USB connection and open up Xcode.

In the top left corner of the Xcode window you will find a play button next to a UI element that displays the application name and a device option.

![xcode device deploy](/images/documentation_images/xcode_device_deploy.png)

Select the device option on the right and you will be able to select where you want to deploy your application. Your options will include all of the virtual emulators and at the top of the list any physical devices you have plugged in.

![xcode device deploy options](/images/documentation_images/xcode_device_deploy_options.png)


Select the physical device to close the prompt, and then hit the play button.

The application will deploy onto your device like any other application installed.

## How to manage on App Store