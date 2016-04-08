#Create and manage date-based and time-based events including a combination of date and time into a single object using LocalDate, LocalTime, LocalDateTime, Instant, Period, and Duration

The new Date/Time API was designed with the following principles:
* Immutable classes
* Dates and times are separated 
* Support for different calendaring systems

###LocalDate, LocalTime and LocalDateTime
The first classes to learn when using the new API are [LocalDate](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html), [LocalTime](https://docs.oracle.com/javase/8/docs/api/java/time/LocalTime.html) and [LocalDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html), which is a pairing of the former classes:
````java
LocalTime time = LocalTime.now();
LocalDate date = LocalDate.now();
LocalDateTime dt = LocalDateTime.of( date, time ); // You can also call LocalDateTime.now();
````
They are local in the sense that they represent date and time from the context of one observer, in contrast to time zones.

All the core classes in the new API are constructed by factory methods. When constructing a value through its fields, the factory is called *of*. When converting from another type, the factory is called *from*. There are also parse methods that take strings as parameters:
````java
LocalDate ld1 = LocalDate.of(2014, Month.SEPTEMBER, 19);
LocalDate ld2 = LocalDate.ofEpochDay(1000);
LocalTime lt1 = LocalTime.of(14, 05);
LocalTime lt2 = LocalTime.parse("14:05:00");
````

You can use standard getters to obtain values from the classes:
````java
int m = LocalDate.now().getDayOfMonth();
int y = LocalDate.now().getYear();
int h = LocalTime.now().getHour();
int min = LocalTime.now().getMinute();
````

You can also modify the object values by using the *with* methods instead of using setters (because the classes are immutable, which also means that you don't actually modify a class, a new one is returned):
````java
LocalDateTime thePast = dt.withDayOfYear(90).withHour(21);
````

There are other methods to perform calculations:
````java
LocalDateTime dt = dt.plusMinutes(10).plus(2, ChronoUnit.DAYS);
LocalDateTime dt = dt.minusYears(10);
````

###Instant
An instant is a point of time counting from the first second of 1/1/1970, also known as epoch. Instants after the epoch have positive values, and earlier instants have negative values and a larger value is always later on the timeline than a smaller value.

The range of an instant requires the storage of a number larger than a long. To achieve this, the class stores a long representing epoch-seconds and an int representing nanosecond-of-second, which will always be between 0 and 999,999,999.

An Instant can be created in a similar way as a date or a time:
````java
Instant now = Instant.now();
Instant epochNow = Instant.ofEpochSecond(1000000);
````
It also has get, plus and minus methods:
````java
long s = Instant.now().getEpochSecond();
int n = Instant.now().getNano();
Instant twoSecondsAfter = now.plusSeconds(2);
Instant twoSecondsBefore = now.minusSeconds(2);
````

###Period
A period represents a value such as "1 months and 15 days", in contrast to the other classes that represent a point in time.

Here are some ways to create a period:
````java
Period period = Period.of(1, 2, 3); // 1 year, 2 months, 3 days
Period periodTwoMonths = Period.ofMonths(2);
Period period20142015 = Period.between(LocalDate.of( 2014, Month.JANUARY, 1), LocalDate.of( 2015, Month.JANUARY, 1));
````
It also has get, plus and minus methods:
````java
int y = period.getYears();
Period newPeriod = period.plusDays(2).minusMonths(1);
````

You can modify the values of dates using periods:
````java
LocalDate newDate = date.plus(period);
````

###Duration
A duration is similar to a period but its precision is based on hours, minutes, seconds, milliseconds. 

A duration can be created using an amount of seconds or minutes or hours or by specifying start and end times:
````java
Duration d2 = Duration.ofSeconds(10, 50); // 10 seconds and 50 nanoseconds
Duration d2 = Duration.between(LocalTime.NOON, LocalTime.MIDNIGHT);
````

It's also possible to perform normal plus, minus, and with operations on durations and also like periods, modify the value of a date or time using a duration.
