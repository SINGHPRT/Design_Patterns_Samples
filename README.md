# Design Patterns Samples
Implementation of DESIGN PATTERNS in Java


# Design Patterns

History:
  Christopher Alexander was the first person who invented all the above Design Patterns in 1977.
  But later the Gang of Four - Design patterns, elements of reusable object-oriented software book was written by a group of four persons named as Erich Gamma, Richard Helm, Ralph Johnson and John Vlissides in 1995.
  That's why all the 23 Design Patterns are known as Gang of Four (GoF) Design Patterns.

"A software design pattern is a general reusable solution to a commonly occurring problem within a given context in software design" 
--- Wikipedia

Design patterns, as name suggest, are solutions for most commonly (and frequently) occurred problems while designing a software. These patterns are mostly “evolved” rather than “discovered”. A lot of learning, by lots of professional, have been summarized into these design patterns. None of these patterns force you anything in regard to implementation; they are just guidelines to solve a particular problem – in a particular way – in particular contexts. Code implementation is your responsibility.

# Advantage of design pattern:
They are reusable in multiple projects.
They provide the solutions that help to define the system architecture.
They capture the software engineering experiences.
They provide transparency to the design of an application.
They are well-proved and testified solutions since they have been built upon the knowledge and experience of expert software developers.
Design patterns don?t guarantee an absolute solution to a problem. They provide clarity to the system architecture and the possibility of building a better system.

# Types of patterns
1. Creational Design Patterns
2. Structural Design Patterns
3. Behavioral Design Patterns

# Creational Design Patterns
Creational patterns often used in place of direct instantiation with constructors. They make the creation process more adaptable and dynamic. In particular, they can provide a great deal of flexibility about which objects are created, how those objects are created, and how they are initialized.

# Structural Design Patterns
These design patterns show you how to glue different pieces of a system together in a flexible and extensible fashion. Structural patterns help you guarantee that when one of the parts changes, the entire structure does not need to change.

# Behavioral Design Patterns
A behavioral pattern abstracts an action you want to take from the object or class that takes the action. By changing the object or class, you can change the algorithm used, the objects affected, or the behavior, while still retaining the same basic interface for client classes.


## Creational Design Patterns
Default way of creating object is- new ClassName(parms...);

# Singleton
When an application wants to have one and only one instance of any class per JVM, in all possible scenarios without any exceptional condition.Singleton pattern restricts the instantiation of a class and ensures that only one instance of the class exists in the Java virtual machine. The singleton class must provide a global access point to get the instance of the class. Singleton pattern is used for logging, driver objects, caching and thread pool. Singleton design pattern is also used in other design patterns like Abstract Factory, Builder, Prototype, Facade etc.

## How to create Singleton:
To implement Singleton pattern, there are really many approaches but all of them have following common concepts:

  A private constructor to avoid instantiation of the class,

  A private static variable from the same class that's the only instance of the class.

  public static method that returns the instance of the class, this is the global access point for the outer world to get the instance of the class.
  
 * Enum as Singleton: This type of implementation employs the use of enum. Enum, as written in the java docs, provided implicit support for thread safety and only one instance is guaranteed. Java enum singleton is also a good way to have singleton with minimal effort.
	  public enum EnumSingleton {
	    INSTANCE;
	    public void someMethod(String param) {
		// some class member
	    }
	}

## Examples:
In-built Examples:

  java.lang.Runtime.getRuntime(): This method gives Runtime class that has only one instance in a JVM.

  java.lang.System.getSecurityManager(): This method returns a SecurityManager for the current platform. java.awt.Desktop.getDesktop()


Custom Examples

  Connection Pool class
  
  Persistence Manager class
  
  

  Singleton Class 
  -----------------
  
	  public final class LazySingleton {
	    private static volatile LazySingleton instance = null;

	    // private constructor
	    private LazySingleton() {
	    }

	    public static LazySingleton getInstance() {
		if (instance == null) {
		    synchronized (LazySingleton.class) {
			instance = new LazySingleton();
		    }
		}
		return instance;
	    }
	}
  
	  public class WPUserDao {

	    private static final Logger log = Logger.getLogger(WPUserDao.class.getName());
	    private static final WPUserDao wpUserDao = new WPUserDao();

	    // private constructor
	    private WPUserDao() {
	    }

	    public static WPUserDao getInstance() {
	      return wpUserDao;
	    }

	    public WPUser findById(Long id) {
	      //code here...
	     }
	  }
  
  
  Client Program Code
  -------------------
  
	WPUser primaryMember = WPUserDao.getInstance().findById(Long.parseLong(userId));
	
  


## Advantages
Merit of this pattern is to have minimal instance creation process which is much costly than cloning process.
One instance per Application instance or JVM.

## Disadvantages
can't think of any.

# Builder
This is an alternative way to construct complex objects and should be used only when you want to build different immutable objects using same object building process.

## Examples:
In-built JDK Implementation:

  All implementations of java.lang.Appendable are infact good example of use of Builder pattern in java. e.g.
  
  java.lang.StringBuilder#append() [Unsynchronized class]

  java.lang.StringBuffer#append() [Synchronized class]

  java.nio.ByteBuffer#put() (also on CharBuffer, ShortBuffer, IntBuffer, LongBuffer, FloatBuffer and DoubleBuffer)


Custom Examples

Builder Class:
---------------


      public class Document implements Serializable {

        private static final long serialVersionUID = 309382038422977263L;

        private final Map<String, List<Field>> fieldMap;
        private final List<Field> fields;


        /**
         * A builder of documents. This is not thread-safe.
         */
        public static class Builder {
          private final Map<String, List<Field>> fieldMap = new HashMap<>();
          private final List<Field> fields = new ArrayList<>();

          /**
           * Constructs a builder for a document.
           */
          protected Builder() {

          }

          /**
           * Adds the field builder to the document builder. Allows multiple
           * fields with the same name.
           *
           * @param builder the builder of the field to add
           * @return this document builder
           */
          public Builder addField(Field.Builder builder) {
            return addField(builder.build());
          }

          /**
           * Adds the field to the builder. Allows multiple fields with the same name, except
           * that documents may only have one date and one number field for a name.
           *
           * @param field the field to add
           * @return this builder
           * @throws IllegalArgumentException if the field is invalid
           */
          public Builder addField(Field field) {
            Field.FieldType type = field.getType();
            if (type == Field.FieldType.DATE || type == Field.FieldType.NUMBER
                || type == Field.FieldType.VECTOR) {
              if (!noRepeatNames.put(field.getName(), type)) {
                if (type == Field.FieldType.VECTOR) {
                  throw new IllegalArgumentException("Vector fields cannot be repeated.");
                } else {
                  throw new IllegalArgumentException("Number and date fields cannot be repeated.");
                }
              }
            }

            fields.add(field);
            List<Field> fieldsForName = fieldMap.get(field.getName());
            if (fieldsForName == null) {
              fieldsForName = new ArrayList<>();
              fieldMap.put(field.getName(), fieldsForName);
            }
            fieldsForName.add(field);
            return this;
          }


          /**
           * Builds a valid document. The builder must have set a valid document
           * id, and have a non-empty set of valid fields.
           *
           * @return the document built by this builder
           * @throws IllegalArgumentException if the document built is not valid
           */
          public Document build() {
            return new Document(this);
          }
        }


        /**
         * Constructs a document with the given builder.
         *
         * @param builder the builder capable of building a document
         */
        protected Document(Builder builder) {
          fieldMap = new HashMap<>(builder.fieldMap);
          fields = Collections.unmodifiableList(builder.fields);
        }

        /**
         * Returns an iterable of {@link Field} in the document
         */
        public Iterable<Field> getFields() {
          return fields;
        }

        /**
         * Returns an iterable of all fields with the given name.
         *
         * @param name the name of the field whose values are to be returned
         * @return an unmodifiable {@link Iterable} of {@link Field} with the given name
         * or {@code null}
         */
        public Iterable<Field> getFields(String name) {
          List<Field> fieldsForName = fieldMap.get(name);
          if (fieldsForName == null) {
            return null;
          }
          return Collections.unmodifiableList(fieldsForName);
        }

        /**
         * Creates a new document builder. You must use this method to obtain a new
         * builder. The returned builder must be used to specify all properties of
         * the document. To obtain the document call the {@link Builder#build()}
         * method on the returned builder.
         *
         * @return a builder which constructs a document object
         */
        public static Builder newBuilder() {
          return new Builder();
        }

        /**
         * Creates a new document builder from the given document. All document
         * properties are copied to the returned builder.
         *
         * @param document the document protocol buffer to build a document object
         * from
         * @return the document builder initialized from a document protocol buffer
         */
        static Builder newBuilder(DocumentPb.Document document) {
          Document.Builder docBuilder = Document.newBuilder().setId(document.getId());

          for (DocumentPb.Field field : document.getFieldList()) {
            docBuilder.addField(Field.newBuilder(field));
          }

          return docBuilder;
        }
      }


Client Program:
---------------

      Document document = Document.newBuilder().setId("document id")
              .setLocale(Locale.UK)
              .addField(Field.newBuilder()
                  .setName("subject")
                  .setText("going for dinner"))
              .addField(Field.newBuilder()
                  .setName("body")
                  .setHTML("&lt;html&gt;I found a restaurant.&lt;/html&gt;"))
              .addField(Field.newBuilder()
                  .setName("signature")
                  .setText("ten post jest przeznaczony dla odbiorcy")
                  .setLocale(new Locale("pl")))
              .addFacet(Facet.withAtom("tag", "food"))
              .addFacet(Facet.withNumber("priority", 5.0))
              .build();

 

## Advantages
Undoubtedly, the number of lines of code increase at least to double in builder pattern, but the effort pays off in terms of design flexibility and much more readable code. The parameters to the constructor are reduced and are provided in highly readable method calls.
Builder pattern also helps minimizing the number of parameters in constructor and thus there is no need to pass in null for optional parameters to the constructor.

Another advantage is that Object is always instantiated in a complete state rather than sitting in an incomplete state until the developer calls (if ever calls) the appropriate “setter” method to set additional fields.

And I finally I can build immutable objects without much complex logic in object building process.

## Disadvantages
The client code is more verbose.


# Prototype
A prototype is a template of any object before the actual object is constructed. In java also, it holds the same meaning. Prototype design pattern is used in scenarios where application needs to create a number of instances of a class, which has almost same state or differs very little.

In this design pattern, an instance of actual object (i.e. prototype) is created on starting, and thereafter whenever a new instance is required, this prototype is cloned to have another instance. The main advantage of this pattern is to have minimal instance creation process which is much costly than cloning process.
Lets understand this pattern using an example. I am creating an entertainment application that will require instances of Movie, Album and Show classes very frequently. I do not want to create their instances everytime as it is costly. So, I will create their prototype instances, and everytime when i will need a new instance, I will just clone the prototype.

## Examples:
In-built Examples:

Custom Examples

## Advantages

## Disadvantages


# Factory
This is most suitable where there is some complex object creation steps are involved. To ensure that these steps are centralized and not exposed to composing classes, factory pattern should be used. We may not always know what kind of objects we want to create in advance.
Some objects can be created only at execution time after a user requests so.
A Factory Pattern or Factory Method Pattern says that just define an interface or abstract class for creating an object but let the subclasses decide which class to instantiate. In other words, subclasses are responsible to create the instance of the class.
Factory pattern introduces loose coupling between classes which is the most important principle one should consider and apply while designing the application architecture. Loose coupling can be introduced in application architecture by programming against abstract entities rather than concrete implementations. This not only makes our architecture more flexible but also less fragile.
The Factory Method Pattern is also known as Virtual Constructor.

Factory pattern is most suitable where there is some complex object creation steps are involved. To ensure that these steps are centralized and not exposed to composing classes, factory pattern should be used.

Examples when you may use a factory method:

A user may click on a certain button that creates an object.
A user may create several new documents of different types.
If a user starts a webbrowser, the browser does not know in advance how many tabs (where every tab is an object) will be opened.

## Examples:

In-built Examples:

java.util.Calendar, ResourceBundle and NumberFormat getInstance() methods uses Factory pattern.

valueOf() method in wrapper classes like Boolean, Integer etc.

java.sql.DriverManager#getConnection()

java.net.URL#openConnection()

java.lang.Class#newInstance()

java.lang.Class#forName()

java.util.logging.logger class



Custom Examples

Example 1:
==========
Calculate Electricity Bill : A Real World Example of Factory Method
Step 1: Create a Plan abstract class.

    import java.io.*;      
    abstract class Plan{  
             protected double rate;  
             abstract void getRate();  

             public void calculateBill(int units){  
                  System.out.println(units*rate);  
              }  
    }//end of Plan class.  

Step 2: Create the concrete classes that extends Plan abstract class.

    class  DomesticPlan extends Plan{  
            //@override  
             public void getRate(){  
                 rate=3.50;              
            }  
       }//end of DomesticPlan class.  
    class  CommercialPlan extends Plan{  
       //@override   
        public void getRate(){   
            rate=7.50;  
       }   
    /end of CommercialPlan class.  

    class  InstitutionalPlan extends Plan{  
       //@override  
        public void getRate(){   
            rate=5.50;  
       }   
    /end of InstitutionalPlan class.  

Step 3: Create a GetPlanFactory to generate object of concrete classes based on given information..

    class GetPlanFactory{  
    
     //use getPlan method to get object of type Plan   
         public Plan getPlan(String planType){  
              if(planType == null){  
               return null;  
              }  
            if(planType.equalsIgnoreCase("DOMESTICPLAN")) {  
                   return new DomesticPlan();  
                 }   
             else if(planType.equalsIgnoreCase("COMMERCIALPLAN")){  
                  return new CommercialPlan();  
              }   
            else if(planType.equalsIgnoreCase("INSTITUTIONALPLAN")) {  
                  return new InstitutionalPlan();  
            }  
        return null;  
     }  
  }//end of GetPlanFactory class.  


Step 4: Generate Bill by using the GetPlanFactory to get the object of concrete classes by passing an information such as type of plan DOMESTICPLAN or COMMERCIALPLAN or INSTITUTIONALPLAN.

    import java.io.*;    
    class GenerateBill{  
        public static void main(String args[])throws IOException{  
          GetPlanFactory planFactory = new GetPlanFactory();  

      System.out.print("Enter the name of plan for which the bill will be generated: ");  
      BufferedReader br=new BufferedReader(new InputStreamReader(System.in));  
  
      String planName=br.readLine();  
      System.out.print("Enter the number of units for bill will be calculated: ");  
      int units=Integer.parseInt(br.readLine());  
  
      Plan p = planFactory.getPlan(planName);  
      //call getRate() method and calculateBill()method of DomesticPaln.  
  
       System.out.print("Bill amount for "+planName+" of  "+units+" units is: ");  
           p.getRate();  
           p.calculateBill(units);  
            }  
    }//end of GenerateBill class.  
    
    
  Example 2:
  ==========


Abstract Super Class:
----------------------

    package com.journaldev.design.model;

    public abstract class Computer {

      public abstract String getRAM();
      public abstract String getHDD();
      public abstract String getCPU();

      @Override
      public String toString(){
        return "RAM= "+this.getRAM()+", HDD="+this.getHDD()+", CPU="+this.getCPU();
      }
    }



Sub Classes:
------------

    package com.journaldev.design.model;

    public class PC extends Computer {

      private String ram;
      private String hdd;
      private String cpu;

      public PC(String ram, String hdd, String cpu){
        this.ram=ram;
        this.hdd=hdd;
        this.cpu=cpu;
      }
      @Override
      public String getRAM() {
        return this.ram;
      }

      @Override
      public String getHDD() {
        return this.hdd;
      }

      @Override
      public String getCPU() {
        return this.cpu;
      }

    }


    package com.journaldev.design.model;

    public class Server extends Computer {

      private String ram;
      private String hdd;
      private String cpu;

      public Server(String ram, String hdd, String cpu){
        this.ram=ram;
        this.hdd=hdd;
        this.cpu=cpu;
      }
      @Override
      public String getRAM() {
        return this.ram;
      }

      @Override
      public String getHDD() {
        return this.hdd;
      }

      @Override
      public String getCPU() {
        return this.cpu;
      }

    }



Factory Class:
---------------

    package com.journaldev.design.factory;

    import com.journaldev.design.model.Computer;
    import com.journaldev.design.model.PC;
    import com.journaldev.design.model.Server;

    public class ComputerFactory {

      public static Computer getComputer(String type, String ram, String hdd, String cpu){
        if("PC".equalsIgnoreCase(type)) return new PC(ram, hdd, cpu);
        else if("Server".equalsIgnoreCase(type)) return new Server(ram, hdd, cpu);

        return null;
      }
    }


Client program/composing Class:
---------------------------------

    package com.journaldev.design.test;

    import com.journaldev.design.factory.ComputerFactory;
    import com.journaldev.design.model.Computer;

    public class TestFactory {

      public static void main(String[] args) {
        Computer pc = ComputerFactory.getComputer("pc","2 GB","500 GB","2.4 GHz");
        Computer server = ComputerFactory.getComputer("server","16 GB","1 TB","2.9 GHz");
        System.out.println("Factory PC Config::"+pc);
        System.out.println("Factory Server Config::"+server);
      }

    }



## Advantages
1. The creation of an object precludes its reuse without significant duplication of code.
2. The creation of an object requires access to information or resources that should not be contained within the composing class.
3. The lifetime management of the generated objects must be centralized to ensure a consistent behavior within the application.
4. Factory design pattern provides approach to code for interface rather than implementation.
5. Factory pattern removes the instantiation of actual implementation classes from client code. Factory pattern makes our code more robust, less coupled and easy to extend. For example, we can easily change PC class implementation because client program is unaware of this.
6. Factory pattern provides abstraction between implementation and client classes through inheritance.
7. Hence promotes Loose coupling.

## Disadvantages



# Abstract factory
Whenever you need another level of abstraction over a group of factories, you should consider using abstract factory pattern.

## Examples:
In-built Examples:

Custom Examples

## Advantages

## Disadvantages

************** WORK IN PROGRES ****************
















References:
1. https://howtodoinjava.com/gang-of-four-java-design-patterns/
2. https://github.com/sdmg15/Java-design-patterns
3. https://www.javatpoint.com/design-patterns-in-java
4. https://www.journaldev.com/1392/factory-design-pattern-in-java
