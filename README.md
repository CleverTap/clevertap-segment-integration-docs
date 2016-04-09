## Getting Started

Once the Segment library is integrated, toggle CleverTap on in your Segment integrations, and add your CleverTap Account ID and CleverTap Account Token which you can find in the CleverTap Dashboard under Settings.

CleverTap supports the identify and track methods.

## Identify

When you identify a user, we'll pass that user's information to CleverTap with userId as CleverTap's Identity value. Segment's special traits recognized as CleverTap's standard user profile fields (in parentheses) are:

- name (Name)
- birthday (DOB)
- avatar (photo)
- gender (Gender)
- phone (Phone)
- email (Email)

All other traits will be sent to CleverTap as custom attributes.


## Track

When you track an event, we will send that event to CleverTap as a custom event.


## Android

### Integrating

1. Add the CleverTap Segment Integration dependency to your app build.gradle:

    `compile 'com.clevertap.android:clevertap-segment-android:+'`

    **Note**: Our group Id is com.clevertap.android and not com.segment.analytics.android.integrations.

2. Next, declare CleverTap's integration in your Analytics instance:

   ``` 
   Analytics analytics = new Analytics.Builder(context, "YOUR_WRITE_KEY_HERE")  
     .use(CleverTapIntegration.FACTORY)  
     ...  
     .build();  
   ```

### Integrating Push     

1. In your AndroidManifest.xml, add relevant permissions.  

    ```
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    <permission android:name="[YOUR_PACKAGE_NAME].permission.C2D_MESSAGE" android:protectionLevel="signature"/>
    <uses-permission android:name="[YOUR_PACKAGE_NAME].permission.C2D_MESSAGE" />
    ```

2. In your AndroidManifest.xml, register CleverTap's GcmBroadcastReceiver.  

    ```
    <receiver
        android:name="com.clevertap.android.sdk.GcmBroadcastReceiver"
        android:permission="com.google.android.c2dm.permission.SEND">  
        <intent-filter>  
            <action android:name="com.google.android.c2dm.intent.RECEIVE" />  
            <action android:name="com.google.android.c2dm.intent.REGISTRATION" />  
            <category android:name="[YOUR_PACKAGE_NAME]" />  
        </intent-filter>  
    </receiver>`  
    ```

3. Inside the application tag of your AndroidManifest.xml, add your GCM Sender ID and google play services version.

    ```
    <meta-data  
        android:name="GCM_SENDER_ID:    
        android:value="id:YOUR_SENDER_ID" />  
    ```    
    ```
    <meta-data  
        android:name="com.google.android.gms.version"  
        android:value="@integer/google_play_services_version" />    
    ```

4. For more in-depth information, visit our [Android push integration documentation](https://support.clevertap.com/integration/android-sdk/#push-notification-support).

### In-App Notifications

1. In your AndroidManifest.xml, add the CleverTap InAppNotificationActivity.

    ```
    <activity  
            android:name="com.clevertap.android.sdk.InAppNotificationActivity"  
            android:configChanges="orientation|keyboardHidden"  
            android:theme="@android:style/Theme.Translucent.NoTitleBar" />  
    ```

    No further action is required to integrate in-app notifications, which are registered for and requested by default by our CleverTap Segment integration.


### Sample App

CleverTap has created a sample Android application that integrates CleverTap via Segment. Check it out at the [Github repo](https://github.com/CleverTap/clevertap-segment-android-example).

### Non-Segment Functionality

CleverTap functionality that isn't integrated with Segment is supported via the use of our standard Android SDK API. For more information, visit our [documentation](https://support.clevertap.com/integration/android-sdk/), and [Github repo](https://github.com/CleverTap/clevertap-android-sdk).

Note that you should gate CleverTap functionality that is accessed directly via CleverTap API methods based on whether the Segment CleverTap integration is active and enabled. That way, when CleverTap is turned off via Segment, all CleverTap functionality is turned off.

For an example of gating CleverTap functionality based on whether CleverTap Segment is enabled, see our [example application class](https://github.com/CleverTap/clevertap-segment-android-example/blob/master/app/src/main/java/com/clevertap/segmenttest/CleverTapSegmentApplication.java), which stores the enabled state.



## iOS 

### Integrating

1. Add the Appboy Segment Pod to your Podfile:

    `pod 'Segment-CleverTap'`

    We recommend using the latest version on [CocoaPods](https://cocoapods.org/pods/Segment-CleverTap) since it will contain the most up to date features and bug fixes.

2. Next, declare CleverTap's integration in your app delegate instance:

    ```
    SEGAnalyticsConfiguration *config = [SEGAnalyticsConfiguration configurationWithWriteKey:@"YOUR_WRITE_KEY_HERE"];
    [config use:[SEGCleverTapIntegrationFactory instance]];
    [SEGAnalytics setupWithConfiguration:config];
    ```

### Integrating Push     

1. Follow the directions to register for push at: [https://segment.com/docs/libraries/ios/](https://segment.com/docs/libraries/ios/).

2. In your application's application:didReceiveRemoteNotification: method, add the following:

    `[[SEGAnalytics sharedAnalytics] receivedRemoteNotification:userInfo];`

3. If you integrated the application:didReceiveRemoteNotification:fetchCompletionHandler: in your app, add the following to that method:

    `[[SEGAnalytics sharedAnalytics] receivedRemoteNotification:userInfo];`

4. If you implemented handleActionWithIdentifier:forRemoteNotification:, add the following to that method:

    `[[SEGAnalytics sharedAnalytics] handleActionWithIdentifier:identifier forRemoteNotification:userInfo];`

### In-App Notifications

No further action is required to integrate in-app notifications, which are registered for and requested by default by our CleverTap Segment integration.

### Sample App

CleverTap has created a sample iOS application that integrates CleverTap via Segment. Check it out at the [Github repo](https://github.com/CleverTap/clevertap-segment-ios/tree/master/Example).

### Non-Segment Functionality

CleverTap functionality that isn't integrated with Segment is supported via the use of our standard iOS SDK API. For more information, visit our [documentation](https://support.clevertap.com/integration/ios-sdk/), and [Github repo](https://github.com/CleverTap/clevertap-ios-sdk).


## Settings

### CleverTapAccountID

**For Bundled Integration Only**: The Account ID  found in your CleverTap dashboard, used to identify your application.

### CleverTapAccountToken

**For Bundled Integration Only**: The Account Token  found in your CleverTap dashboard, used to identify your application.

