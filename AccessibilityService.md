# AccessibilityService

Monitor android system events like poping up a window or notifying a message or button being clicked and so on, then perform some actions.

1. new a service class to override two methods
```
public class RobService extends AccessibilityService {

    @Override
    public void onAccessibilityEvent(AccessibilityEvent event) {   }

    @Override
    public void onInterrupt() {  }
```

2. declear a AccessibilityService in manifest xml file
```
 <service
            android:name=".HelpService"
            <!-- declear BIND_ACCESSIBILITY_SERVICE so system can bind to the service to send event to it -->
            android:permission="android.permission.BIND_ACCESSIBILITY_SERVICE">
            <intent-filter>
                <action android:name="android.accessibilityservice.AccessibilityService" />
            </intent-filter>
            <meta-data
                android:name="android.accessibilityservice"
                android:resource="@xml/help" />
 </service>
```

3. service attribute setting like what kinds of event to monitor or which packages to monitor and so on.
There are two type of setting method, `Meta-data` and `setServiceInfo()`
    - Meta-data in manifest file like above and define a new help xml file
    ```
    <accessibility-service
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:description="@string/watcher_description"
    android:accessibilityFlags="flagDefault"
    android:canRetrieveWindowContent="true"
    />
    ```

    - setServiceInfo()
    ```
    @Override
    protected void onServiceConnected() {
        AccessibilityServiceInfo serviceInfo = new AccessibilityServiceInfo();
        // event type like windows opened or focus changed
        serviceInfo.eventTypes = AccessibilityEvent.TYPES_ALL_MASK;
        // feed back type of ring or vibration 
        serviceInfo.feedbackType = AccessibilityServiceInfo.FEEDBACK_GENERIC;
        // package names
        serviceInfo.packageNames = new String[]{"com.tencent.mm"}; 
        serviceInfo.notificationTimeout=100;
        setServiceInfo(serviceInfo);
    }
    ```

4. deal with the event
```
public void onAccessibilityEvent(AccessibilityEvent event) {
    if (null == event) {
        return;
    }
    if (AccessibilityEvent.TYPE_WINDOW_STATE_CHANGED == event.getEventType()) {
        String[] keywords = new String[] {"允许", "安装", "下一步"};
        simulationClick(keywords);
    }
}
private void simulationClick(String[] keywords) {
    List<AccessibilityNodeInfo> nodeInfoList = new ArrayList<>();
    for (String keyword: keywords) {
        nodeInfoList.addAll(getRootInActiveWindow().findAccessibilityNodeInfosByText(keyword));
    }
    for (AccessibilityNodeInfo node : nodeInfoList) {
        if (node.isClickable() && node.isEnabled()) {
            node.performAction(AccessibilityNodeInfo.ACTION_CLICK);
        }
    }
}
```



