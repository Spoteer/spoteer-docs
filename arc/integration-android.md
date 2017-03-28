# Arc for Android - Integration Guide

### REQUIREMENTS
- Latest Android development environment.
- Android 2.3 - Gingerbread (API level 9) or later.

### Installation
This section describes how to integrate **Arc** into an existing project.

##### ANDROID STUDIO
Open build.gradle file and add **Spoteer**'s repository, **Arc** and **play-services** dependancies:

```
repositories {
	mavenCentral()
	maven { url 'SPOTEER-MAVEN-URL' }
}
	
dependencies {
  compile 'com.spoteer:arc:1.0.+@aar'
  compile 'com.google.android.gms:play-services:9.2.1'
}
```

### Activation
1 - Add the following **permissions** to the **AndroidManifest.xml**:

```xml
<manifest>
        <!-- Basic permissions -Required for running the Arc SDK -->
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
	
        <!-- Location Permissions - Required for collecting location signals -->
        <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="com.google.android.gms.permission.ACTIVITY_RECOGNITION" />
	
        <!-- Additional data Permissions - Required for improving accuracy -->
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.READ_CONTACTS" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
</manifest>
```
2 - Add the following application elements to the **AndroidManifest.xml**:
```xml
<application>
  ...
  <service
            android:name="com.spoteer.arc.ArcService"
            android:enabled="true"
            android:exported="false"
            android:process=":background" />

    <receiver
            android:name="com.spoteer.arc.ArcReceiver"
            android:enabled="true"
            android:exported="true"
            android:process=":background">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="com.spoteer.arc.action.SAMPLE" />
                <action android:name="com.spoteer.arc.action.INIT" />
            </intent-filter>
    </receiver>
  ...
</application>
```
3 - If your project doesn't have the Google Play Services SDK, please add it by following these instructions:
https://developers.google.com/android/guides/setup
4 - Activate the **Arc** service
Add a call to the Arc.activate() method in your applications first activity. This call receives the application context. Here is a simple example:
```java
import com.spoteer.arc.Arc;

public class SplashScreenActivity extends Activity {
  @Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      Arc.activate(getApplicationContext());
      // here comes the rest of your Activity code
  }
}
```
5 - Add Android 6 support
Beginning in Android 6.0 (API level 23), users grant location permissions while the app is running using a Dialog. Call Arc.requestPermissionsRuntime() with the relevant activity, to show the location permission dialog. If the SDK is running on an older Android version, this method will not do anything.
```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Arc.activate(getApplicationContext());

        Arc.requestPermissionsRuntime(this);
    }
}
```
