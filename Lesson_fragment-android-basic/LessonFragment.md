# Android Multiple Screen 

## Fragment

### Navigation Patterns in Android


Navigation guides users between different parts of your app.

There are many ways to navigate around apps, each of which is best suited to the type of data that is being presented to the user. As you view more apps, you’ll notice some common navigation patterns.

The “master detail layout” consists of a master list of data. When you click one of those items of data, a detailed view of that item appears. You can easily adapt this layout to larger screen devices. When there is more screen real estate (meaning, more space on the screen) available, then we can view the master list of data alongside the detailed view of an item, at the same time.

![](fragment1.png "Fragment exemple 1")

Selecting an item from the Master Screen opens up more Details

Another way to view your data is to use a “Navigation Drawer” pattern. If an app has many screens that are "siblings" to each other, then the different screens can be listed in a "Drawer" that pulls out from the left side of the screen. In the Google News & Weather app, the navigation drawer provides links to different categories of news.

![](fragment2.png "Fragment exemple 1")

**Example of Navigation Drawer that comes in from the left side of the screen**

Another pattern that you’ll see is “swipeable tabs.” You can swipe horizontally left and right between different screens, or you can tap one of the tabs across the top of the screen. There’s a section on [tabs](https://material.io/guidelines/components/tabs.html)in the Design spec. Here’s an example of the YouTube app, which uses icons for each tab:

![](fragment3.png "Fragment exemple 1")

**This app contains 3 tabs that users can swipe through**

There are many other types of navigation. For example, the Google Calendar app has a scrolling agenda view, but you can jump to specific days by using the calendar month view. Or you can view different lengths of time like the week view. These interactions are specific to a calendar-based app.

![](fragment4.png "Fragment exemple 1")

**Google Calendar app contains a variety of user navigation patterns**

As you build your own app, you can learn more about how to structure your app in both the [navigation section](https://material.io/guidelines/patterns/navigation.html) of the Google Material Design spec and this guide on [designing effective navigation](https://developer.android.com/training/design-navigation/index.html). Keep in mind that your app will need to adapt to devices with a variety of screen sizes. This is known as responsive design, which we first talked about in the last course. Android apps must work across phones, tablets, and TVs, as well as watches and cars!

### Navigation Patterns in Other Apps

[http://androidniceties.tumblr.com/](http://androidniceties.tumblr.com/)

[https://pttrns.com/android-patterns](https://pttrns.com/android-patterns?srtby=popularity_desc)

## Up Button

You can create a diagram of the relationships between the screens of an app.

The following diagram shows an example of the relationship between screens in the Miwok app. The home screen (with the four category buttons) is the “parent” activity. It leads to the list of vocab words, which are the “children” activities. This type of parent-child relationship is important because sometimes the user may want to navigate to parent or child activities. It’s another way of navigating around the app, and can come in useful if the user lands somewhere within the app that’s not the home screen. See more details in the [training documentation](https://developer.android.com/training/design-navigation/screen-planning.html?utm_source=udacity&utm_medium=course&utm_campaign=android_basics#diagram-relationships).

![](fragment5.png "Relationship")

When viewing Android apps, you may have noticed a horizontal arrow pointing left in the app bar. This is called the “Up” button. In the upcoming coding task, you will be adding the “Up” button to NumbersActivity, FamilyActivity, ColorsActivity, and PhrasesActivity. 

![](fragment6.png "Relationship")

This button allows the user to navigate to the parent activity, which we will call MainActivity.

![](fragment7.png "Relationship")

#### “Up” Button vs. “Back” Button

Now you might be wondering, doesn’t the “Up” button just do the same thing as the “Back” button?

Well, not exactly. The “Back” button is part of the system navigation bar on Android (leftmost triangle icon). No matter which app you’re in, when you tap the “Back” button, you’ll go back to where you previously came from.

![](fragment8.png "Relationship")

However, there are certain cases where “Back” and “Up” result in different behavior. The “Up” button ALWAYS leads you to the parent activity. The “Back” button can lead you to the parent activity, or the home screen, or to another app, depending on how you arrived at the current screen.

Here’s an example scenario. Say you are browsing the web in an app. You receive notification of a new email. You click the notification, and suddenly you’re in the email app. Once you’re done reading the email, if you tap the “Back” button, you’ll go back to the web app. If you tap the “Up” button, you’ll go to the parent activity, which is the list of all emails.

The distinction between “Up” and “Back” really starts to matter if the user can get directly to a screen in your app without going through the main page (i.e. directly opening a single email without going through the list of all emails). In the Miwok app, the user has to go through the main screen, so “Up” and “Back” have the same effect. However, the ideal thing would be to provide the user with another way to navigate to the MainActivity.

For best practices, we will practice implementing the “Up” button. For information on how to do this, check out [this tutorial](https://developer.android.com/training/implementing-navigation/ancestral.html?utm_source=udacity&utm_medium=course&utm_campaign=android_basics).

This is what the app looks like before the coding task: 

![](fragment9.png "Relationship")

This is what the app looks like after the coding task (look closely at the app bar):

![](fragment10.png "Relationship")

##### Add Up Button to your Activity

- [implementing-navigation](http://developer.android.com/training/implementing-navigation/ancestral.html)

##### Additional Resources on Navigation:

- [design-navigation](http://developer.android.com/design/patterns/navigation.html)

- [navigation](http://developer.android.com/training/design-navigation/ancestral-temporal.html)

### An Alternative Version of the App

The app looks amazingly awesome and beautiful! It looks done! So why change it?

This can happen in app development teams. You build version 1 of an app. Then the team decides to do a design refresh, to have an even better user experience. Then you proceed to build version 2 of the app!

When you talk to any professional Android developer, they can tell you lots of stories of how the user interface for their app has evolved over the last months or even years.

As a developer, being able to **refactor** your code is an important skill to have. This means that the functionality of the app will remain the same, but visually the app will look differently. You can’t break any existing functionality (for example, you can’t lose the images or audio playback capabilities) when switching over to the new design. When you break something, and the user loses the ability to do something in the app compared to earlier versions, this is called **regression**.

To make sure that we don’t break anything, let’s move in small stages at a time. Try to make the app run on your device as often as possible. You don’t want to spend 5 days writing new code, and then realize that it doesn’t run on your device anymore.

Here are the new designs. We want to swipe between the word lists. This saves us an extra tap from having to open the vocab word lists. When we launch the app, we can immediately see the word lists. 

![](fragment11.png "New design")

**New design above with tabs to swipe for different lists of words.**

### Android Development Patterns

Now before we jump into Step 1: Review a Sample App, I’d like you to watch t[his short Android Development Patterns video](https://www.youtube.com/watch?v=zQekzaAgIlQ) on Tabs and ViewPager so that you can become familiar with the Android ViewPager component. After you are done, continue to the next step!

Note: You’ll hear the term “Fragments” in the video. We have not talked about Fragments yet, so don’t worry if you don’t understand everything perfectly.

#### Background context

This video is part of the Android Development Patterns created by Developer Advocates Ian Lake and Joanna Smith. (You saw them in the videos and articles from Lesson 4.)

Android Development Patterns will teach you how to build better apps by explaining the fundamental components of Android development, the reasoning behind them, and best practices for using them in your app. Feel free to check out [these videos](https://www.youtube.com/playlist?list=PLWz5rJ2EKKc-lJo_RGGXL2Psr8vVCTWjM) later.

### Upcoming Changes

We’re going to approach this change in multiple stages through the remainder of this lesson.

- Step 1: Review a Sample App
- Step 2: Refactor the logic for the four activities to use Fragments
- Step 3: Modify Main Activity so that it uses a ViewPager
- Step 4: Add Tabs

Here's an overview of what we'll do at each step:

#### Step 1: Review a Sample App

First you’ll experiment with a sample app that contains a something called a ViewPager. You’ll see how a FragmentPagerAdapter will provide a different Fragment for each “page” that you swipe to. Then we’ll learn a little more about Fragments, to prepare you for the next coding step.

![](fragment12.png "Step one")

#### Step 2: Refactor the logic for the four activities to use Fragments

Next, you’re going to refactor the current Miwok app from the 4 activities (numbers, colors, family, phrases) into the 4 fragments. The user-facing app will look the same, but all the logic to display the list of words will be in the fragments instead of the activity files. Once the logic is inside fragments, we can move to the next step.

- NumbersActivity will contain the NumbersFragment
- FamilyActivity will contain the FamilyFragment
- ColorsActivity will contain the ColorsFragment
- PhrasesActivity will contain the PhrasesFragment

![](fragment13.png "Step two")

#### Step 3: Modify Main Activity so that it uses a ViewPager

A ViewPager allows you to swipe between different “pages” or screens. We’re going to modify the MainActivity so it contains a ViewPager with 4 pages, where each page is a Fragment. We can swipe between each Fragment to see a different list of words.

At this point, we’re removing the layout that had a button for each category. We will also delete the category activities (NumbersActivity, FamilyActivity, ColorsActivity, PhrasesActivity) because the app only has 1 activity now (MainActivity). You can tell that we’re in the MainActivity because the app bar says “Miwok” across all the screens.

![](fragment14.png "Step three")

#### Step 4: Add Tabs

Lastly, once the ViewPager is working, we’ll add tabs across the top of the ViewPager, so you can tap to jump to a specific page.

![](fragment15.png "Step four")

### Sample ViewPager

#### Step 1: Review a Sample App

Let’s play with a sample app to explore how a ViewPager works in a simple scenario.

1. Download this sample app from the [GitHub link](https://github.com/udacity/ud839_ViewPager_Example/tree/quiz) by clicking on the “Download zip” (make sure you are on the "quiz" branch). 

![](fragment16.png "Step one github link")

2. Import this project into Android Studio and run the app on your device.

3. When you open the app, there should be 3 pages to swipe between in this ViewPager. First it should say “Monday”, then “Tuesday”, then “Wednesday.

![](fragment17.png "Step two")

4. Browse around the codebase and see how the layout and Java files are working together. Prepare for the quiz, which will ask you to modify this sample app.
How does it work?

The ViewPager works by getting its data from an adapter - called a FragmentPagerAdapter.

In our case, we want to customize the adapter to display our own fragments, so we have to use inheritance to subclass the FragmentPagerAdapter. By inheriting, we get all the functionality from the FragmentPagerAdapter for free, and we can add our own customization on top of it. We create the SimpleFragmentPagerAdapter class and extend from the FragmentPagerAdapter class.

When you launch the app on your device, first the ViewPager asks the adapter how many pages there will be. In our case, the adapter says there will be 3 pages. See the SimpleFragmentPagerAdapter getCount() method.

In order for the ViewPager to display page 0, the ViewPager asks the adapter for the 0th fragment. See the SimpleFragmentPagerAdapter getItem(int position) method. When the user swipes leftward, we move onto page 1, which means the ViewPager asks the adapter for the fragment at position 1. When we get to page 2, the ViewPager asks the adapter for the fragment at position 2. Thus, depending on which page (also known as position), the user has swiped to, the corresponding fragment gets shown.

### Intro to Fragments
A fragment is just a part of an activity. You can have a fragment that takes up part of a screen or a whole screen. Or you can show multiple fragments at the same time to make up a whole screen. Within an activity, you can also swap out different fragments with each other. (You can also have invisible fragments as well, that do some work related to the activity, but we won’t cover those in this course.)

Fragments were introduced in Android when we started building for larger screen devices like tablets. Let me show you an example.

In the master/detail pattern, a list fragment is on the left-side of the screen, while the detail fragment on the right swaps out depending on the list item selected.

![](fragment18.png "fragment")

[image source](https://developer.android.com/guide/components/fragments.html?utm_source=udacity&utm_medium=course&utm_campaign=android_basics#Design%22%20target=%22_blank%22%3ESource%3C/a)

In this case, using fragments is convenient when adapting the app to smaller devices like phones. When the user opens the app on a phone, they can see the list fragment. If they tap on an item in the list, they can navigate to the detail fragment. 

![](fragment19.png "fragment")

On the phone, only 1 fragment is shown at a time. On the tablet, 2 fragments are shown beside each other at the same time, to take advantage of the larger screen real estate available. 

![](fragment20.png "fragment")

This is just one use case for fragments. You can split up the logic of your app into as many fragments as you want. However, splitting it up into too many fragments can cause extra overhead because your Activity will need to manage communication between the fragments.

A Fragment is a Java class. You create your own Fragment, just like you created your own activities. You subclass the Fragment class in the Android framework.

#### Review Inheritance

Remember earlier we discussed the concept of inheritance in Java in which subclasses are derived from a superclass. In our original code, the Activity class created by the Android framework is the superclass and classes we created such as the MainActivity or NumbersActivity are subclasses that inherit from the Activity class.

![](fragment21.png "fragment inheritance")

Similarly, the Fragment class is a class provided by the Android framework. The fragments we've create - NumbersFragment, ColorsFragment, etc - are subclasses that inherit from the Fragment super class. 

![](fragment22.png "fragment inheritance")
