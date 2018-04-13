# Lesson 8 - Content Provider

## Content Provider

A content provider is a class that sits between an application and its data source. Its job is to provide easily managed access to the underlying data source.

![](lesson_8_2_content_provider.png "Content Provider")

## Content Provider Advantages 

- Allow developers to change the underlying data source without needing to change any code in the applications that access the content provider.

![](lesson_8_3_layer_abstraction.png "Layer")

- 
![](lesson_8_3_access_data.png "Access data")

- 
![](lesson_8_3_example_content_provider.png "pass data to content provider")

![](lesson_8_3_example_app.png "pass data to another app")

## DroidTermExample

![](lesson_8_5_droid_term.png "droidTermExample")


General Steps for Using a ContentProvider

You will take the following steps:

1. Get permission to use the ContentProvider.
2. Get the ContentResolver
3. Pick one of four basic actions on the data: query, insert, update, delete
4. Identify the data you are reading or manipulating to create a URI
5. In the case of reading from the ContentProvider, display the information in the UI

## Content Provider Permissions

In AndroidManifest.xml : 
```xml
<uses-permission android:name="com.example.udacity.droidtermexample.TERMS_READ" />
```

## Content Resolver

![](lesson_8_8_content_provider.png "Content Resolver")

## Steps for using a Content Provider

```java
ContentResolver resolver = getContentResolver();
Cursor cursor = Resolver.query(DroidTermsExampleContract.
CONTENT_URI, null, null, null, null);
```

### Four basic actions
- read from the data: **query()**
- add a row or rows to the data: **insert()**
- update the data: **update()**
- delete a row or rows from the data: **delete()**

## Uniform Resource Identifier

![](lesson_8_10_uri.png "Uniform Resource Identifier")

![](lesson_8_10_uri_example.png "Uniform Resource Identifier example")

![](lesson_8_10_uri_review.png "Uniform Resource Identifier Review")

## Calling the ContentProvider

### Make an AsyncTask

The goal is to make an **AsyncTask** that loads the data on a background thread in a Cursor object. It then updates a variable called **mData** in the MainActivity to store the returned **Cursor**.

#### Steps to get the data from the Content Provider and save it into an instance variable :

1. Create an **AsyncTask** with the following generic types **<Void, Void, Cursor>**
2. In the **doInBackground** method, write the code to access the DroidTermsExample provider and return the **Cursor** object.
3. Create an instance variable **Cursor mData**.
4. In the **onPostExecute** method, store the **Cursor** object in **mData**.
5. Create and execute the **AsyncTask** in **onCreate**.

```java
// Create an instance variable storing a Cursor called mData
private Cursor mData;

// Use an async task to do the data fetch off of the main thread.
public class WordFetchTask extends AsyncTask<Void, Void, Cursor> {

    // Invoked on a background thread
    @Override
    protected Cursor doInBackground(Void... params) {
        // Make the query to get the data

        // Get the content resolver
        ContentResolver resolver = getContentResolver();

        // Call the query method on the resolver with the correct Uri from the contract class
        Cursor cursor = resolver.query(DroidTermsExampleContract.CONTENT_URI,
                null, null, null, null);
        return cursor;
    }

    // Invoked on UI thread
    @Override
    protected void onPostExecute(Cursor cursor) {
        super.onPostExecute(cursor);

        // Set the data for MainActivity
        mData = cursor;
    }
}

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Get the views
    mButton = (Button) findViewById(R.id.button_next);

    // Run the database operation to get the cursor off of the main thread
    // Create and execute your AsyncTask here
    new WordFetchTask().execute();
}
```

## Structure of the Data




