# Lesson 9 - Building a Content Provider
https://github.com/udacity/ud851-Exercises
## Steps to create a Provider

[Content Provider Documentation](https://developer.android.com/guide/topics/providers/content-providers.html)

1. Create a class that extends from the content provider and implements the onCreate() function.
2. Register the content provider in the Manifest.
3. Define URI's that identify the TaskContentProvider and the different data types that it can return.
4. Add these URI's to the Contract class.
5. Build a URIMatcher to match URI patterns to integers.
6. Implement the required CRUD methods.

## Create TaskContentProvider

```java
public class TaskContentProvider extends ContentProvider {

    // Member variable for a TaskDbHelper that's initialized in the onCreate() method
    private TaskDbHelper mTaskDbHelper;

    /* onCreate() is where you should initialize anything you’ll need to setup
    your underlying data source.
    In this case, you’re working with a SQLite database, so you’ll need to
    initialize a DbHelper to gain access to it.
     */
    @Override
    public boolean onCreate() {
        Context context = getContext();
        mTaskDbHelper = new TaskDbHelper(context);
        return true;
    }


    @Override
    public Uri insert(@NonNull Uri uri, ContentValues values) {

        throw new UnsupportedOperationException("Not yet implemented");
    }


    @Override
    public Cursor query(@NonNull Uri uri, String[] projection, String selection,
                        String[] selectionArgs, String sortOrder) {

        throw new UnsupportedOperationException("Not yet implemented");
    }


    @Override
    public int delete(@NonNull Uri uri, String selection, String[] selectionArgs) {

        throw new UnsupportedOperationException("Not yet implemented");
    }


    @Override
    public int update(@NonNull Uri uri, ContentValues values, String selection,
                      String[] selectionArgs) {

        throw new UnsupportedOperationException("Not yet implemented");
    }


    @Override
    public String getType(@NonNull Uri uri) {

        throw new UnsupportedOperationException("Not yet implemented");
    }

}
```

## Create and Register a ContentProvider

In the **Manifest** :

```xml
<!-- Exported = false limits access to this ContentProvider to only this app -->
<provider 
    android:name="com.example.android.todolist.data.TaskContentProvider"
    android:authorites="com.example.android.todolist"
    android:exported="false" />
```

## Define the URI Structure

```<scheme>//<authority>/<path>```

content://com.android.example.todolist/tasks

Example : **CalendarContentProvider** => content://com.android.calendar/```<path to calendars>```

- content://com.android.calendar/events

- content://com.android.calendar/attendees

Example : access the second task in the table Tasks

- content://com.udacity.example.todolist/tasks/2

Access a task - # stands for any integer number
- content://com.udacity.example.todolist/tasks/#

![](lesson_9_8_wild_cards.png "uri wild cards")

## Change the Contract

- Scheme= content:// 
- Content authority = reference to the provider (com.example.android.todolist)
- Base content URI = content_scheme + authority => a unique reference to the provider
- Path = to specific data
- Content URI = base content URI + path

```java
public class TaskContract {

    // The authority, which is how your code knows which Content Provider to access
    public static final String AUTHORITY = "com.example.android.todolist";

    // The base content URI = "content://" + <authority>
    public static final Uri BASE_CONTENT_URI = Uri.parse("content://" + AUTHORITY);

    // Define the possible paths for accessing data in this contract
    // This is the path for the "tasks" directory
    public static final String PATH_TASKS = "tasks";

    /* TaskEntry is an inner class that defines the contents of the task table */
    public static final class TaskEntry implements BaseColumns {

        // TaskEntry content URI = base content URI + path
        public static final Uri CONTENT_URI =
                BASE_CONTENT_URI.buildUpon().appendPath(PATH_TASKS).build();

        // Task table and column names
        public static final String TABLE_NAME = "tasks";

        // Since TaskEntry implements the interface "BaseColumns", it has an automatically produced
        // "_ID" column in addition to the two below
        public static final String COLUMN_DESCRIPTION = "description";
        public static final String COLUMN_PRIORITY = "priority";
    }
}
```

## Build the URIMatcher

**UriMatcher** : Determines what king of URI the provider receives and match it to an integer constant. 

We can easily make a switch statement instead of using a series of long if statements that check for equality.

- Create the integer constants that these URIs will match to
```java
// Define final integer constants for the directory of tasks and a single item.
// It's convention to use 100, 200, 300, etc for directories,
// and related ints (101, 102, ..) for items in that directory.
public static final int TASKS = 100;
public static final int TASK_WITH_ID = 101;
```
- Write a helper function called UriMatcher
```java
// Define a static buildUriMatcher method that associates URI's with their int match
/**
Initialize a new matcher object without any matches,
then use .addURI(String authority, String path, int match) to add matches
*/
public static UriMatcher buildUriMatcher() {

    // Initialize a UriMatcher with no matches by passing in NO_MATCH to the constructor
    UriMatcher uriMatcher = new UriMatcher(UriMatcher.NO_MATCH);

    /*
    All paths added to the UriMatcher have a corresponding int.
    For each kind of uri you may want to access, add the corresponding match with addURI.
    The two calls below add matches for the task directory and a single item by ID.
    */
    // addURI(String authority, String path, int code)
    // directory
    uriMatcher.addURI(TaskContract.AUTHORITY, TaskContract.PATH_TASKS, TASKS);
    // single item
    uriMatcher.addURI(TaskContract.AUTHORITY, TaskContract.PATH_TASKS + "/#", TASK_WITH_ID);

    return uriMatcher;
}
```
- Declare a static variable for the Uri matcher that you construct
```java
// begin with s like static
private static final UriMatcher sUriMatcher = buildUriMatcher();
```
- then we can create the switch statements like this
```java
int match = sUriMatcher.match(uri);

switch(match) {
    // handle different integer matches
    case TASKS:
        retCursor = db.query(TABLE_NAME,
                        projection,
                        selection,
                        selectionArgs,
                        null,
                        null,
                        sortOrder);
        break;
    case TASK_WITH_ID:
    // handle single task case
        break;
    // default exception
    default:
        throw new UnsupportedOperationException("Unknow uri: " + uri);
}
```

## Resolver to Database Flow









