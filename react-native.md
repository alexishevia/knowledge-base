Launch project (iOS)
----------------------------
create project:
```
react-native init { ProjectName }
```

Open the ios/ProjectName.xcodeproj file with XCode, select target device and
click on the Run (Play) button.

If you're testing on a real device, you need to modify the "localhost" on the
files:
- `AppDelegate.m`
- `./node_modules/react-native/Libraries/WebSocket/RCTWebSocketExecutor.m`
so it points to your dev machine. Also, visit the "General" tab on your XCode
project and make sure no warnings are displayed.

Frameworks / UI libraries
----------------------------
[Ignite](https://github.com/infinitered/ignite) - CLI, Generator and more
[NativeBase](http://nativebase.io/) - UI Framework
[ReactXP](https://microsoft.github.io/reactxp/) - A LIBRARY FOR BUILDING CROSS-PLATFORM APPS

IDE
----------------------------
[https://www.decosoftware.com/]()

Deploy / Push Code
----------------------------
[iTunes Connect documentation](https://goo.gl/orq2gq)
[TestFlight](https://developer.apple.com/testflight/)
[TestFairy](http://my.testfairy.com/)

Testing
----------------------------
https://medium.com/@thisbejim/testing-react-native-components-with-enzyme-d46bf735540

Analytics + Crash Reports
----------------------------
[https://fabric.io]()
[react-native-fabric](https://github.com/corymsmith/react-native-fabric)
[react-native-fabric-crashlytics](https://github.com/mikelambert/react-native-fabric-crashlytics)
[react-native-mixpanel](https://github.com/davodesign84/react-native-mixpanel)
[rn-redux-mixpanel](https://github.com/danscan/rn-redux-mixpanel)

To upload a new version of the app to iTunes Connect:
----------------------------
0. Make sure your app settings are pointing to your production API server.
1. Edit ios/ACP/AppDelegate.m and make sure jsCodeLocation is pointing to
   mainBundle instead of local server
2. Open the project on XCode and increase build number
3. navigate to Product > Scheme > Edit Scheme... in xcode and change Archive >
   Build Configuration from Debug to Release.
4. make sure the selected deploy target is "Generic iOS Device" (not a real
   phone nor a simulator), then go to Product > Archive.
5. Open XCode > Window > Organizer
6. Choose the latest version and click on Export > Save for iOS App Store
   Deployment
7. Open Xcode > Open Developer Tool > Application Loader > Deliver Your App and
   choose the ipa file created on step 6
8. If you're using Fabric, you'll need to download the dSYM file from iTunes Connect & upload it to Fabric. Open iTunes Connect > Select your App > Activity > [Latest Build] > Download dSYM

To generate a new APK:
----------------------------
More info:
https://facebook.github.io/react-native/docs/signed-apk-android.html

```
cd android && ./gradlew assembleRelease
```
You can now upload the apk from `android/app/build/outputs/apk/app-release.apk`

```
# Install to phone
adb install /Users/alexishevia/Projects/Quanto/android/app/build/outputs/apk/app-release.apk

# Uninstall to phone
adb uninstall [app.id]
adb uninstall com.quanto

# List all installed apps
adb shell 'pm list packages -f' | sed -e 's/.*=//' | sort
```


Generating app icons & launch screen
----------------------------
To generate icons use:
[MakeAppIcon](https://makeappicon.com/)

## iOS
Once you've generated your icons, go to xCode's project navigator and open file
`YourProject/Images.xcassets/AppIcon`. Drag the images from MakeAppIcon's
folder into the corresponding slots.

Also, while Images.xcassets is selected, click on the + icon and create a new
imageset called LaunchImage. Then follow this guide to get that image into
your launch screen:
[How to create a launch screen for an iOS app](https://youtu.be/Vz6tCgXgZFo?t=259)

## android
Follow this guide to add app icon:
[How to add app icons in React Native Android](http://harrymoreno.com/2016/01/21/add-launcher-icon-to-react-native-android-app.html)

Follow this guide to add splashscreen:
[Change splash screen in React Native Android app](https://medium.com/react-native-development/change-splash-screen-in-react-native-android-app-74e6622d699)

Note: I had to create an `app/res/values/colors.xml` file, since @color/gray
wasn't been recognized.
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
   <color name="white">#ffffff</color>
   <color name="gray">#fefefe</color>
</resources>
```
Also, if you get any errors, try running the project on
Android Studio, since it gives better error messages than the console.

In-App Purchases
----------------------------
[Testing In-App Purchases (ios)](https://developer.apple.com/library/mac/documentation/LanguagesUtilities/Conceptual/iTunesConnectInAppPurchase_Guide/Chapters/TestingInAppPurchases.html)
[react-native-in-app-utils module](https://github.com/chirag04/react-native-in-app-utils)

Geolocation
----------------------------
I found that [react-native-location](https://github.com/timfpark/react-native-location) provided more accurate results than the default Geolocation library built in React Native.

React Native Tutorials
----------------------------
[MakeItOpen](http://makeitopen.com/)

React Native Books
----------------------------
Learning React Native (Google Play Books)
