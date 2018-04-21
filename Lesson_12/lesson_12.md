# Lesson 12 - Polishing the UI

https://github.com/udacity/ud851-Exercises/tree/student/Lesson12-Visual-Polish

## Android Design Principles

Users jugde the quality of your app within the first 30 seconds.

For some guidance on how to make slick and beautiful apps, check out [Material Design](https://developer.android.com/design/material/index.html). Material Design is a design language incorporated in the Android Lollipop release. The [Material Design specifications](https://material.io/guidelines/material-design/introduction.html) is a great place to start.

## Visual Mocks and Keylines

Mockup = a model of an app, used for design evaluations.

Keyline = lines that specify the size and the spacing of app components.

Material Design = a set of principles for creating useful and beautiful visuals.

## Color Guidelines

### Color Palette Tools

Material Design Guideline recommend a primary color (3 slightly different shades) and an accent color.

Primary color = menu bar...

Accent color = serves to draw attention to key elements like buttons.

Following material design guidelines, Google provides [vibrant color palettes](https://material.io/guidelines/style/color.html#color-color-palette) for use in Android apps.

There are also other helpful resources for choosing a color palette for your app, including [this primary and accent color palette generator](https://www.materialpalette.com/).


## Typography

[Typography Guidelines](https://material.io/guidelines/style/typography.html)

The default text for Android is a font called Roboto.

Font-family = groups of fonts that share similar design characteristics, like serif or sans-serif.

Sans-serif is the default in Android.

Scale-Independent Pixels = scale-independent pixels will stay the same physical size across different resolution screens. Text size is mesured in units of sp (scale independent pixels).

SP is also used for accesibility purposes.

## Changing colors and fonts

In colors.xml file:
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Base application colors -->
    <color name="colorPrimary">#673AB7</color>
    <color name="colorPrimaryDark">#512DA8</color>
    <color name="colorAccent">#FF9100</color>
    <color name="colorPrimaryLight">#D1C4E9</color>
</resources>
```
Font Example:
```xml
<TextView
    android:id="@+id/text16"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="@string/smallcaps_16"
    android:textSize="16sp"
    android:fontFamily="sans-serif-smallcaps"/>
```

## Styles and Themes

Styles = a style is an xml resource file, separate from the layouts, qhere you can set all these properties in one place. Then later, we can apply that style to any View we want.

Theme = is just a style that's applied to an entire Activity or application and not just one view.

## Style a mail layout




