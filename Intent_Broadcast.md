# Intent and Boradcast

## Intent
When one activity starts another activity, the Intent is the media to convey messages.

Activity A --(start)--> Activity B:
in Activity A  `Intent i = new Intent(); i.putExtra(); startActivity(i)`
in Activity B  `getIntent()`

## Broadcast 

### What is Boradcast
Message sent from sender to receiver.
And Boradcast transports between apps.

### Sender

In Activity of one app as a sender:

```
Intent i = new Intent();
i.setAction(package_name);
// this broadcast will wake up the stopped apps
i.setFlags(Intent.FLAG_INCLUDE_STOPPED_PACKAGES);
sentBroadcast(i)

```

### Receiver

- New a no activity project, and new a BroadcastReceiver class

- in MainActivity xml file, add intent filter

```
<receiver>
 <intent-filter> 
 	<action android.name="package_name"/>
 </intent-filter> 
</receiver>
```

- implement onReceiver(Context context, Intent intent) method

- run as "do not launch activity"

> https://developer.android.com/guide/components/broadcasts.html

