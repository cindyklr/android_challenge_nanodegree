# How to use MovieDB Api

## Before starting

- Create an account
- Request a key

## HTTP Request tot he URL

http://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=[THE_KEY]

http://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=[YOUR_KEY]

https://api.themoviedb.org/3/discover/movie?api_key=[YOUR_KEY_API]&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1

## Analyse the JSON Data

```json
{
  "page": 1,
  "total_results": 350929,
  "total_pages": 17547,
  "results": [
    {
      "vote_count": 900,
      "id": 337167,
      "video": false,
      "vote_average": 6.2,
      "title": "Fifty Shades Freed",
      "popularity": 525.701922,
      "poster_path": "/jjPJ4s3DWZZvI4vw8Xfi4Vqa1Q8.jpg",
      "original_language": "en",
      "original_title": "Fifty Shades Freed",
      "genre_ids": [
        18,
        10749
      ],
      "backdrop_path": "/9ywA15OAiwjSTvg3cBs9B7kOCBF.jpg",
      "adult": false,
      "overview": "Believing they have left behind shadowy figures from their past, newlyweds Christian and Ana fully embrace an inextricable connection and shared life of luxury. But just as she steps into her role as Mrs. Grey and he relaxes into an unfamiliar stability, new threats could jeopardize their happy ending before it even begins.",
      "release_date": "2018-02-07"
    },
    {
      "vote_count": 6540,
      "id": 269149,
      "video": false,
      "vote_average": 7.7,
      "title": "Zootopia",
      "popularity": 380.23527,
      "poster_path": "/sM33SANp9z6rXW8Itn7NnG1GOEs.jpg",
      "original_language": "en",
      "original_title": "Zootopia",
      "genre_ids": [
        16,
        12,
        10751,
        35
      ],
      "backdrop_path": "/mhdeE1yShHTaDbJVdWyTlzFvNkr.jpg",
      "adult": false,
      "overview": "Determined to prove herself, Officer Judy Hopps, the first bunny on Zootopia's police force, jumps at the chance to crack her first case - even if it means partnering with scam-artist fox Nick Wilde to solve the mystery.",
      "release_date": "2016-02-11"
    }
```
JSON Object
- unordered collectiono of name/value pairs
- String wrapped in curly braces with colons between the names and values, and commas between the value and names
```json
{
    name : value,
    name : value
},
{
    name : value
}
```

JSON Array
- Ordered sequence of values
- Sequence of values separated by commas enclosed with square brackets
- Values can be Boolean, String, JSONObject, JSONArray...

## Movie App Stage 2

Query for trailer and reviews using the movie IDs obtained from Stage 1 API requests

https://api.themoviedb.org/3/movie/[ID]/videos?api_key=[YOUR_API_KEY]

https://api.themoviedb.org/3/movie/[ID]/reviews?api_key=[YOUR_API_KEY]


Don't forget to remove the api key when submitting the project !!!
Don't forget to mention where to put the api key.

## GridView

```java
@Override
    public View getView(int position, View convertView, ViewGroup parent) {
        AndroidFlavor androidFlavor = getitem(position);

        if(convertView == null) {
           convertView = LayoutInflaterfrom(getContext()).inflate(R.layout.flavor_item, parent, false);
        }

        ImageView iconView = (ImageView) convertView.findViewById(R.id.flavor_image;
        iconView.setImageResource(androidFlavor.image);

        TextView versionNameView = (TextView) convertView.findViewById(R.id.flavor_text);
        versionName.setText(androidFlavor.versionName
         + " - " + androidFlavoir.versionNumber);

        return convertView;
    }
```
```java
@Override
public View onCreateView(LayoutInflater inflater, Viewgroup container Bundle savedInstanceState) {
    View rootView = inflater.inflate(R.layout.fragment_main, container, false);

    flavorAdapter = new AndroidFlavorAdapter(getActivity(), array.asList(androidFlavors));

    GridView gridView = (GridView) rootView.findViewById(R.id.flavors_grid);
    gridView.setAdapter(flavorAdapter);

    return rootView;
}
```
```xml
<GridView
    ...
    android:layout_width="match_parent"
     android:layout_height="match_parent"
     android:columnWidth="150dp"
     android:numColumns="auto_fit"
     android:verticalSpacing="0dp"
     android:horizontalSpacing="0dp"
     android:stretchMode="columnWidth"
     tools:context=".MainActivityFragment"
     android:id="@+id/flavors_grid">
</GridView>
```
```xml
<FrameLayout ...>
    <ImageView
     android:layout_width="200dp"
     android:layout_height="200dp"
     android:scaleType="centerCrop"
     android:id="@+id/flavor_image" />
    <TextView 
     android:layout_width="wrap_content"
     android:layout_height="wrap_content"
     android:id="@+id/flavor_text" />
</FrameLayout>
```