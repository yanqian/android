# Activity LifeCycle
There are six callback methods in Activity class.

- `onCreate()`
- `on Start()`
- `onResume()`
- `onPause()`
- `onStop()`
- `onDestroy()`

## Activity lifecycle concept

![Activity lifecycle](activity_lifecycle.png)

### onCreate

This is the first callback and called when the activity is first created.

You must implement this callback, which fires when the system first creates the activity. On activity creation, the activity enters the Created state. In the onCreate() method, you perform basic application startup logic that should happen only once for the entire life of the activity.

This method receives the parameter savedInstanceState, which is a Bundle object containing the activity's previously saved state. If the activity has never existed before, the value of the Bundle object is null.


### onStart

This callback is called when the activity becomes visible to the user.

 The onStart() call makes the activity visible to the user, as the app prepares for the activity to enter the foreground and become interactive.

 The onStart() method completes very quickly and, as with the Created state, the activity does not stay resident in the Started state. Once this callback finishes, the activity enters the Resumed state, and the system invokes the onResume() method.

### onResume

This is called when the user starts interacting with the application.

When the activity enters the Resumed state, it comes to the foreground, and then the system invokes the onResume() callback. This is the state in which the app interacts with the user. The app stays in this state until something happens to take focus away from the app. Such an event might be, for instance, receiving a phone call, the user’s navigating to another activity, or the device screen’s turning off.

### onPause

The paused activity does not receive user input and cannot execute any code and called when the current activity is being paused and the previous activity is being resumed.

The system calls this method as the first indication that the user is leaving your activity (though it does not always mean the activity is being destroyed). Use the onPause() method to pause operations such animations and music playback that should not continue while the Activity is in the Paused state, and that you expect to resume shortly.

onPause() execution is very brief, and does not necessarily afford enough time to perform save operations. For this reason, you should not use onPause() to save application or user data, make network calls, or execute database transactions; such work may not complete before the method completes. Instead, you should perform heavy-load shutdown operations during onStop().

### onStop

This callback is called when the activity is no longer visible.

This may occur, for example, when a newly launched activity covers the entire screen. The system may also call onStop() when the activity has finished running, and is about to be terminated.

if you can't find a more opportune time to save information to a database, you might do so during onStop().

### onDestroy

This callback is called before the activity is destroyed by the system.

This is the final call that the activity receives. The system either invokes this callback because the activity is finishing due to someone's calling finish(), or because the system is temporarily destroying the process containing the activity to save space.

The onDestroy() callback releases all resources that have not yet been released by earlier callbacks such as onStop().

### onRestart

This callback is called when the activity restarts after stopping it.




