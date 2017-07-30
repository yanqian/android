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

### Bind Services

Bind the clint to the Service:

Service  --(IBinder)-->  Client(MainActivity)


#### MyService.java  Service class

```
private final IBinder myBinder = new MyLocalBinder(); // ②

public IBinder onBind(Intent intent){
	return myBinder;  // ①
}
// return a reference to MyService
public MyLocalBinder extends Binder{
	MyService getService(){
		return MyService.this;  // ③
	}
}

// do something in the service

public String getTime(){ return "12:00"}
```
#### MainActivity.java Client class

1. set MyService
```
import package.MyService.MyLocalBinder

MyService myService;
boolean isBind = false;
```
2. new a ServiceConnection

```
private ServiceConnection myConnection = new ServiceConnection(){
	// the parameter IBinder will be got by android system from Service class
	// and it is the bridge between Service and Client
	public void onServiceConnected(ComponentName name, IBinder service){
		MyLocalBinder binder = (MyLocalBinder) service;
		// So we got the service instance now
		myService = binder.getService();
		isBind = true;
	}
	public void onServiceDisconnected(){
		isBind = false;
	}
};
```
3. Bind the acitivity to service in onCreate method

```
Intent i = new Intent(this, MyService.class);
bindService(i, myConnection, CONTEXT.BINDER_AUTO_CREATED)
```
4. invoke the actual action of service as a button listener

```
public void showTime(View view){
	findViewById(id).setText(myService.getTime());
}
```

> https://developer.android.com/guide/components/services.html


