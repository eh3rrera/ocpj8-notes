#Work with dates and times across timezones and manage changes resulting from daylight savings including Format date and times values
###Timezones
Time zones are defined by their offset from Coordinated Universal Time (UTC) and correspond to a region in which the time is the same.

###Formatting
[java.time.format.DateTimeFormatter](http://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html) is the class for printing and parsing date-time objects.

This class works by using:
* Predefined constants, such as ISO_LOCAL_DATE
* Pattern letters, such as uuuu-MMM-dd
* Localized styles, such as long or medium

The date-time classes provide two methods - one for formatting, for example:
````java
LocalDateTime dt = LocalDateTime.of( 2010, Month.JULY, 03, 09, 0, 30 );
String isoDateTime = dt.format(DateTimeFormatter.ISO_DATE_TIME);
````
And one for parsing, for example:
````java
LocalDate dt = LocalDate.parse( "2014/09/19 14:05:12", DateTimeFormatter.ofPattern( "yyyy/MM/dd kk:mm:ss" ) );
````
The last example makes use of a pattern. Patterns are sequences of letters and symbols used to create a Formatter using the `ofPattern(String)` and `ofPattern(String, Locale)` methods.
