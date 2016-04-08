#Build a resource bundle for each locale and load a resource bundle in an application

[java.util.ResourceBundle](http://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html) class is used to store texts in key/pair values and components that are locale sensitive.

Resource bundles can share a common base name, but names can also have additional components that identify their locales. For example, if the base name of resource bundles is "MyBundle", we can have a "MyBundle_en" for the English locale and "MyBundle_es" for a Spanish locale. We can even have different resources for different countries, for example, "MyBundle_fr_CA" for Canadian French:
````
MyBundle.properties
MyBundle_en.properties
MyBundle_es.properties
MyBundle_fr_CA.properties
````
These files should be located in the same directory. If no locale is found for a resource bundle, the default bundle ("MyBundle.properties") will be used.

To load the resource bundle MyBundle.properties for an English locale, we use the following code:
````java
Locale locale = new Locale("en", "US");
ResourceBundle rb = ResourceBundle.getBundle("MyBundle", locale);
System.out.println(rb.getString("label"));
````

Although we only use the *ResourceBundle* class, it actually has two subclasses,  *PropertyResourceBundle* and *ListResourceBundle*. 

The *PropertyResourceBundle* class stores localized texts in standard Java property files.

The *ListResourceBundle* class uses classes to contain the resources. Using classes, you can use more than just *String* values.

Here's an example implementation:
````java
public class MyBundle_en extends ListResourceBundle {

    @Override
    protected Object[][] getContents() {
        return labels;
    }

    private Object[][] labels = {
            { "value1"   , new Integer(100) },
            { "label1", "MILES" },
    };
}
````

To get an object value, we use `rb.getObject(key)` or `rb.getStringArray(key)` (which is just a shortcut to `(String[])getObject(key)`) instead of `rb.getString(key)`

You can also obtain a set of all the keys contained in the *ResourceBundle* by using:
````java
Set<String> keys = rb.keySet();
````
