#Create and read a Properties file

Properties are files with string key/value pairs that store configuration data or settings:
````
# A comment
user=amtg
passw=changeme
language=java
````

To use them, you create instances of `java.util.Properties`. The following example, loads the file config.properties from project classpath and read its properties:
````java
public class Test {
  public static void main(String[] args) {
    	Properties prop = new Properties();
    	InputStream input = null;
 
    	try {
    		input = Test.class.getClassLoader().getResourceAsStream("config.properties");
    		//load the properties file from class path
    		prop.load(input);
 
        //get a property value and print it out
        System.out.println(prop.getProperty("user"));
        
        //get all properties
        Enumeration<?> e = prop.propertyNames();
    		while (e.hasMoreElements()) {
    			String key = (String) e.nextElement();
    			String value = prop.getProperty(key);
    			System.out.println("Key : " + key + ", Value : " + value);
    		}
 
    	} catch (IOException ex) {
    		ex.printStackTrace();
      } finally {
        	input.close();
			}
    }
}
````
