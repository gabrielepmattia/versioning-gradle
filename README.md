# Script for versioning
This simple script will allow you to auto-increment the build version in *Android Studio*.

## Description
- `gradle.properties` store the current build version
- `versioning.gradle` contains the script
- `versionName` is the human-readable version (as `2.4.12`)
- `versionCode` is a progressive integer that raises on every build, it allows the system to understand which version is earlier of another

The script increases automatically the version name but only the last integer, for example `0.4.2` to `0.4.3` so if you want to increase the second or the first integer you have to do it manually, so `0.5.0` and on next build it will become `0.5.1` and so on. Instead, please never edit the `versionCode`!

## Instructions
Suppose that `app/` is the folder where you have `/src` and `/res`. Just copy this repo structure in your working folder and just add to your `app/build.gradle` at the top of the file:

`apply from: 'versioning.gradle'`

and in your `defaultConfig` scope
```
    defaultConfig {
        applicationId "com.company.yourappid"
        minSdkVersion ..
        targetSdkVersion ..
        versionCode newVersionCode.toInteger()
        versionName newVersionName
        project.setVersion(newVersionName)
        println 'Currently building version ' + project.getVersion() + " build " + newVersionCode
    }
```

Whenever you will build your `app` configuration, version (that is written `gradle.properties`) will be increased.