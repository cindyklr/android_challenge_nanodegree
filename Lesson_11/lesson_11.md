# Lesson 11 - Completing the UI

## Views & View Group

![](lesson_11_2_linear_layout.png "LinearLayout")

![](lesson_11_2_relative_layout.png "LinearLayout")

![](lesson_11_2_frame_layout.png "LinearLayout")

![](lesson_11_2_grid_layout.png "LinearLayout")

![](lesson_11_2_grid_layout_2.png "LinearLayout")

![](lesson_11_2_width_height.png "LinearLayout")

![](lesson_11_2_padding_margin.png "LinearLayout")

![](lesson_11_2_gravity.png "LinearLayout")

![](lesson_11_2_visibility.png "LinearLayout")

## Constraint Layout

Constraint Layout allows to create a complex layout without having to nest view group inside each other.

It's very similar to a relative layout in that older views are laid out relative to each other, or to the parent layout itself.

## Installing the Constraint Layout Library

To continue building the Boarding Pass app, you'll need to make sure you have the latest Constraint Layout library. To ensure you have the latest Constraint Layout library:

1. Click **Tools** > **Android** > **SDK Manager**.
2. Click the **SDK Tools** tab.
3. Expand **Support Repository** and then check **ConstraintLayout for Android** and **Solver for ConstraintLayout**. Check **Show Package Details** and take note of the version you're downloading (you'll need this below).
4. Click OK.
5. Add the **ConstraintLayout** library as a dependency in your module-level **build.gradle** file:

```
dependencies {
    compile 'com.android.support.constraint:constraint-layout:1.0.0-beta4'
}
```

6. The library version you download may be higher, so be sure the value you specify here matches the version from step 3.
7. In the toolbar or sync notification, click **Sync Project with Gradle Files**.
8. Now you're ready to build your layout with **ConstraintLayout**.

![](sdktools.png "SDK Tools")

## Design the Boarding Pass

![](lesson_11_4_boarding_pass.png "Boarding pass app")

In build.gradle:
```
// 1.  Add the compile dependency for the constraint layout support library
compile 'com.android.support.constraint:constraint-layout:1.0.0-beta4'
```

In activity_main.xml:
```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- 17. Surround the Constraint layout with a ScrollView -->
<ScrollView xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/scroll"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <!-- 2. Replace the Relative layout with a ConstraintLayout -->
    <android.support.constraint.ConstraintLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">


        <!-- 3. Create a TextView for the Passenger label and name -->
        <TextView
            android:text="@string/passenger_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/textViewPassengerLabel"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:letterSpacing="0.5"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            android:layout_marginStart="16dp"
            android:layout_marginTop="16dp"
            android:layout_marginLeft="16dp"
            tools:layout_constraintTop_creator="1"
            tools:layout_constraintLeft_creator="1" />

        <!-- 4. Use tool:text to set the text value -->
        <TextView
            tools:text="@string/passenger_name"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/textViewPassengerName"
            android:textAppearance="@style/TextAppearance.AppCompat.Display1"
            android:textColor="@color/colorPrimary"
            app:layout_constraintTop_toBottomOf="@+id/textViewPassengerLabel"
            android:layout_marginStart="16dp"
            app:layout_constraintLeft_toLeftOf="parent"
            android:layout_marginLeft="16dp"
            tools:layout_constraintTop_creator="1" />


        <!-- 5. Create an ImageView for the left rectangle -->
        <!-- 6. Set the background to the shape_rectangle_stroke drawable -->
        <ImageView
            android:id="@+id/leftRectangle"
            android:layout_width="60dp"
            android:layout_height="80dp"
            android:background="@drawable/shape_rectangle_stroke"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@id/textViewPassengerName"
            android:layout_marginLeft="32dp"
            android:layout_marginTop="16dp"
            android:layout_marginStart="32dp" />

        <!-- 7. Create an ImageView for the divider -->
        <ImageView
            android:id="@+id/divider"
            android:background="@color/colorPrimaryLight"
            android:layout_height="1dp"
            android:layout_width="0dp"
            app:layout_constraintLeft_toRightOf="@+id/leftRectangle"
            app:layout_constraintRight_toLeftOf="@+id/rightRectangle"
            app:layout_constraintTop_toBottomOf="@+id/rightRectangle"
            app:layout_constraintBottom_toTopOf="@+id/rightRectangle"
            app:layout_constraintHorizontal_bias="0.0"/>

        <!-- 8. Create an ImageView for the rightRectangle -->
        <ImageView
            android:id="@+id/rightRectangle"
            android:layout_width="60dp"
            android:layout_height="80dp"
            android:background="@drawable/shape_rectangle_stroke"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@id/textViewPassengerName"
            android:layout_marginRight="32dp"
            android:layout_marginTop="16dp"
            android:layout_marginEnd="32dp" />

        <!-- 9. Create a TextView for the origin code, the destination code and the flight code -->
        <TextView
            tools:text="@string/origin_code"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/textViewOriginAirport"
            android:textAppearance="@style/TextAppearance.AppCompat.Headline"
            app:layout_constraintBottom_toBottomOf="@+id/divider"
            app:layout_constraintRight_toRightOf="@+id/leftRectangle"
            app:layout_constraintTop_toBottomOf="@+id/divider"
            app:layout_constraintLeft_toLeftOf="@+id/leftRectangle" />

        <TextView
            tools:text="@string/destination_code"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/textViewDestinationAirport"
            android:textAppearance="@style/TextAppearance.AppCompat.Headline"
            app:layout_constraintBottom_toBottomOf="@+id/divider"
            app:layout_constraintRight_toRightOf="@+id/rightRectangle"
            app:layout_constraintTop_toBottomOf="@+id/divider"
            app:layout_constraintLeft_toLeftOf="@+id/rightRectangle" />

        <!-- 15. Import the plane image SVG file into the drawable directory and name it art_plane -->
        <!-- 16. Create an ImageView for the plane and set the background to art_plane drawable -->
        <ImageView
            android:id="@+id/imagePlane"
            android:layout_height="wrap_content"
            android:layout_width="wrap_content"
            android:background="@drawable/art_plane"
            app:layout_constraintBottom_toTopOf="@+id/divider"
            app:layout_constraintLeft_toRightOf="@+id/leftRectangle"
            app:layout_constraintRight_toLeftOf="@+id/rightRectangle"
            android:layout_marginBottom="16dp"
            />


        <TextView
            android:id="@+id/textViewFlightCode"
            tools:text="@string/flight_code"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Display1"
            android:textColor="@color/colorPrimary"

            app:layout_constraintTop_toTopOf="@+id/divider"
            app:layout_constraintLeft_toRightOf="@+id/leftRectangle"
            app:layout_constraintRight_toLeftOf="@+id/rightRectangle"
            android:layout_marginTop="8dp"
            android:layout_marginStart="8dp"
            android:layout_marginEnd="8dp"
            android:layout_marginLeft="8dp"
            android:layout_marginRight="8dp" />


        <!-- 10. Create a TextView for the time texts and their corresponding labels -->
        <TextView
            android:id="@+id/textViewBoardingTimeLabel"
            android:text="@string/boarding_time_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:letterSpacing="0.3"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/leftRectangle"
            android:layout_marginTop="16dp"
            android:layout_marginStart="16dp"
            android:layout_marginLeft="16dp" />


        <TextView
            android:id="@+id/textViewBoardingTime"
            tools:text="@string/boarding_time"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Display1"
            android:textColor="@android:color/black"
            app:layout_constraintLeft_toLeftOf="@+id/textViewBoardingTimeLabel"
            app:layout_constraintTop_toBottomOf="@+id/textViewBoardingTimeLabel" />


        <TextView
            android:id="@+id/textViewDepartureTimeLabel"
            android:text="@string/departure_time_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:letterSpacing="0.3"
            android:layout_marginTop="8dp"
            app:layout_constraintTop_toBottomOf="@+id/textViewBoardingTime"
            app:layout_constraintLeft_toLeftOf="@+id/textViewBoardingTime" />


        <TextView
            android:id="@+id/textViewDepartureTime"
            tools:text="@string/departure_time"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Headline"
            android:textColor="@color/colorGood"
            app:layout_constraintLeft_toLeftOf="@+id/textViewDepartureTimeLabel"
            app:layout_constraintTop_toBottomOf="@+id/textViewDepartureTimeLabel" />


        <TextView
            android:id="@+id/textViewBoardingInTimeLabel"
            android:text="@string/boarding_in_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:letterSpacing="0.3"
            android:layout_marginEnd="40dp"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/leftRectangle"
            android:layout_marginTop="16dp"
            android:layout_marginRight="40dp" />


        <TextView
            android:id="@+id/textViewBoardingInCountdown"
            tools:text="@string/boarding_in_time"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Display1"
            android:textColor="@color/colorBad"
            app:layout_constraintLeft_toLeftOf="@+id/textViewBoardingInTimeLabel"
            app:layout_constraintTop_toBottomOf="@+id/textViewBoardingInTimeLabel" />


        <TextView
            android:id="@+id/textViewArrivalTimeLabel"
            android:text="@string/arrival_time_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:letterSpacing="0.3"
            app:layout_constraintTop_toBottomOf="@+id/textViewBoardingInCountdown"
            app:layout_constraintLeft_toLeftOf="@+id/textViewBoardingInCountdown"
            android:layout_marginTop="8dp"/>


        <TextView
            android:id="@+id/textViewArrivalTime"
            tools:text="@string/arrival_time"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Headline"
            android:textColor="@color/colorGood"
            app:layout_constraintLeft_toLeftOf="@+id/textViewArrivalTimeLabel"
            app:layout_constraintTop_toBottomOf="@+id/textViewArrivalTimeLabel" />

        <!-- 11. Create an ImageView for the blue table's header -->
        <ImageView
            android:id="@+id/tableHeaderImage"
            android:background="@color/colorPrimaryLight"
            android:layout_height="24dp"
            android:layout_width="0dp"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            android:layout_marginTop="32dp"
            android:layout_marginLeft="16dp"
            android:layout_marginRight="16dp"
            app:layout_constraintTop_toBottomOf="@+id/textViewDepartureTime"
            app:layout_constraintHorizontal_bias="0.33" />

        <!-- 12. Create an ImageView for the blue table's body -->
        <ImageView
            android:id="@+id/tableImage"
            android:background="@color/colorPrimary"
            android:layout_height="0dp"
            android:layout_width="0dp"
            android:layout_marginLeft="16dp"
            android:layout_marginRight="16dp"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/tableHeaderImage"
            app:layout_constraintBottom_toBottomOf="@+id/textViewTerminal"/>


        <!-- 13. Create a TextView for each of the labels and text fields in the blue table -->
        <TextView
            android:id="@+id/textViewTerminalLabel"
            android:text="@string/terminal_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:textColor="@android:color/black"
            app:layout_constraintBottom_toBottomOf="@+id/tableHeaderImage"
            app:layout_constraintLeft_toLeftOf="@+id/textViewTerminal"
            app:layout_constraintRight_toRightOf="@+id/textViewTerminal"

            app:layout_constraintTop_toTopOf="@+id/tableHeaderImage" />

        <TextView
            android:id="@+id/textViewGateLabel"
            android:text="@string/gate_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:textColor="@android:color/black"
            app:layout_constraintBottom_toBottomOf="@+id/tableHeaderImage"
            app:layout_constraintLeft_toLeftOf="@+id/textViewGate"
            app:layout_constraintRight_toRightOf="@+id/textViewGate"
            app:layout_constraintTop_toTopOf="@+id/tableHeaderImage"
            />

        <TextView
            android:id="@+id/textViewSeatLabel"
            android:text="@string/seat_label"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textAppearance="@style/TextAppearance.AppCompat.Caption"
            android:textColor="@android:color/black"
            app:layout_constraintBottom_toBottomOf="@+id/tableHeaderImage"
            app:layout_constraintRight_toRightOf="@+id/textViewSeat"
            app:layout_constraintLeft_toLeftOf="@+id/textViewSeat"
            app:layout_constraintTop_toTopOf="@+id/tableHeaderImage"
            />

        <TextView
            tools:text="@string/terminal"
            android:layout_width="120dp"
            android:layout_height="wrap_content"
            android:id="@+id/textViewTerminal"
            app:layout_constraintTop_toTopOf="@+id/tableImage"
            app:layout_constraintLeft_toLeftOf="@+id/tableImage"
            app:layout_constraintRight_toRightOf="@+id/tableImage"
            android:textAppearance="@style/TextAppearance.AppCompat.Display2"
            android:textColor="@android:color/white"
            app:layout_constraintHorizontal_bias="0.0"
            android:textAlignment="center" />


        <TextView
            android:id="@+id/textViewGate"
            tools:text="@string/gate"
            android:layout_width="120dp"
            android:layout_height="0dp"
            app:layout_constraintLeft_toLeftOf="@+id/tableImage"
            app:layout_constraintRight_toRightOf="@+id/tableImage"
            android:textAppearance="@style/TextAppearance.AppCompat.Display2"
            android:textColor="@android:color/white"
            android:textAlignment="center"
            app:layout_constraintTop_toBottomOf="@+id/tableHeaderImage"
            app:layout_constraintBottom_toBottomOf="@+id/tableImage"/>

        <TextView
            android:id="@+id/textViewSeat"
            tools:text="@string/seat"
            android:layout_height="wrap_content"
            app:layout_constraintTop_toTopOf="@+id/tableImage"
            app:layout_constraintLeft_toLeftOf="@+id/tableImage"
            app:layout_constraintRight_toRightOf="@+id/tableImage"
            android:textAppearance="@style/TextAppearance.AppCompat.Display2"
            android:textColor="@android:color/white"
            app:layout_constraintHorizontal_bias="1.0"
            android:textAlignment="center"
            android:layout_width="120dp" />

        <!-- 14.Create an ImageView for the barcode -->
        <ImageView
            android:layout_width="100dp"
            android:layout_height="100dp"
            app:srcCompat="@mipmap/barcode"
            android:id="@+id/barcode"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/tableImage"
            android:layout_marginTop="16dp"
            />

    </android.support.constraint.ConstraintLayout>
</ScrollView>
```

## The Hierarchy Viewer

- Select Tools > Android > Android device Monitor.
- Then select Windows > Open Perspective.
- Finally, select Hierarchy View > OK.
- Click on the activity (on the left).

The hierarchy viewer builds a tree of all the views and view groups you have in any layout.

If the views aren't nested, it becomes super fast to load.

Too many views in a layout, nested or not, may still affect the display performance.

That's why it's always a good ideato break down your design in multiple screens, if you seems to be using too many views in one screen.

A general rule of thumbs is to have a maximum of 80 views in a single layout and never more then 10 nested view groups.

## Data Binding

![](lesson_11_12_data_binding.png "Data Binding")

Enable Data Binding in build.gradle, inside the Android section:
```
dataBinding{
    enabled = true
}
```
In activity_main.xml, surround the **ScrollView** tag with the **layout** tag:
```xml
<layout xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
xmlns:android="http://schemas.android.com/apk/res/android">
<ScrollView
    android:id="@+id/scroll"
    android:layout_width="match_parent"
android:layout_height="wrap_content">
...
</ScrollView>
</layout>
```



