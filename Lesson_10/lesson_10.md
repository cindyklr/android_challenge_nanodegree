# Lesson 10 - Background Tasks

https://github.com/udacity/ud851-Exercises/tree/student/Lesson10-Hydration-Reminder

## Services

Great for things like processing loading and processing of data in the background.

![](lesson_10_4_services.png "Services")

## Services vs Loaders

### Loaders 

If the background task is loading information that will only be used in the activity, it's good candidate for a loader.

### Service

When the task that you are doing is decoupled from the user interface.

![](lesson_10_5_services_loaders.png "Loaders vs Services")

## Starting Services

[Bound Services](https://developer.android.com/guide/components/bound-services.html)

![](lesson_10_7_starting_services_1.png "Starting Services")

![](lesson_10_7_starting_services_2.png "Starting Services")

![](lesson_10_7_starting_services_3.png "Starting Services")

![](lesson_10_7_starting_services_4.png "Starting Services")

![](lesson_10_7_starting_services_5.png "Starting Services")

![](lesson_10_7_starting_services_6.png "Starting Services")

![](lesson_10_7_starting_services_7.png "Starting Services")

## Running Services in the Background

![](lesson_10_8_lifecycle_services.png "Lifecycle Services")

## Intent Services

![](lesson_10_9_intent_services_1.png "Intent Services")

![](lesson_10_9_intent_services_2.png "Intent Services")

![](lesson_10_9_intent_services_3.png "Intent Services")

![](lesson_10_9_intent_services_4.png "Intent Services")

![](lesson_10_9_intent_services_5.png "Intent Services")

## Starter Code

### Pluralization in Android

Part of Android’s robust resource framework involves a mechanism for pluralizing strings called “Quantity Strings”. In the **strings.xml** file for the Hydration Reminder app, you’ll see an example of how pluralization can be used:

```xml
<plurals name="charge_notification_count">
   <item quantity="zero">Hydrate while charging reminder sent %d times</item>
   <item quantity="one">Hydrate while charging reminder sent %d time</item>
   <item quantity="other">Hydrate while charging reminder sent %d times</item>
</plurals>
```

When you use the plural in code, you specify a quantity number. This number specifies what string should be used. In this case:

- if the number is zero, use ```<item quantity="zero">```
- If the number is one, use ```<item quantity="one">```
- otherwise use ```<item quantity="other">```

Then in the **MainActivity** we have the following Java code to generate the correct String:

```java
String formattedChargingReminders = getResources().getQuantityString(R.plurals.charge_notification_count, chargingReminders, chargingReminders);
```

The first usage of chargingReminder is the quantity number. It determines which version of the pluralized string to use (you must pass in a number). The second usage of chargingReminder is the number that’s actually inserted into the formatted string.

For more detail on Quantity Strings, check out the [documentation](https://developer.android.com/guide/topics/resources/string-resource.html#Plurals)

## Plan for Adding an IntentService

![](lesson_10_12_intent_services.png "Intent Services")

![](lesson_10_12_sunshine.png "Sunshine App")

![](lesson_10_12_sunshine_intent_services.png "Intent Services Sunshine App")

![](lesson_10_12_reminderTask.png "ReminderTask")

Steps to Implement the **IntentService**
- Create a new class that extends IntentService
- Override onHandleIntent
- Start the service using startService()

## Add an IntentService

