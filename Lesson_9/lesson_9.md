# Lesson 9 - Building a Content Provider

## Steps to create a Provider

[Content Provider Documentation](https://developer.android.com/guide/topics/providers/content-providers.html)

1. Create a class that extends from the content provider and implements the onCreate() function.
2. Register the content provider in the Manifest.
3. Define URI's that identify the TaskContentProvider and the different data types that it can return.
4. Add these URI's to the Contract class.
5. Build a URIMatcher to match URI patterns to integers.
6. Implement the required CRUD methods.