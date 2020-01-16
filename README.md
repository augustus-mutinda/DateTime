# DateTime

This library is a package of functions that let you manipulate objects and or java date string. it combine the most common functions used when managing dates under android, such as converting a mysql /sqlLite date to a Date object and vis-versa etc.

This library is available under the [MIT License](http://www.opensource.org/licenses/mit-license.php).

This library was forked from [Thunder413's liblary](https://github.com/thunder413/DateTimeUtils).


## Usage

The DateTime library is available from [JitPack](https://jitpack.io/#augustusiam/DateTime/1.0.0).

First add JitPack dependency line in your project `build.gradle` file:

```xml
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```

And then simply add the following line to the `dependencies` section of your app module `build.gradle` file:

```groovy
implementation 'com.github.augustusiam:DateTime:1.0.0'
```

## Examples

### setTimeZone

``setTimeZone`` allow you to define your time zone by default it's ``UTC``

```java
DateTime.setTimeZone("UTC");
```
### formatDate

``formatDate`` is a method that allow you to convert ``date object`` to ``string`` or ``timeStamp`` to date and vice-versa.

#### Date string to Date object 

```java
// MySQL/SQLite dateTime example
Date date = DateTime.formatDate("2017-06-13 04:14:49");
// Or also with / separator
Date date = DateTime.formatDate("2017/06/13 04:14:49");
// MySQL/SQLite date example
Date date = DateTime.formatDate("2017-06-13");
// Or also with / separator
Date date = DateTime.formatDate("2017/06/13");
```
#### Date object to date string MySQL/SQLite

```java
String date = DateTime.formatDate(new Date());
```

#### timeStamp to Date object

By default it will considere given timeStamp in milliseconds but in case you did retrieve the timeStamp from server wich usually will be in seconds supply ``DateTimeUnits.SECONDS`` to tell the fonction about

```java
// Using milliseconds
Date date = DateTime.formatDate(1497399731000);
// Using seconds (Server timeStamp)
Date date = DateTime.formatDate(1497399731,DateTimeUnits.SECONDS);
```

### formatWithStyle

``formatWithStyle``  allow to parse date into localized format using most common style

#### Date object to localized date

```java
DateTime.formatWithStyle(new Date(), DateTimeStyle.FULL); // Tuesday, June 13, 2017
DateTime.formatWithStyle(new Date(), DateTimeStyle.LONG); // June 13, 2017
DateTime.formatWithStyle(new Date(), DateTimeStyle.MEDIUM); // Jun 13, 2017
DateTime.formatWithStyle(new Date(), DateTimeStyle.SHORT); // 06/13/17
```

#### Date string to localized date

```java
DateTime.formatWithStyle("2017-06-13", DateTimeStyle.FULL); // Tuesday, June 13, 2017
DateTime.formatWithStyle("2017-06-13", DateTimeStyle.LONG); // June 13, 2017
DateTime.formatWithStyle("2017-06-13", DateTimeStyle.MEDIUM); // Jun 13, 2017
DateTime.formatWithStyle("2017-06-13", DateTimeStyle.SHORT); // 06/13/17
```

### formatWithPattern

``formatWithPattern`` allow to define your own parse pattern following  ``SimpleDateFormat`` scheme

#### Date string as source

```java
DateTime.formatWithPattern("2017-06-13", "EEEE, MMMM dd, yyyy"); // Tuesday, June 13, 2017
```

#### Date object as source

```java
DateTime.formatWithPattern(new Date(), "EEEE, MMMM dd, yyyy"); // Tuesday, June 13, 2017
```

 ### isToday

``isToday`` Tell whether or not a given date is today date 

```java
// Date object as source
boolean state = DateTime.isToday(new Date());
// Date String as source
boolean state = DateTime.isToday("2017-06-15 04:14:49");
```

### isYesterday

``isYesterday`` Tell whether or not a given date is yesterday date 

```java
// Date object as source
boolean state = DateTime.isYesterday(new Date());
// Date String as source
boolean state = DateTime.isYestrday("2017-06-15 04:14:49");
```
### Get Previous next Week

``getPreviousWeekDate/getNextWeekDate`` Return the next or a previous week date from a given date it also allow you to set the day of the week by using Calendar Constant

```java
// Date object as source
Date date = DateTime.getPreviousWeekDate(new Date(), Calendar.MONDAY);
// Date String as source
Date date = DateTime.getNextWeekDate("2017-06-15 04:14:49",Calendar.SUNDAY);

```
### Get Previous next month

``getPreviousMonthDate/getNextMonthDate`` Return the next or a previous month date from a given date

```java
// Date object as source
Date date = DateTime.getNextMonthDate(new Date());
// Date String as source
Date date = DateTime.getPreviousMonthDate("2017-06-15 04:14:49");

```
### getDateDiff

``getDateDiff`` give you the difference between two date in days, hours, minutes, seconds or milliseconds ``DateTimeUnits`` 

```java
// Dates can be date object or date string
Date date = new Date();
String date2 = "2017-06-13 04:14:49";
// Get difference in milliseconds
int diff = DateTime.getDateDiff(date,date2, DateTimeUnits.MILLISECONDS);
// Get difference in seconds
int diff = DateTime.getDateDiff(date,date2, DateTimeUnits.SECONDS);
// Get difference in minutes
int diff = DateTime.getDateDiff(date,date2, DateTimeUnits.MINUTES);
// Get difference in hours
int diff = DateTime.getDateDiff(date,date2, DateTimeUnits.HOURS);
// Get difference in days
int diff = DateTime.getDateDiff(date,date2, DateTimeUnits.DAYS);
```

### getTimeAgo

``getTimeAgo`` give ou the elapsed time since a given date, it also offer two print mode the full and short strings ``eg . 3 hours ago | 3h ago`` the strings are localized but at the moment only FR and EN language are available. If you need your langage to be add just let me know :)

```java
String timeAgo = DateTime.getTimeAgo(context,new Date()); // Full string style will be used
// Short string style
String timeAgo = DateTime.getTimeAgo(context,"new Date()",DateTimeStyle.AGO_SHORT_STRING ); 
```

### formatTime

``formatTime`` allow you to extract time from date by default it wont show the hours if equal to ``0`` but you can supply ``forceShowHours`` parameter to force hours display

```java
String time = DateTime.formatTime(new Date()); // 14:49 if hours equals 0 or 04:14:09 if hours witch is wrong when use it on time rather than a duration
// Solution >> force hours display
String time = DateTime.formatTime(new Date(),true);
// And you can also supplie a date string
String time = DateTime.formatTime("2017-06-13 04:14:49"); // 04:14:49
```

### millisToTime

``millisToTime`` is usefull when your dealing with duration and want to display for example player duration or current playback position into human readable value.

```java
String time = DateTime.millisToTime(2515); // It take millis as an argument not seconds
```

### timeToMillis

``timeToMillis`` allow to convert ``time`` string to ``millseconds`` 

```java
int milliseconds = DateTime.timeToMillis("14:20"); // 860000
```



## Author 

- **Thunder413** (https://github.com/thunder413)
- **Edited by Augustusiam** (https://github.com/augustusiam)

## License

This project is licensed under the  [MIT License](http://www.opensource.org/licenses/mit-license.php) 
