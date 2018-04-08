## Lesson 7  - Storing Data in SQlite

## Creating the Contract

Design what the database will look like.
Define the tables and the columns for each table.

The **contract** is a class, then we need to create an **inner class for each table**. 

The **constructor** needs to be private : you should never neef to create an instance of the contract class because the contract is simply a class filled with DB related constants thar are all static.

The inner class can (not mandatory) implements the interface **BaseColumns**.
The BaseColumns interface **automatically includes** a constant representing the primary key field called **_ID**.

In WaitlistContract class :
```java
public static final class WaitlistEntry implements BaseColumns {
    public static final String TABLE_NAME = "waitlist";
    public static final String COLUMN_GUEST_NAME = "guestName";
    public static final String COLUMN_PARTY_SIZE = "partySize";
    public static final String COLUMN_TIMESTAMP = "timestamp";
}
```

## Creating the database



