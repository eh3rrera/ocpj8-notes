#Define and create and manage date-based and time-based events using Instant, Period, Duration, and TemporalUnit

[Instant](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html) captures the current moment in time. They are useful for obtaining timestamps to a nanosecond precision.
````java
Instant i = Instants.now();
````

[Period](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html) represents an amount of time in years, months, and/or days. They are useful for adding/subtracting time to/from a date:
````java
LocalDateTime today = LocalDateTime.now();
Period period = Period.ofDays(7);
LocalDateTime nextWeek = today.plus(period);
````

[Duration](https://docs.oracle.com/javase/8/docs/api/java/time/Duration.html) represents an amount of time in hours, minutes, and/or seconds. Same concept as period but with time units:
````java
LocalTime now = LocalDateTime.now();
Duration tenMinutes = Duration.ofMinutes(10);
LocalTime tenMinutesLater = now.plus(tenMinutes);
````

Period and Duration also have a `between()`method to for determining elapsed time between dates (or time) objects:
````java
LocalDate ld1 = LocalDate.parse("2015-05-23");
LocalDate ld2 = LocalDate.parse("2014-05-23");
Period timeBetween = Period.between(ld1,ld2); //Difference in years, months, days
Duration timeSpan = Duration.between(ld1,ld2); //Difference in hours, minutes, seconds
````

[TemporalUnit](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalUnit.html) is an interface that represents a unit of date-time, like years, months, days, hours, minutes and seconds. It doesn't represent the amount of the unit. Its implementation is the class [ChronoUnit](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoUnit.html), which contains enum constants like:
* NANOS - Unit that represents the concept of a nanosecond
* SECONDS - Unit that represents the concept of a second.
* HALF_DAYS - Unit that represents the concept of half a day.
* MILLENNIA - Unit that represents the concept of a millennium. For the ISO calendar system, it is equal to 1000 years.

And almost any other time unit you can imagine. It has some helpful methods like `between()`. For example, if you need to find the number of years between two dates:
````java
ChronoUnit.YEARS.between(date1, date2):
````
