# Android Project template for Amulet

Creating an Android Project for building .apks from Amulet involved a few steps in relation to dependencies.

I've written up what was done to get the builds working since my memory is terrible.

# Project

I created a Project without an activity. For the name and path I used `xyz.amulet`.

# minSdk, targetSdk

On the app build.graddle, I used:

    minSdkVersion 14
    targetSdkVersion 28

Starting November 1st, 2018, all Google Play apps must target Sdk 28 or newer.

minSdk 14 means we pretty much cover every device available.

# Dependencies

On the app build.gradle, we need three dependencies:

Google Play services - was getting errors with 'version not found' but 12.0.1 does the trick.

    implementation 'com.google.android.gms:play-services:12.0.1'

In order to build with Gradle from the commandline, we need to be able to run tests

    testImplementation 'junit:junit:4.12'

Multidex - this is required to build APKs as we go beyond the methods limit. Oh well.

    implementation 'com.android.support:multidex:1.0.3'

Final dependencies look like this:

    dependencies {
        implementation fileTree(dir: 'libs', include: ['*.jar'])
        testImplementation 'junit:junit:4.12'
        implementation 'com.google.android.gms:play-services:12.0.1'
        implementation 'com.android.support:multidex:1.0.3'
    }


## Multidex

On app build.gradle, added `multiDexEnabled true`, as below

    defaultConfig {
        ...
        minSdkVersion 14
        targetSdkVersion 28
        multiDexEnabled true
        ...
    }

On AndroidManifest.xml, added

        android:name="android.support.multidex.MultiDexApplication"

Just before the <application> closing tag

        <application
        ...
        android:name="android.support.multidex.MultiDexApplication">

This way we don't have to fudge around with the Activity file class

# AmuletActivity.java

Copied from:
    
    https://github.com/ianmaclarty/amulet/blob/master/android/src/xyz/amulet/AmuletActivity.java

To:

    app/src/main/java/xyz/amulet/AmuletActivity.java

# libamulet.so

Copied from the zip file available on the website, from:

    builds/android/lua51/release/bin/libamulet.so

To:
    
    app/src/main/jniLibs/armeabi-v7a/libamulet.so


