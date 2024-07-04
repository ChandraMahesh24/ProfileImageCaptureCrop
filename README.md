# ProfileImageCaptureCrop
capturing an image from the camera or picking one from the gallery and then cropping it using the UCrop library in an Android application


Permissions
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.CAMERA" />

FileProvider Setup: To use FileProvider, configure it in your AndroidManifest.xml:
    <provider
        android:name="androidx.core.content.FileProvider"
        android:authorities="com.example.yourapp.fileprovider"
        android:exported="false"
        android:grantUriPermissions="true">
        <meta-data
            android:name="android.support.FILE_PROVIDER_PATHS"
            android:resource="@xml/file_paths" />
    </provider>

And create a res/xml/file_paths.xml to specify the allowed paths:

  <?xml version="1.0" encoding="utf-8"?>
  <paths xmlns:android="http://schemas.android.com/apk/res/android">
      <external-path
          name="my_images"
          path="Android/data/com.example.yourapp/files/Pictures" />
  </paths>

UCrop Setup: Ensure that UCrop is properly added to your build.gradle:
  implementation 'com.github.yalantis:ucrop:2.2.6'


 1 Purpose: To initiate the camera and capture a photo.
    Process:
    Intent Creation: Creates an Intent to capture an image.
    Check for Camera App: Ensures there’s an app to handle the intent.
    File Creation: Calls createImageFile() to create a file to store the image.
    Set Output URI: Uses FileProvider to get a fileUri for storing the captured image.
    Launch Camera: Starts the camera app to capture the image, with the image saved to the specified fileUri.
    
2. CameraLauncher Activity Result Handler
  Purpose: To handle the result from the camera app and start the UCrop activity for cropping.
  Process:
  Check Result: Ensures the result code is RESULT_OK, indicating a successful image capture.
  Prepare UCrop: Creates an output URI and configures UCrop options.
  Start UCrop: Initiates UCrop to crop the captured image.

4. GalleryLauncher Activity Result Handler
    Purpose: To handle the result from the camera app and start the UCrop activity for cropping.
    Process:
    Check Result: Ensures the result code is RESULT_OK, indicating a successful image capture.
    Prepare UCrop: Creates an output URI and configures UCrop options.
    Start UCrop: Initiates UCrop to crop the captured image.
   
5. GalleryLauncher Activity Result Handler
   Purpose: To open the media picker for selecting images from the gallery.
  Process:
  Check Version: Determines the Android version to decide whether to check for permissions.
  Check Permissions: Calls utility methods to check/request storage permissions if required.
  Open Gallery: Calls openIntentChooser() if permissions are granted.
6. openIntentChooser() Method
     Purpose: To launch the gallery for selecting an image.
    Process:
    Create Intent: Creates an intent for picking images from external content.
    Launch Gallery: Starts the gallery app to allow the user to select an image.

