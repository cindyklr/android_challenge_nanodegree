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
