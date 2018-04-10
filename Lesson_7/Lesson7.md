## Lesson 7  - Storing Data in SQlite

## Creating the Contract

Design what the database will look like.
Define the tables and the columns for each table.

The **contract** is a class, then we need to create an **inner class for each table**. 

The **constructor** needs to be private : you should never neef to create an instance of the contract class because the contract is simply a class filled with DB related constants thar are all static.

The inner class can (not mandatory) implements the interface **BaseColumns**.
The BaseColumns interface **automatically includes** a constant representing the primary key field called **_ID**.

In WaitlistContract class :
```java
public static final class WaitlistEntry implements BaseColumns {
    public static final String TABLE_NAME = "waitlist";
    public static final String COLUMN_GUEST_NAME = "guestName";
    public static final String COLUMN_PARTY_SIZE = "partySize";
    public static final String COLUMN_TIMESTAMP = "timestamp";
}
```

## Creating the database

![](lesson_7_8_db_helper.png "DB Helper")

Create a class DB Helper.

```java
public class WaitlistDbHelper extends SQLiteOpenHelper {
    // The database name
    private static final String DATABASE_NAME = "waitlist.db";

    // If you change the database schema, you must increment the database version
    private static final int DATABASE_VERSION = 1;

    public WaitlistDbHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }

    @Override
    public void onCreate(SQLiteDatabase sqLiteDatabase) {

        // Create a table to hold waitlist data
        final String SQL_CREATE_WAITLIST_TABLE = "CREATE TABLE " + WaitlistEntry.TABLE_NAME + " (" +
                WaitlistEntry._ID + " INTEGER PRIMARY KEY AUTOINCREMENT," +
                WaitlistEntry.COLUMN_GUEST_NAME + " TEXT NOT NULL, " +
                WaitlistEntry.COLUMN_PARTY_SIZE + " INTEGER NOT NULL, " +
                WaitlistEntry.COLUMN_TIMESTAMP + " TIMESTAMP DEFAULT CURRENT_TIMESTAMP" +
                "); ";

        // Execute the query by calling execSQL on sqLiteDatabase and pass the string query SQL_CREATE_WAITLIST_TABLE
        sqLiteDatabase.execSQL(SQL_CREATE_WAITLIST_TABLE);
    }

    @Override
    public void onUpgrade(SQLiteDatabase sqLiteDatabase, int i, int i1) {
        // For now simply drop the table and create a new one. This means if you change the
        // DATABASE_VERSION the table will be dropped.
        // In a production app, this method might be modified to ALTER the table
        // instead of dropping it, so that existing data is not deleted.
        sqLiteDatabase.execSQL("DROP TABLE IF EXISTS " + WaitlistEntry.TABLE_NAME);
        onCreate(sqLiteDatabase);
    }
}
```

## Querying all guests

**getWritableDatabase** => create/write in the DB

**getReadableDatabase** => read in the DB

Write fake data, in MainActivity : 
```java
 private GuestListAdapter mAdapter;

 @Override
    protected void onCreate(Bundle savedInstanceState) {
        ...
        // Create a DB helper (this will create the DB if run for the first time)
        WaitlistDbHelper dbHelper = new WaitlistDbHelper(this);

        // Keep a reference to the mDb until paused or killed. Get a writable database
        // because you will be adding restaurant customers
        mDb = dbHelper.getWritableDatabase();

        // call insertFakeData in TestUtil and pass the database reference mDb
        //Fill the database with fake data
        TestUtil.insertFakeData(mDb);

        // Run the getAllGuests function and store the result in a Cursor variable
        Cursor cursor = getAllGuests();

        // Create an adapter for that cursor to display the data
        mAdapter = new GuestListAdapter(this, cursor.getCount());

        // Link the adapter to the RecyclerView
        waitlistRecyclerView.setAdapter(mAdapter);

}

private Cursor getAllGuests() {
        // COMPLETED (6) Inside, call query on mDb passing in the table name and projection String [] order by COLUMN_TIMESTAMP
        return mDb.query(
                WaitlistContract.WaitlistEntry.TABLE_NAME,
                null,
                null,
                null,
                null,
                null,
                WaitlistContract.WaitlistEntry.COLUMN_TIMESTAMP
        );
}
```

In GuestListAdpater : 
```java
// Add a new local variable mCount to store the count of items to be displayed in the recycler view
private int mCount;

public GuestListAdapter(Context context, int count) {
        this.mContext = context;
        // Set the local mCount to be equal to count
        mCount = count;
}

@Override
    public int getItemCount() {
        return mCount;
}
```

## Updating the Adapter

In GuestListAdapter :

```java
 // Replace the mCount with a new Cursor field called mCursor
// Holds on to the cursor to display the waitlist
private Cursor mCursor;

public GuestListAdapter(Context context, Cursor cursor) {
        this.mContext = context;
        // COMPLETED (3) Set the local mCursor to be equal to cursor
        this.mCursor = cursor;
}

@Override
    public void onBindViewHolder(GuestViewHolder holder, int position) {
    //  Move the cursor to the passed in position, return if moveToPosition returns false
    // Move the mCursor to the position of the item to be displayed
    if (!mCursor.moveToPosition(position))
        return; // bail if returned null
    // Call getString on the cursor to get the guest's name
    String name = mCursor.getString(mCursor.getColumnIndex(WaitlistContract.WaitlistEntry.COLUMN_GUEST_NAME));
    // Call getInt on the cursor to get the party size
    int partySize = mCursor.getInt(mCursor.getColumnIndex(WaitlistContract.WaitlistEntry.COLUMN_PARTY_SIZE));
    // Set the holder's nameTextView text to the guest's name
    // Display the guest name
    holder.nameTextView.setText(name);
    // Set the holder's partySizeTextView text to the party size
    // Display the party count
    holder.partySizeTextView.setText(String.valueOf(partySize));
}

@Override
    public int getItemCount() {
        // Update the getItemCount to return the getCount of the cursor
        return mCursor.getCount();
}

```
In MainActivity :

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    ...
    Cursor cursor = getAllGuests();

    // Pass the entire cursor to the adapter rather than just the count
            // Create an adapter for that cursor to display the data
    mAdapter = new GuestListAdapter(this, cursor);

     waitlistRecyclerView.setAdapter(mAdapter);
```

## Adding Guests

Read guest's name from the UI, in MainActivity :
```java
// Create local EditText fields for mNewGuestNameEditText and mNewPartySizeEditText
private EditText mNewGuestNameEditText;
private EditText mNewPartySizeEditText;

@Override
protected void onCreate(Bundle savedInstanceState) {
    ... 

    // Set the Edit texts to the corresponding views using findViewById
    mNewGuestNameEditText = (EditText) this.findViewById(R.id.person_name_edit_text);
    mNewPartySizeEditText = (EditText) this.findViewById(R.id.party_count_edit_text);
    ...
}

public void addToWaitlist(View view) {
    // check if any of the EditTexts are empty, return if so
    if (mNewGuestNameEditText.getText().length() == 0 || 
    mNewPartySizeEditText.getText().length() == 0) {
        return;
    }
    // Create an integer to store the party size and initialize to 1
    int partySize = 1;
    // Use Integer.parseInt to parse mNewPartySizeEditText.getText to an integer
    try {
        //mNewPartyCountEditText inputType="number", so this should always work
        partySize = Integer.parseInt(mNewPartySizeEditText.getText().toString());
    } catch (NumberFormatException ex) {
        // Make sure you surround the Integer.parseInt with a try catch and log any exception
        Log.e(LOG_TAG, "Failed to parse party size text to number: " + ex.getMessage());
    }

    // call addNewGuest with the guest name and party size
    // Add guest info to mDb
    addNewGuest(mNewGuestNameEditText.getText().toString(), partySize);

    // call mAdapter.swapCursor to update the cursor by passing in getAllGuests()
    // Update the cursor in the adapter to trigger UI to display the new list
    mAdapter.swapCursor(getAllGuests());

    // To make the UI look nice, call .getText().clear() on both EditTexts, also call clearFocus() on mNewPartySizeEditText
    //clear UI text fields
    mNewPartySizeEditText.clearFocus();
    mNewGuestNameEditText.getText().clear();
    mNewPartySizeEditText.getText().clear();
}

private long addNewGuest(String name, int partySize) {
    // Inside, create a ContentValues instance to pass the values onto the insert query
    ContentValues cv = new ContentValues();
    // call put to insert the name value with the key COLUMN_GUEST_NAME
    cv.put(WaitlistContract.WaitlistEntry.COLUMN_GUEST_NAME, name);
    // call put to insert the party size value with the key COLUMN_PARTY_SIZE
    cv.put(WaitlistContract.WaitlistEntry.COLUMN_PARTY_SIZE, partySize);
    // call insert to run an insert query on TABLE_NAME with the ContentValues created
    return mDb.insert(WaitlistContract.WaitlistEntry.TABLE_NAME, null, cv);
}
```

## Swap cursor

In GuestListAdapter :
```java
public void swapCursor(Cursor newCursor) {
    // Inside, check if the current cursor is not null, and close it if so
    // Always close the previous mCursor first
    if (mCursor != null) mCursor.close();
    // Update the local mCursor to be equal to  newCursor
    mCursor = newCursor;
    // Check if the newCursor is not null, and call this.notifyDataSetChanged() if so
    if (newCursor != null) {
        // Force the RecyclerView to refresh
        this.notifyDataSetChanged();
    }
}
```
## Removing guests

In MainActivity : 

```java
private boolean removeGuest(long id) {
    // Inside, call mDb.delete to pass in the TABLE_NAME and the condition that WaitlistEntry._ID equals id
    return mDb.delete(WaitlistContract.WaitlistEntry.TABLE_NAME, WaitlistContract.WaitlistEntry._ID + "=" + id, null) > 0;
}
```

In GuestListAdapter, we need to add the guest's id in the UI :
```java
@Override
public void onBindViewHolder(GuestViewHolder holder, int position) {
    ...
    // Retrieve the id from the cursor and
    long id = mCursor.getLong(mCursor.getColumnIndex(WaitlistContract.WaitlistEntry._ID));
    // Set the tag of the itemview in the holder to the id
    holder.itemView.setTag(id);
}
```

Then in MainActivity, **onCreate** method, create a new  **ItemTouchHelper** :
```java
...
// Create a new ItemTouchHelper with a SimpleCallback that handles both LEFT and RIGHT swipe directions
new ItemTouchHelper(new ItemTouchHelper.SimpleCallback(0, ItemTouchHelper.LEFT | ItemTouchHelper.RIGHT) {

    // Override onMove and simply return false inside
    @Override
    public boolean onMove(RecyclerView recyclerView, RecyclerView.ViewHolder viewHolder, RecyclerView.ViewHolder target) {
        //do nothing, we only care about swiping
        return false;
    }

    // Override onSwiped
    @Override
    public void onSwiped(RecyclerView.ViewHolder viewHolder, int swipeDir) {
        // Inside, get the viewHolder's itemView's tag and store in a long variable id
        //get the id of the item being swiped
        long id = (long) viewHolder.itemView.getTag();
        // call removeGuest and pass through that id
        //remove from DB
        removeGuest(id);
        // call swapCursor on mAdapter passing in getAllGuests() as the argument
        //update the list
        mAdapter.swapCursor(getAllGuests());
    }

    // attach the ItemTouchHelper to the waitlistRecyclerView
}).attachToRecyclerView(waitlistRecyclerView);
```

