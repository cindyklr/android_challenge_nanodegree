# Lesson 6 - Preferences

## Data Persistence

SavedInstanceState : allows to save key- value pairs, to store the state of one of the views.
It's usually used to save the state during things like app rotation or if the system destroys the activity because of memory constraints.
Should only be used if the user is still actively using the app.

![](lesson_6_5_savedinstancestate.png "savedInstanceState")

If we need data available across app restarts and turning the phone off and on again :

1. SharedPreferences class : specify a file and it saves simple key value pairs to that file
=> to save single text or numerical value about the user.
![](lesson_6_5_sharedpreferences.png "shared preferences")

2. Databases :  for complexe data with relations

3. Internal/External storage (to save files): store multimedia or large amounts of text. 

4. In the Cloud (database on a server or service like Google's Firebase) : save data in a place accessed by multiple devices.

![](lesson_6_5_storage_solutions.png "Storage solutions")

## Preference Fragments

Fragment = a class that represents a modular and reusable piece of an Activity

![](lesson_6_7_fragment.png "Fragments")

![](lesson_6_7_fragments_mobile_tablet.png "Fragments")

PreferenceFragment = 

![](lesson_6_7_preferencefragment.png "PreferenceFragments")

