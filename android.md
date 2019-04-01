# Installation

## Ubuntu

Install Oracle JAVA
```
sudo apt-add-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

Add `JAVA_HOME` to `.bashrc`:
```
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

Remove built-in android libraries:
```
sudo apt-get remove android-tools-adb android-tools-fastboot
```

Download Android Command Line Tools from
https://developer.android.com/studio/index.html
(you don't need the complete Android Studio, just the SDK)

Extract the .tar.gz into ~/android-sdk

Add binaries to PATH:
```
export PATH=$PATH:~/android-sdk/tools
export PATH=$PATH:~/android-sdk/platform-tools
```

You can start the Android SDK Manager with `android`

# Useful links

[Android SDK](https://developer.android.com/index.html)

[Genymotion emulator](https://www.genymotion.com/)

[Ghostlab](http://www.vanamco.com/ghostlab/) - Synchronized browser testing for
web and mobile. Remote debugging.
