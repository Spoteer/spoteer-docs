# Beam for Android - Integration Guide

### REQUIREMENTS
- Latest Android development environment.
- Android 2.3 - Gingerbread (API level 9) or later.

### Installation
This section describes how to integrate **Beam** into an existing project.

##### ANDROID STUDIO
Open build.gradle file and add **Spoteer** repository, **Beam** and **play-services** dependancies:

```gradle
repositories {
	mavenCentral()
	maven { 
        	url 'http://maven.spoteer.com/artifactory/beam'
		credentials {
			username = "<USERNAME>"
			password = "<PASSWORD>"
		}		
	}
}

dependencies {
  compile 'com.spoteer:beam:1.0.0'
  compile 'com.google.android.gms:play-services:9.2.1'
}
```

### Activation
1 - Add the following **permissions** to the **AndroidManifest.xml**:

```xml
<manifest>
        <!-- Basic permissions -Required for running the Arc SDK -->
        <uses-permission android:name="android.permission.INTERNET" /> <!-- Mandatory -->
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> <!-- Mandatory -->
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" /> <!-- Mandatory -->
	
        <!-- Location Permissions - Required for collecting location signals -->
        <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" /> <!-- Mandatory -->
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="com.google.android.gms.permission.ACTIVITY_RECOGNITION" />
</manifest>
```
2 - Add the following application elements to the **AndroidManifest.xml**:

```xml
<application>
  ...
  <service
            android:name="com.spoteer.beam.BeamService"
            android:enabled="true"
            android:exported="false"
            android:process=":background" />

    <receiver
            android:name="com.spoteer.beam.BeamReceiver"
            android:enabled="true"
            android:exported="true"
            android:process=":background">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="com.spoteer.beam.action.INIT" />
            </intent-filter>
    </receiver>
  </service>
  
  <activity-alias android:targetActivity="com.spoteer.beam.MainActivity"
            android:name="BeamActivity">
            <intent-filter>
                <action android:name="com.spoteer.beam.action.SHOW" />
                <action android:name="com.spoteer.beam.action.HIDE" />
            </intent-filter>
  </activity-alias>
  ...
</application>
```
3 - If your project doesn't have the Google Play Services SDK, please add it by following these instructions:
https://developers.google.com/android/guides/setup

4 - Activate the **Beam** service

Add a call to the Beam.activate() method in your application's first activity. This call receives the application context. Here is a simple example:
```java
import com.spoteer.beam.Beam;

public class SplashScreenActivity extends Activity {
  @Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      Beam.activate(getApplicationContext());
      // here comes the rest of your Activity code
  }
}
```
5 - Add Android 6 support

Beginning in Android 6.0 (API level 23), users grant location permissions, while the app is running, using a Dialog. Call Arc.requestPermissionsRuntime() with the relevant activity, to show the location permission dialog. If the SDK is running on an older Android version, this method will not do anything.
```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Beam.activate(getApplicationContext());

        Beam.requestPermissionsRuntime(this);
    }
}
```

6 - Whenever it's time to play Spoteer content, call the `show` method with a callback listener:
```java
import com.spoteer.beam.util.OnShowResponse;
import com.spoteer.beam.util.ShowResponse;

...

Beam.show(getApplicationContext(), new OnShowResponse() {
         public void response(ShowResponse response) { 
            Log.i("beam-show-response", String.format("success: %s", response.success));
         }
     });
```

  `ShowResponse` has the following properties:
 
   **success**: boolean value represents the accomplishment of the `show` request
     
     
7 - Whenever it's time to stop/hide Spoteer content, call the `hide` method with a callback listener:
```java
import com.spoteer.beam.util.OnHideResponse;
import com.spoteer.beam.util.HideResponse;

...

Beam.show(getApplicationContext(), new OnHideResponse() {
         public void response(HideResponse response) { 
            Log.i("beam-hide-response", String.format("success: %s", response.success));
         }
     });
```

  `HideResponse` has the following properties:
  
   **success** boolean value represents the accomplishment of the `hide` request
