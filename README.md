

UnsplashPhotoPicker is an Android UI component that allows you to quickly search the Unsplash library for free high-quality photos with just a few lines of code.

iOS photo picker [here](https://github.com/unsplash/unsplash-photopicker-ios).

![Unsplash Photo Picker for Android preview](https://github.com/unsplash/unsplash-photopicker-android/blob/dev/unsplash-photo-picker-android.png "Unsplash Photo Picker for Android")


## Description

`UnsplashPhotoPicker` is a Kotlin object you use to initialize the library. You present the picker by navigating to the `UnsplashPickerActivity` to offer your users to select one or multiple photos from Unsplash. Once they have selected photos, the `UnsplashPickerActivity` returns `UnsplashPhoto` objects that you can use in your app.

## Requirements

- Android minimum API 21+
- Android Studio 3.3+
- Kotlin 1.3+
- Use AndroidX artifacts when creating your project
- [Unsplash API Access Key and Secret Key](https://unsplash.com/documentation#registering-your-application)

## Installation

### Gradle

To integrate `UnsplashPhotoPicker` into your Android Studio project using Gradle, specify in your project `build.gradle` file:

```gradle
allprojects {
   repositories {
      ...
      maven { url  'https://jitpack.io' }
   }
}
```
And in your app module `build.gradle` file, replacing `x.y.x` by the latest [tag](https://github.com/unsplash/unsplash-photopicker-android/tags):

```gradle
dependencies {
   implementation 'com.github.unsplash:unsplash-photopicker-android:x.y.z'
}
```

## Usage

❗️Before you get started, you need to register as a developer on our [Developer](https://unsplash.com/developers) portal. Once registered, create a new app to get an **Access Key** and a **Secret Key**.

### Configuration

The `UnsplashPhotoPicker` is a Kotlin object you need to use in order to initialize the library. Add this in your custom application class `onCreate` method:

```kotlin
UnsplashPhotoPicker.init(
            this, // application
            "your access key",
            "your secret key"
            /* optional page size */
        )
```
| Property                      | Type          | Optional/Required | Default |
|-------------------------------|---------------|-------------------|---------|
| **`application`**             | _Application_ | Required          | N/A     |
| **`accessKey`**               | _String_      | Required          | N/A     |
| **`secretKey`**               | _String_      | Required          | N/A     |
| **`pageSize`**                | _Int_         | Optional          | `20`    |

### Presenting

In order to access the picker screen you need to navigate to the `UnsplashPickerActivity`. This activity has a `getStartingIntent` method to create the `Intent` needed:

```kotlin
startActivityForResult(
                UnsplashPickerActivity.getStartingIntent(
                    this, // context
                    isMultipleSelection
                ), REQUEST_CODE
            )
```

### Using the results

Your calling activity must use a `startActivityForResult` method to be able to retrieve the selected `UnsplashPhoto`:

```kotlin
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        if (resultCode == Activity.RESULT_OK && requestCode == REQUEST_CODE) {
            val photos: ArrayList<UnsplashPhoto>? = data?.getParcelableArrayListExtra(UnsplashPickerActivity.EXTRA_PHOTOS)
            // use your photos here
        }
}
```

See [UnsplashPhoto.kt](https://github.com/unsplash/unsplash-photopicker-android/blob/master/photopicker/src/main/java/com/unsplash/pickerandroid/photopicker/data/UnsplashPhoto.kt) for more details.



