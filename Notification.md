# Notification

## How to send notification in Android system

1. new a Notification model
```
int uniqueId = 12345;
NotificationCompat.Builder notification = new NotificationCompat.Builder(this);
// when the notification is clicked, it will atuo disappear. 
notification.setAutoCancel(true);
```

2. set attritute of notification
```
notification.setSmallIcon(R.drawable.xx);
notification.setTicker("");
notification.setWhen(time);
notification.setContentTitle("Title");
notification.setContentText("text");
```

3. set the activity to launch when the notification is clicked
```
Intent intent = new Intent(this, MainActivity.class);
PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);
notification.setContentIntent(pendingIntent);
```

4. notify the message
```
NotificationManager nm = getSystemService(NOTIFICATION_SERVICE);
nm.notify(uniqueId, notification.build());
```