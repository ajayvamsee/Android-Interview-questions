# Android-Interview-questions
Most Asked and Important Topics which will be covered and soon starting clear cut example and explanation



Android Interview Questions

BASE:

Why does an android app Lag?

Here, the critical point is that the time for which the GC runs, your app does not run for that time. So, it seems that the app is lagging. And hence, a bad experience for the user of the application. Let's understand it deeply.
The Android app updates its UI every 16ms (considering 60FPS -> 1000ms/60 = 16.67ms ~ 16ms) for smooth UI rendering.
Frame per second (FPS) is the measurement of the number of frames that appear within a second
So, if the GC runs for more time, the app will be unable to update UI and it will skip a few frames, so it will seem that the app is lagging. That is one of the reasons for the app lag.


Another reason is that the app is doing too much on the main thread. For example, at that time if any method/task is taking more time than 16m.s the app will be unable to update UI, which means lag will be there in the app for that time.


GC running frequently 
Doing too much work on the main thread.


What is Context? How is it used?

The Context in android is actually the context of what we are talking about and where we are currently present.

Few Points about the context.
It is the context of the current state of the application.
It can be used to get information about activities and applications.
It can be used to get access to resources, databases, shared preferences and etc.

Mainly Two Types of Context:

Application Context: It is the application and we are present in the application. For Example, MyApplication(which extends the Application class)
is an instance of MyApplication only.

It is an Instance that is a singleton and can be accessed in activity via getApplication().

This context is tied to the lifecycle of an application. The application context can be used where you need a context whose lifecycle is separate from the current context to when you pass a context beyond the scope of activity.

[Reason to not use activity context]
If you pass the activity context here, it will lead to the memory leak as it will keep the reference to the activity and the activity will not be garbage collected.

Activity Context: It is the activity and we are present in the Activity.
For Example, MainActivity
is an Instance of MainActivity only.


This context is available in the activity. This context is tied to the activity lifecycle.
This activity context should be used when you are passing the context in the scope of an activity or you need the context whose lifecycle is attached to the current activity or context.


Rules: So always remember, in the case of singleton(lifecycle is attached to the application lifecycle), always use the application context.

So Now when to use the activity context. Whenever you are in activity, for any UI operations like showing toast, dialogs, etc use the activity context.

Tell all the Android application components
App components are the essential building blocks of an android app. Each component is an entry point through which the system or a user can enter your app. Some components depend on others.

There are four types of app components:
Activities
Services
Broadcast Receivers
Content Providers.

What is an application class?

The Application class in Android is the base class within an Android app that contains all other components such as activities and services. The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.


What is the use of the Android manifest XML file?

Every app project must have an AndroidManifest.xml file (with precisely that name) at the root of the project source set. The manifest file describes essential information about your app to the Android build tools and the Android operating system.

Among many other things
The components of the app, including all activities, services, broadcast receivers, and content providers.
The permission that the app needs in order to access protected parts of the system or other apps. It also declares any permissions that other apps must have if they want to access the content of the app.
The hardware & software features the app requires affect which devices can install the app.
App components:
<activity> for each subclass of Activity.
<service> for each subclass of Service.
<receiver> for each subclass of BroadcastReceiver.
<provider> for each subclass of ContentProvider.


Activity and Fragment


What are Activity and its lifecycle?
Activity is like a frame or window in java that represents GUI. It represents one screen of android.
onCreate
called when activity is first created.
onStart
called when activity is becoming visible to the user.
onResume
called when activity will start interacting with the user.
onPause
called when activity is not visible to the user.
onStop
called when activity is no longer visible to the user.
onRestart
called after your activity is stopped, prior to start.
onDestroy
called before the activity is destroyed.




what is the difference between oncreate() and onstart() 

onCreate():  called when the activity is first created. This is where you should do all of your normal static setup: create views, bind data to lists, etc. This method also provides you with a Bundle containing the activity's previously frozen state, if there was one.

 Always followed by onStart().  Called when the activity is becoming visible to the user. Followed by onResume() if the activity comes to the foreground, or onStop() if it becomes hidden.



What is Fragment and its lifecycle.?

The fragment is the part of the Activity which represents a portion of the User Interface(UI) on the screen. It is the modular section of the android activity that is very helpful in creating UI designs that are flexible in nature and auto-adjustable based on the device screen size. The UI flexibility on all devices improves the user experience and adaptability of the application. Fragments can exist only inside an activity.




1
onAttach(Activity)
it is called only once when it is attached with activity.
2)
onCreate(Bundle)
It is used to initialize the fragment.
3)
onCreateView(LayoutInflater, ViewGroup, Bundle)
creates and returns view hierarchy.
4)
onActivityCreated(Bundle)
It is invoked after the completion of onCreate() method.
5)
onViewStateRestored(Bundle)
It provides information to the fragment that all the saved state of fragment view hierarchy has been restored.
6)
onStart()
makes the fragment visible.
7)
onResume()
makes the fragment interactive.
8)
onPause()
is called when fragment is no longer interactive.
9)
onStop()
is called when fragment is no longer visible.
10)
onDestroyView()
allows the fragment to clean up resources.
11)
onDestroy()
allows the fragment to do final clean up of the fragment state.
12)
onDetach()
It is called immediately prior to the fragment no longer being associated with its activity.





when should you use a Fragment rather than an Activity

when you have some UI components to be used across various activities
when multiple views can be displayed side by side just like view page.

Why is it recommended to use only the default constructor

Android Framework decides to recreate our fragment 
Orientation changes
Android calls the no-argument constructor of our Fragment
It has no idea what constructor we have created

 
What is Service in Android
Android service is a component that is used to perform operations in the background such as playing music, handling network transactions, interacting with content providers, etc. It doesn't have any UI (user interface).
The service runs in the background indefinitely even if the application is destroyed.
Moreover, service can be bounded by a component to perform interactivity and inter-process communication (IPC).
Types of Services:
Foreground Services: Services that notify the user about its ongoing operations are termed Foreground Services. Users can interact with the service by the notifications provided about the ongoing task. Such as in downloading a file, the user can keep track of the progress in downloading and can also pause and resume the process.
Background services: Background services do not require any user intervention. These services do not notify the user about ongoing background tasks and users also cannot access them. Processes like schedule syncing of data or storing of data fall under this service.
Bound Services: This type of android service allows the components of the application like activity to bound themselves with it. Bound services perform their task as long as any application component is bound to it. More than one component is allowed to bind themselves with a service at a time. In order to bind an application component with a service bindService() method is used. 


Life Cycle of Android Service;
1. Started Service(Unbounded Services): A service is started when a component (like activity) calls startService() methods, now it runs in the background indefinitely. It is stopped by the stopService() method. This service can stop itself by calling the stopSelf() method.

2. Bound Service: It can be treated as a server in a client-server interface. By following this path, android application components can send requests to the service and can fetch results. A service is termed as bounded when an application component binds itself with a service by calling bindService() method. To stop the execution of this service, all the components must unbind themselves from the service by using unbindService() method.

What is a broadcast Receiver?
A broadcast receiver is an application component that allows you to register for system or application events. All registered receivers for an event are notified by the android runtime once this event happens.

For Example, the Application can register for the ACTION_BOOT_COMPLETED system event which is fired once the android system has completed the boot process.

Implementation:
A receiver can be registered via the AndroidManifest.xml file

Alternatively to this static registration, you can also register a receiver dynamically via the Context.registerReciever().

Life Cycle of a broadcast receiver
After the onRecieve() of the receiver class has finished, the android system is allowed to recycle the receiver.


What is a Content Provider?
A content provider component supplies data from one application to others on requests. Such requests are handled by the methods of the content resolver class. A content provider can use different ways to store its data and the data can be stored in a database, in files, or even over a network.
Sometimes it is required to share data across applications. This is where content providers become very powerful.
What is Android Launch Mode?

Launch mode is an android OS command that determines how the activity should be started. 
It Specifies how every new action should be linked to the existing task.
Types 

Standard:
This is the default launch mode of activity (if not specified). It launches a new instance of an activity in the task from which it was launched. No Instances of an activity can be generated and multiple instances of the activity can be assigned to the same or separate task.

In other words, you can create the same activity multiple times in the same task as well as in different tasks.

Syntax:
<activity android:launchMode=”standard” />

Single Top:  If an instance of the activity already exists at the top of the current task in this launch mode, no new instance will be created and the android system will send the intent data through onNewIntent(). If an instance does not exist on the top of the task, a new instance will be created. You can use this launch mode to generate numerous instances of the same activity within the same task or across tasks, but only if the identical instance does not already exist at the top of the stack.
	
	Syntax:
<activity android:launchMode=”singleTop” />

Single Task: In this method of operation, a new task is always generated and a new instance is added to the task as the root one. If the activity already exists on another task no new instance is created, and the android system transmits the intent information via the onNewIntent() function. At any one time, there will be just one instance of the activity.

Syntax:
<activity android:launchMode=”singleTask” />

Single Instance: This is a highly unique start option that is only used in programs with a single activity. It works similarly to Single Task, except that no additional activities are generated in the same task. Any further activity initiated from this point will result in the creation of a new task.

Syntax:
<activity android:launchMode=”singleInstance” />
What is the difference between replace() and add() in Android fragments?
replace() removes the existing fragment and adds a new fragment..
add() retains the currently displayed fragment and adds a new fragment onto the fragment stack. This means the existing fragment will still be active and will be in the ‘paused’ state as such when a back button is pressed onCreateView() will not be called for the existing fragment(the fragment which was there before the new fragment was added).
Views (UI)
What are ViewGroups and how they are different from the Views?
View: View objects are the basic building blocks of User Interface(UI) elements in Android. The view is a simple rectangle box which responds to the user’s actions. Examples are EditText, Button, CheckBox, etc. View refers to the android. view.View class, which is the base class of all UI classes.
ViewGroup: ViewGroup is the invisible container. It holds View and ViewGroup. For example, LinearLayout is the ViewGroup that contains Button(View), and other Layouts also. ViewGroup is the base class for Layouts.
LinearLayout means you can align views one by one (vertically/ horizontally).
RelativeLayout means based on the relation of views from its parents and other views.
ConstraintLayout: Allows you to create large and complex layouts with a flat view hierarchy (no nested view groups). It’s similar to RelativeLayout in that all views are layered out according to relationships between sibling views and the parent layout, but it’s more flexible than RelativeLayout and easier to use with Android Studio’s Layout Editor. The ConstraintLayout is also compatible right down to API level 9.


Constraints A constraint defines a relationship between two widgets in the layout and controls how those widgets will be positioned within the layout.


The aim of the ConstraintLayout is to help reduce the number of nested views, which will improve the performance of our layout files.


WebView to load HTML, static or dynamic pages.
FrameLayout to load child one above another, like cards inside a frame, we can place one above another or anywhere inside the frame.
What are chains?
Chains are a specific kind of constraint which allows us to share space between the views within the chain and control how the available space is divided between them. The closest analog with traditional Android layouts is weighted in Linear Layout but chains do far more than that, as we shall see.
There are three possible modes: spread, spread_inside, and packed.
Guidelines
A guideline is a visual guide which will not be seen at runtime that is used align other views.Guidelines can be oriented either horizontally or vertically.
What is the difference between ListView and RecyclerView
List View:
An adapter actually bridges between UI components and the data source that fills data into UI Component. The adapter holds the data and sends the data to the adapter view, the view can take the data from the adapter view and shows the data on different views like a spinner, list view, grid view, etc.
RecyclerView:
RecyclerView was created as a ListView improvement, so yes, you can create an attached list with ListView control, but using RecyclerView is easier as it:
Reuses cells while scrolling up/down - this is possible with implementing View Holder in the ListView adapter, but it was an optional thing, while in the RecycleView it's the default way of writing adapter.
Decouples list from its container - so you can put list items easily at run time in the different containers (linear layout, grid-layout) with setting LayoutManager.
Advantages of RecyclerView over listview:
Contains ViewHolder by default.
Easy animations.
Supports horizontal, grid, and staggered layouts
Advantages of listView over recyclerView:
Easy to add divider.
Can use inbuilt arrayAdapter for simple plain lists
Supports Header and footer.
Supports OnItemClickListner.( In RecyclerView we need to create our custom on-click listener)




DIALOGS & TOASTS
What is dialog 
A dialog is a small window that prompts the user to make a decision or enter additional information. A dialog does not fill the screen and is normally used for modal events that require users to take an action before they can proceed.


Alert Dialog that shows s can show a title, up to three buttons, a list of selectable items, or a custom layout.
DatePickerDailog or TimePickerDailog with a predefined UI that allows the user to select  data or time.


What is Toast
A toast provides simple feedback about an operation in a small popup. It only fills the amount of space required for the message and the current activity remains visible and interactive. Toasts automatically disappear after a timeout.
What is the difference between Dialog and Dialog Fragment?
Dialog: A dialog is a small window that prompts the user to make a decision or enter additional information.
 DialogFragment: A DialogFragment is a special fragment subclass that is designed for creating and hosting dialogs
Data Storage
What are different ways to store data in your Android app
Shared preferences
Internal Storage
External Storage
Room
Saving Cache Files
How do save state during orientation change in Android if the state is made of my classes?


 On newer versions of Android and with the compatibility library, retained fragments are usually the best way to handle keeping expensive-to-recreate data alive across activity destruction/creation. And as Dianne pointed out, retaining non configuration data was for optimizing things like thumbnail generation that are nice to save for performance reasons but not critical to your activity functioning if they need to be redone - it's not a substitute for properly saving and restoring activity state.
But back when I first answered this in 2010:
If you want to retain your own (non-view-state) data, you can actually pass an arbitrary object specifically for orientation changes using onRetainNonConfigurationInstance(). See this Android Developers blog post. Just be careful not to put any Views or other references to the pre-rotation Context/Activity in the object you pass, or you'll prevent those objects from being garbage collected and may eventually run out of memory (this is called a context leak).



What is commit() and apply() in SharedPreferences
Commit() returns a boolean value of success or failure immediately by writing data synchronously.
Apply() is asynchronous and it won't return any boolean response. If you have an apply() outstanding and you are performing commit(), then the commit() will be blocked until the apply() is not completed.




















What is the difference between LiveData and MutableLiveData?
LiveData is immutable(will not change) while MutableLiveData is mutable(reliable to change). MutableLiveData extends LiveData and provides methods like setValue() and postValue().
 What is ADB?
ADB stands for Android Debug Bridge. It is a command line tool that is used to communicate with the emulator instance.
What is a singleton class in Android?
A singleton class is a class that can create only an object that can be shared by all other classes.
Difference between setValue() and postValue()
While using the Main thread to change the data, you should use the setValue() method of the MutableLiveData class and while using the background thread to change the LiveData, you should use the postValue() method of the MutableLiveData class.


 What is the difference Between Parcelable and Serializable?
Parcelable is going to convert objects to byte streams and pass the data between two activities. Parcelable is faster than serializable.
Serializable does the same thing but it is a slow process compared to parcelable.


49) Name some exceptions in Android?
Inflate Exception
Surface.OutOfResourceException
SurfaceHolder.BadSurfaceTypeException
WindowManager.BadTokenException





