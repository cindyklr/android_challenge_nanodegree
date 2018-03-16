# Creating and using a Custom ArrayAdapter

[Exemple Project](https://github.com/udacity/android-custom-arrayadapter)

[Webcast](https://plus.google.com/u/0/events/chlh8qqr5q5grs1lajpqnvvql8k?authkey=CNXMrZuHsMWhNg)

## Purpose
[Codepath](https://guides.codepath.com/android/Using-an-ArrayAdapter-with-ListView)

## Filling an adpter view with data

[Writting better Adapters](https://proandroiddev.com/writing-better-adapters-1b09758407d2)
=> Bind the AdapterView instance to an Adapter, wich retrieves data from an external source and create a View that represents each data entry.

One of the most common adapters is : 
- **ArrayAdapter** when the data source is an array.

```java
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this, // context,
android.R.layout.simple_list_item, // the layout that contains a TextView for each string in the array,
myStringArray); //  the string array
```
Then, call **setAdapter()** on your **ListView** :
```java
ListView listView = (ListView) findViewById(R.id.listview);
listView.setAdapter(adapter);
```

### ArrayAdapter
By default, the array adapter creates a view by calling **toString()** on each data object in the collection you provide, and places the result in a **TextView**. 


### Custom ArrayAdapter

To customize what type of view is used for the data object, override **getView(int, View, ViewGroup)** and inflate a **view resource**.

Create a **model** to make an array of Object rather than an simple array.

```java
public class AndroidFlavor {
    String versionName;
    String versionNumber;
    int image;git 

    public AndroidFlavor(String vName, String vNumber, int image) {
        this.versionName = vName;
        this.versionNumber = vNumber;
        this.image = image;
    }
}
```

```java
AndroidFlavor[] androidFlavors = {
    new AndroidFlavor("Cupcake", "1.5", R.drawable.cupcake),
    new AndroidFlavor("Donut", "1.6", R.drawable.donut),
    ...
}
```
```java
public class androidFlavorAdapter extends ArrayAdapter<AndroidFlavor> {
    private static final String LOG_TAG = AndroidFlavorAdapter.class.getSimpleName();

    public AndroidFlavorAdapter(Activity context, List<AndroidFlavor> androidFlavor) {
        super(context, 0, androidFlavors);
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        AndroidFlavor androidFlavor = getitem(position);
        View rootView = LayoutInflater.from(getContext().inflate(R.layout.list_item_flavor, parent));

        ImageView iconView = (ImageView) rootView.findViewById(R.id.listitem_icon);
        iconView.setImageResource(androidFlavor.image);

        TextView versionNameView = (TextView) rootView.findViewById(R.id.list_item_version_name);
        versionName.setText(androidFlavor.versionName);

        TextView versionNumberView = (TextView) rootView.findViewById(R.id.list_tem_versionnumber);
        versionNumberView.setText(androidFlavor.versionNumber);
        return rootView;
    }

}
```

