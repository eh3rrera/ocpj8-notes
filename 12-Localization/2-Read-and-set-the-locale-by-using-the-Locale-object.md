#Read and set the locale by using the Locale object
Here's the [javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) for the Locale class.

The four ways to create a Locale object are:
* `Locale.Builder` Class
  
  For example:
  ````java
  Locale loc = new Locale.Builder().setLanguage("fr").setRegion("FR").build();
  ````
* Locale Constructors

  There are three constructors available in the Locale class:
  * `Locale(String language)`
  * `Locale(String language, String country)`
  * `Locale(String language, String country, String variant)`
  
  For example:
  ````java
  Locale l1 = new Locale("es", "ES");
  Locale l2 = new Locale("en");
  ````
* `Locale.forLanguageTag` Factory Method

  For example:
  ````java
  Locale loc = Locale.forLanguageTag("ja-JP");
  ````
* Locale Constants

  For example:
  ````java
  Locale loc1 = Locale.ITALIAN;
  Locale loc2 = Locale.CHINA;
  ````

To find out which types of *Locale* definitions a locale-sensitive class recognizes, you invoke the `getAvailableLocales()` method. For example, to find out which *Locale* definitions are supported by the *NumberFormat* class:
````java
public class Test {
    static public void main(String[] args) {
        Locale locales[] = NumberFormat.getAvailableLocales();
        for (Locale l : locales) {
            System.out.println(l.toString());
        }
    }
}
````
The output can be something like this:
````
ms_MY
ar_QA
is_IS
fi_FI
pl
en_MT
````
If we change from`System.out.println(l.toString())` to `System.out.println(l.getDisplayName ())` the output would be:
````
Malay (Malaysia)
Arabic (Qatar)
Icelandic (Iceland)
Finnish (Finland)
Polish
English (Malta)
````

You can assign a different *Locale* to every locale-sensitive object in your program. However, locale-sensitive objects rely on the default *Locale* set by the Java Virtual Machine. You can use the `Locale.getDefault()` method to get it and the `Locale.setDefault(Locale)` to set it.
