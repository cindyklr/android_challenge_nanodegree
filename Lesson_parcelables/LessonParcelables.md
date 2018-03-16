# Parcelables and onSaveInstanceState()

[Article](http://www.developerphil.com/parcelable-vs-serializable/)

[Webcast](https://plus.google.com/u/0/events/cfftk1qo4tjn7enecof6f9oes0o?authkey=CNu5uui-k5qAtQE)
[Repo Github](https://github.com/udacity/android-custom-arrayadapter/tree/parcelable)

## Parcelables 
More efficient than Serializable

```java
public class AndroidFlavor implements Parcelable {
    String versionName;
    String versionNumber;
    int image;

    public AndroidFlavor(String vName, String vNumber, int image) {
       this.versionName = vName;
       this.versionNumber = vNumber;
       this.image = image;
    }

   private AndroidFlavor(Parcel in) {
       versionName = in.readString();
       versionNumber = in.readString();
       image = in.readInt();
   }

   @Override
   public int describeContents() { return 0;}

   public String toString() { return versionName + "--" + versionNumber + "--" + image;}

   @Override
   public void writeToParcel(Parcel parcel, int i) {
       parcel.writeString(versionName);
       parcel.writeString(versionNumber);
       parcel.writeInt(image);
   }

   public final Parcelable.Creator<AndroidFlavor> CREATOR = new Parcelable.Creator<AndroidFlavor>() {
       @Override
       public AndroidFlavor creatorFromParcel(Parcel parcel) { return new AndroidFlavor(parcel); }

       @Override
       public AndroidFlavor[] new Array(int i) { return AndroidFlavor[i]; }
   } ;
}
```

## onSaveInstanceState

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    if(savedInstanceState == null || !savedInstanceState.containsKey("flavors")) {
        flavorList = new ArrayList<AndroidFlavor>(Array.asList(androidFlavors));
    }
    else {
        flavorList = savedInstanceState.getParcelableArrayList("flavors");
    }
}

@Override
public void onSaveInstanceState(Bundle outState) (
    outState.putParcelableArrayList("flavors", flavorList);
    super.onSaveInstanceStateout(outState);
)
```