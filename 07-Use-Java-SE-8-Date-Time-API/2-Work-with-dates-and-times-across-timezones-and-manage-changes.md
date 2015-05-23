#Work with dates and times across timezones and manage changes resulting from daylight savings including Format date and times values
###Timezones
Time zones are defined by their offset from Coordinated Universal Time (UTC) and correspond to a region in which the time is the same.

Time zones can be referred to by two identifiers: abbreviated, for example, "PLT" and longer, for example, "Europe/Paris".
[ZoneId](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html) is an identifier for a region:
````java
ZoneId id = ZoneId.of("Europe/Paris");
````
[ZoneOffset](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneOffset.html) is the period of time representing a difference between Greenwich/UTC and a time zone.
````java
ZoneOffset offset = ZoneOffset.of("-6:00");
````
[ZonedDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/ZonedDateTime.html) is a date and time with a fully qualified time zone. You should use this class if you want to represent a date and time without relying on the context of a specific server.  
````java
ZonedDateTime zdt1 = ZonedDateTime.parse("2014-12-03T10:15:300[Europe/Paris]");//2014-12-03T10:15:300Z[Europe/Dublin]
ZonedDateTime zdt2 = ZonedDateTime.now(ZoneId.of("Europe/Paris"));
````
[OffsetDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html) is an immutable representation of a date-time with an offset from UTC/Greenwich, for example '2000-12-31T10:15:30+01:00'.

OffsetDateTime, ZonedDateTime and Instant all store an instant on the timeline to a nanosecond precision. Instant is the simplest, just representing the instant. OffsetDateTime adds to the instant the offset from UTC/Greenwich, which allows the local date-time to be obtained. ZonedDateTime adds full timezone data.

[OffsetTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetTime.html) is a time with an offset from UTC/Greenwich in the ISO-8601 calendar system, such as '08:45:21+05:00'.
````java
OffsetDateTime odt = OffsetDateTime.of(LocaDateTime.now(),ZoneOffset.of("-4")); //2015-05-22T23:42:20.101-06:00
OffsetTime ot = OffsetTime.ofInstant(Intant.now(),ZoneId.of("America/Los_Angeles")); //22:42:20.101-07:00
````

[Clock](http://docs.oracle.com/javase/8/docs/api/java/time/Clock.html) gives us the ability to get the current date/time from the system clock with a specific timezone:
````java
Clock default = Clock.systemDefaultZone();
Clock clock = Clock.system(ZoneId.of("Europe/Italy"));
````

###Formatting
[java.time.format.DateTimeFormatter](http://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html) is the class for printing and parsing date-time objects.

This class works by using:
* Predefined constants, such as ISO_LOCAL_DATE
* Pattern letters, such as yyyy-MMM-dd
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
