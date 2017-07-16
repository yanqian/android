# Service 

Designed for time consuming backgroud job like downloading or database querying or notification watcher or something.

There are 2 types of service.

- IntentService
- Service

## IntentService

- Override `onHandleIntent(Intent intent)` in MyIntentService java class to handle the intent passed to it from the main activity.
- Register service in main_activity xml file
```
<service android:name=".MyIntentService" />
```
- Start service in onCreate method of mainAcitivy java class 
```
Intent i = new Intent(this, MyIntentService.class)
startService(i)
```
- Run app

Note:
The IntentService implement the thread(runnable.run) method. So it's multiple threaded and you do not have to implement the thread manually and it's working pretty cool.



## Service

- Overrid `onBind(Intent intent)` and `onStartCommand(Intent intent, int flag, int startId)`
- onStartCommand implements thread(runnable.run) method.
- Register service in main_activity xml file
- Start service in onCreate method of mainAcitivy java class 
- Run app

Note:
The Service does not implement the thread(runnable.run) method. So you have to implement the thread manually to make it work fine.

