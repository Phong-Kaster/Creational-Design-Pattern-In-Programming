<h1 align="center">Cretional Design Pattern in Programming<br/>
    An exhaustive document describes creation design pattern 
</h1>

<p align="center">
    <img src="./photo/cover.jpg" width="1280" />
</p>


# [**Table Of Content**](#table-of-content)
- [**Table Of Content**](#table-of-content)
- [**Introduce**](#introduce)
- [**What is Creational Design Pattern ?**](#what-is-creational-design-pattern-)
- [**Creational - Factory Method**](#creational---factory-method)
- [**Creational - Abstract Method**](#creational---abstract-method)
- [**Creational - Singleton**](#creational---singleton)
- [**Creational - Builder**](#creational---builder)
- [**Creational - Prototype**](#creational---prototype)
- [**My Mentors**](#my-mentors)
- [**Credit**](#credit)
- [**Made with 💘 and English  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/English_language.svg/2560px-English_language.svg.png" width="60">**](#made-with--and-english--)

# [**Introduce**](#introduce)

This is my series repository about design pattern in programming. There are 4 repository in my series. They comprise:

- [**Overview**](https://github.com/Phong-Kaster/Design-Pattern-In-Programming)

- **Creational**(current)

- [**Structural**](#)

- [**Behavioural**](#)

You are reading the second episode of the series. The repository will describe everything you have to know about creational design pattern. For more information, continue reading the rest of the repository.

# [**What is Creational Design Pattern ?**](#creational)

<p align="center">
    <img src="./photo/creational.png" width="640" />
</p>
<h3 align="center">

***CREATIONAL PATTERN INCLUDES 5 SAMPLES***
</h3>

Creational pattern comprise 5 prototypes: 

1. Factory Method

2. Abstract Method

3. Singleton

4. Builder

5. Prototype


Instead of creating an object with `new` method, creational pattern provides a solution to instantiate an object & hide the logical way to create it. This way makes an application more flexible when it determines which objects will be created depend on what situation happens.

These patterns are used for instantiation of classes. They are concerned with the way of creating objects. Normally object creation happens in the below way by using the new keyword.

    Student myStudent = new Student();

The above code is more than enough for object instantiation, but in some cases `the object must be changed according to the nature of the program in runtime`, in such cases, creational design patterns will be useful.

# [**Creational - Factory Method**](#creational---factory-method)

- Fluency of use: ⭐ ⭐ ⭐ ⭐ ⭐ 

[**1. Definition**](#)

Factory Method is a creational design pattern that Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

Factory Method is a factory explicitly. This "factory" manufactures objects which we need only.

In Factory Method, it consist of 3 basic components:

1. Super Class: a super class could be interface, abstract & normal class.

2. Sub Class: classes which implements all methods from super class according to its own business.

3. Factory Class: a class is in charge of instantiate subclass's objects basing on passed parameters.

>Note: Factory class could be `Singleton` or any class providing a `public static` method for querying or creating an objects. It is said that factory uses `if-else` or `switch-case` so as to decide output subclass.

[**2. Example**](#)

We own a Mobile Money application for mobile device(Momo, Zalo and so forth). There are many financial organizations as ARGIBANK, BIDV, VIETCOMBANK,.... They are able to supply us a restfulAPI to use their services. The point in this scenario is how we don't need to change our core source code to use their restfulAPI if we want to cope with other businesses..... The answer for the problem is taking advantage of `Factory Method`


<p align="center">
    <img src="./photo/factory-example.png" width="640" />
</p>
<h3 align="center">

***WE DON'T WANT TO MODIFY / EXTEND CODE FOR EACH BANKS WE INCORPORATE? FACTORY METHOD IS THE KEY TO ADDRESS***
</h3>

First, create super class:

    public interface Bank{

        String getName();
        String getAddress();

        #do what you want
    }

Second, create 2 subclass which implements `Bank` interface 

- TPBank Class:
  
        package com.gpcoder.patterns.creational.factorymethod;
 
        public class TPBank implements Bank {
 
            @Override
            public String getName() {
                return "TPBank - A deeper understanding";
            }
 
            @Override
            public String getAddress()
            {
                return "49 Mac Dinh Chi, District 1, TP.HCM, Vietnam"
            }

            # any method/ functions are able to declare below.
        }

- Vietcombank Class

        package com.gpcoder.patterns.creational.factorymethod;
 
        public class Vietcombank implements Bank {
 
            @Override
            public String getName() {
                return "Vietcombank - Together for the future";
            }

            @Override
            public String getAddress()
            {
                return "125 Oktoberfest, District Deutschland, Berlin, Germany"
            }

            # any method/ functions are able to declare below.
        }

Third, instantiating `enum BankName`, the enum stores constant through our application. To manage easier with our customers, `ENUM` is chosen to store banks name.

        public enum BankName{

            # you can add more bank name if needed
            TPBANK, VIETCOMBANK
            BIDV, AGRIBANK,
            LienVietPostBank;

        }

Fourth, creating Factory Method. In this example, it is called `BankFactory`.

        public class BankFactory {
 

            # Constructor
            private BankFactory() {
            }
        


            # "getBank" method create an instance depending on @parameter BankName
            public static final Bank getBank(BankName bankName) {
                switch (bankName) {
        
                case TPBANK:
                    return new TPBank();
        
                case VIETCOMBANK:
                    return new Vietcombank();

                default:
                    throw new IllegalArgumentException("This bank is unsupported");
                }
            }
        
        }
Final, call `BankFactory` in our application"

    public class Client {
 
        public static void main(String[] args) {

            Bank bank = BankFactory.getBank(BankType.Vietcombank);

            String name = bank.getName();
            String address = bank.getAddress();


            System.out.println("One of our customer is " + content);
            System.out.println("Their headquarter is in " + address);
        }
    }

The output is absolutely as

    One of our customer is Vietcombank - Together for the future

    Their headquarter is in 125 Oktoberfest, District Deutschland, Berlin, Germany

# [**Creational - Abstract Method**](#creational---abstract-method)

- Fluency of use: ⭐ ⭐ ⭐ ⭐ 

[**1. Definition**](#)

Abstract Factory is a creational design pattern that provide an interface for creating families of  related or dependent objects without specifying their concrete classes.

>From my point of view, an Abstract (Factory) Method is a Factory method whose ability is to create a Factory Method.

Abstract Factory is the way to create a Super Factory. A `Super Factory` is eligible for creating a [**Factory Method**](#creational---factory-method)

In other word, Abstract Factory is a higher level of Factory Method. You could assume that Abstract Factory is an enormous factory. The enormous(Abstract Factory) factory comprises a number of small factory. Each small factory(Factory Method) specializes its own business.

A standard Abstract (Factory) Method embraces 5 components:

- **Abstract (Factory) Method** - it is defined `Interface` or `Abstract` class. They consists methods creating Abstract objects. To answer question: What does Abstract Method embrace ?

- **Abstract Product** - it is declared as `Interface` or `Abstract` class so as to define Abstract objects. To answer question: what activity **Abstract (Factory) Method's element** do ?

- **Concrete Factory** - building, instantiating methods which is used to create specific objects. To answer question: What do they need to begin run ?

- **Product** - Install of specific objects & write coding-flow for **Abstract Product's methods**. To answer question: How do they do ?

- **Client** - The objects uses **Abstract Factory** & **Abstract Product**.

[**2. Example**](#)

You are the chairman of GeoComply group - a furniture manufacturer. Your business supplies Table & Chair which is made from Wood or Plastic. However, manufacturing Wood furnitures & Plastic furnitures is 100% different . Therefore, you need 2 different factories to create them. Your customers can make orders which include both wood & plastic furnitures. Both of 2 factories will make process to fulfill your customers's order.   

<p align="center">
    <img src="./photo/abstract-method-sample.png" width="640" />
</p>
<h3 align="center">

***A BUSINESS HAS 2 FACTORY SPECIALIZED FOR EACH MATERIALS***
</h3>


First, using `ENUM` to store constants:

    public enum  Material{

        # add more types of material if you want
        PLASTIC, WOOD;

    }


Second, declaring **Abstract (Factory) Method**, it will be called Furniture Factory:

    public class FurnitureFactory {
 
        # constructor
        private FurnitureFactory() {
    
        }
    

        public static FurnitureAbstractFactory getFactory(Material material) {
            switch (materialType) 
            {
                case PLASTIC:
                    return new PlasticFactory();

                case WOOD:
                    return new WoodFactory();

                default:
                    throw new UnsupportedOperationException("This material is unsupported ");
            }
        }
    }

Third, creating **Abstract Factory**. This is `Abstract` class which defines what activities that WoodFactory & PlasticFactory do. ManufactureChair() and manufactureTable(), for instance.

    public abstract class FurnitureAbstractFactory{

        public abstract Chair manufactureChair();

        public abstract Table manufactureTable();
    }

>Note: Don't forget to declare `Chair` class & `Table` class into a Model folder.

Fourth, **Concrete Factory** determines what factories need to begin operating

- Plastic Factory:

        public class PlasticFactory extends FurnitureAbstractFactory {

            # what does PlasticFactory need to manufacture a Plastic Chair?
            @Override
            public Chair manufactureChair() {
                return new PlasticChair();
            }
 
            # what does PlasticFactory need to manufacture a Plastic Table?
            @Override
            public Table manufactureTable() {
                return new PlasticTable();
            }
        }

- Wood Factory:

        public class WoodFactory extends FurnitureAbstractFactory {
 
            @Override
            public Chair manufactureChair() {
                return new WoodChair();
            }
 
            @Override
            public Table manufactureTable() {
                return new WoodTable();
            }
        }

Fifth, **Abstract Product** tell us what actions we could do with a `Chair` & `Table`

- Chair:

        public interface Chair(){
            
            void create();
        }
- Table:

        public interface Table(){
            
            void create();
        }
Sixth, Depending on what material is used to make them. We have to write code for each Factory with its own business.


1. Plastic Factory 
- Chair
  
        public class PlasticChair implements Chair{


            @Override
            public void create(){
                System.out.println("Plastic chair is created !");
            }
        }

- Table

         public class PlasticTable implements Table{

            @Override
            public void create(){
                System.out.println("Plastic table is created !");
            }
        }
2. Wood Factory
- Chair
  
        public class WoodChair implements Chair {

            @Override
            public void create() {
                System.out.println("Wood chair is created !");
            }

        }
- Table

        public class WoodTable implements Table{
            @Override
            public void create(){
                System.out.println("Wood table is created !");
            }
        }

Finally, we are able to use **Furniture Factory** as:

        public static void main(String[] args){

            FurnitureAbstractFactory factory = FurnitureFactory.getFactory(MaterialType.WOOD);
 
                Chair chair = factory.manufactureChair();
                chair.create(); 
 
                Table table = factory.manufactureTable();
                table.create();
            }
        }

Output

        Wood chair is created !

        Wood table is created !

# [**Creational - Singleton**](#creational---singleton)

- Fluency of use: ⭐ ⭐ ⭐ ⭐ 

[**1. Definition**](#)

Scenario: Sometimes, in a system analysis, we desire having objects that exist only & could be given access from every where. How can we do this ? Maybe you have idea using a `public static final` variable. However, the use of it absolutely break one of 4 principles of OOP - Encapsulation. To prevent this happening, it's high time we used `Singleton`.

Singleton is a creational design pattern that lets you ensure that a class has only one instance and provide a global access point to this instance.

There are many possible ways to use Singleton yet they have something in common:

- `Private constructor` prevents accessing from other classes.

- `Private static final` variable guarantees it is only defined in its class.

- There is a `public static` method to return its instance from any other classes.

[**2. Implementation**](#)


[**2.1. Singleton - Eager Initialization**](#)

Singleton is created immediately when called. This is the simplest way yet it has a disadvantage that the instance isn't maybe used.

    public class EagerSingleton{
        
        # Private static final variable guarantees it is only defined in its class.
        private static final EagerSingle instance = new EagerSingle();


        # Private constructor prevents accessing from other classes.
        private EagerSingleton{

        }

        
        # the public static method returns its instance
        public static getInstance(){
            return this.instance;
        }

    }

Eager initialization is a good approach, easy to implement, however, it is easily broken by Reflection.

[**2.2. Singleton - Static Block Initialization**](#)

It is similar to `Eager Initialization` whereas Static Block Initialization created in a static block provides an option for exception handling.
 
    public class StaticBlockSingleton {
 
        # Private static final variable guarantees it is only defined in its class.
        private static final StaticBlockSingleton INSTANCE;
 

        # Private constructor prevents accessing from other classes.
        private StaticBlockSingleton() {
        }
 

        # Static block initialization for exception handling
        static {
            try 
            {
                INSTANCE = new StaticBlockSingleton();
            } 
            catch (Exception e) 
            {
                throw new RuntimeException("Exception occured in creating singleton instance");
            }
        }
 

        # the public static method returns its instance
        public static StaticBlockSingleton getInstance() {
         return INSTANCE;
        }
    }

[**2.3. Singleton - Lazy Initialization**](#)

Lazy Initialization expands from 2 implementations above & operates well with single-thread.

    public class LazySingleton {
        
        # Private static final variable guarantees it is only defined in its class.
        private static LazySingleton instance;
 

        # Private constructor prevents accessing from other classes.
        private LazySingleton() {
        }
 

        # the public static method returns its instance
        public static LazySingleton getInstance() {
            if (instance == null) {
                instance = new LazySingleton();
            }
            return instance;
        }
    }

The implementation of **Lazy Initialization** has overcome the disadvantage of Eager initialization, only when getInstance() is called will the instance be initialized. However, this method only works well in the case of single-thread. In case, there are many threads (multi-thread) running and calling getInstance() at the same time, there can be many more than 1 instance of the instance. To overcome this drawback we use Thread Safe Singleton.


[**2.4. Singleton - Thread Safe Singleton**](#)

The easiest way is `calling synchronized method with getInstance()` & then system would guarantee that only one thread can give access to getInstance() at the same time.


    public class ThreadSafeSingleton {
 
        private static volatile ThreadSafeSingleton instance;
 

        # Private constructor prevents accessing from other classes.
        private ThreadSafeSingleton() {
        }
 

        # the public static method returns its instance
        public static synchronized ThreadSafeSingleton getInstance() {
            if (instance == null) 
            {
                instance = new ThreadSafeSingleton();
            }
            return instance;
        }
    }

>Note: the key "volatile" in JAVA notifies instance's changes to other threads if the instance is being using by many threads.

The disadvantage of Thread Safe Singleton is sluggish & requiring many resources. Any thread calls this instance then they have to wait for running thread finishes. Hence, we can improve it by `Double Check Locking Singleton`.

[**2.5. Singleton - Double Check Locking Singleton**](#)

        public class DoubleCheckLockingSingleton {
 
            private static volatile DoubleCheckLockingSingleton instance;
 
            private DoubleCheckLockingSingleton() {
            }
 
            public static DoubleCheckLockingSingleton getInstance() {
                if (instance == null) 
                {

                    # Do the task too long before create instance ...
                    # Block so other threads cannot come into while initialize
                    synchronized (DoubleCheckLockingSingleton.class) {
                        // Re-check again. Maybe another thread has initialized before
                        if (instance == null) 
                        {
                            instance = new DoubleCheckLockingSingleton();
                        }
                    }

                }
                return instance;
            }
        }

>Note: the key "volatile" in JAVA notifies instance's changes to other threads if the instance is being using by many threads.

[**2.6. Singleton - Bill Pugh Singleton Implementation**](#)

[**2.7. Singleton - Using Reflection to destroy Singleton Pattern**](#)

[**2.8. Singleton - Enum**](#)

When using enum, the params are only initialized once, this is also a way to help you create a Singleton instance.

    public enum BANK{
        
        BIDV, ARGIBRANK, VIETCOMBANK;
    }

Disadvantage of Enum:

- Enum can be used as Singleton but it is unable to extend from other classes.

- The enum constructor is lazy initialization, which means that when used, the constructor runs and it only runs once. If you want to use it as an eager singleton, you need to call the execution in a static block when starting the program.

# [**Creational - Builder**](#creational---builder)

- Fluency of use: ⭐ ⭐ 

[**1. Definition**](#)

Builder is a creational design pattern that separate the construction of a complex object from its representation so that the same construction process can create different representations.

Builder pattern is an object design pattern created to build a complex object using simple objects and using a step-by-step approach, building objects independently of other objects.

Builder pattern is built to overcome some disadvantages of [**Factory Method**](#creational---factory-method) & [**Abstract (Factory) Method**](#creational---abstract-method) when objects have too many properties.

- Client side has to pass many parameters to Factory Method.

- Some parameters are optional but we have to pass all of them when using Factory Method. With an optional parameter, if nothing is entered, it will pass as null.

- If an object has too many properties, it'll be complex.

A Builder pattern includes these basic components below:

- **Product** represents for the objects be created, this object is complex & has many properties.

- **Builder** is an abstract class or interface. It defines method creating the objects.

- **ConcreteBuilder** inherits Builder and implements detailed object creation. It identifies and holds the instances it creates, and it also provides a method to return the instances it has previously created.
   
- **Client** is the class calls Builder to create objects.

[**2. When do we need to use Builder**](#)

1. To create complex object having many properties(greater than 4). Some properties are mandatory & some others are optional.
2. Too many constructors
3. To diversify ways to create an object.s

[**3. Example**](#)

[**3.1 A Standard Builder Example**](#)

Example: 

We assumes that we has a FastFood restaurant. In our menu, we provide a menu meal for children. Children's meal typically consist of a main item, a soft drink, a toy. Note that there can be variation in the content of the children's meal, but the construction process is the same. Whether a customer orders a hamburger, cheeseburger, or chicken, the process is the same. The employee at the counter directs the crew to assemble a main item, side item, and toy. These items are then placed in a bag. The drink is placed in a cup and remains outside of the bag. This process operates in every FastFood restaurant.

<p align="center">
    <img src="./photo/builder-sample.png" width="640" />
</p>
<h3 align="center">

***We can choose whatever we want to assemble a child's meal***
</h3>


The key to answer this question is building a `Builder` to create optional meal.

First, declaring ENUM for storing meal options:

- Type

        public enum TYPE{

            ONSITE, TAKEAWAY;
        }
- Bread

        public enum BREAD{

            STANDARD, HAMBURGER, PORK, SAUSAGE, NONE;
        }

- Drink

        public enum DRINK{

            COCA-COLA, PEPSI, JUICE, NONE;
        }

Second, defining **Order** class:

    public class Order{

        # declare private variables
        private TYPE type;
        private BREAD bread;
        private DRINK drink;


        # constructor
        public Order(TYPE type, BREAD bread, DRINK drink){
            this.type = type;
            this.bread = bread;
            this.drink = drink;
        }


        # getter for each private variable
        ........


        # @Override
        public String toString() {

            return "Order Script \n 1. TYPE + " + type + 
            "\n 2. BREAD: " + bread + 
            "\n 3. DRINK: " + drink + "\n";
        }
    }

Third, defining `interface OrderBuilder` 

    public interface Builder{

        # TYPE's setter method
        Builder setType();

        # BREAK's setter method
        Builder setBread();

        # DRINK's setter method
        Builder setDrink();

        # this function helps us to combine different option to a complete meal
        Order assemble();

    }

Fourth, implement `OrderBuilder` and write detailed code for each methods which is defined in `interface Builder`:

    public class OrderBuilder implements Builder{

        private TYPE type = TYPE.ONSITE;
        private BREAD bread = TYPE.NONE;
        private DRINK drink = TYPE.NONE;


        @Override
        public Builder setType(TYPE type){
            this.type = type;
            return this;
        }

        @Override
        public Builder setBread(BREAD bread){
            this.bread = bread;
            return this;
        }


        @Override
        public Builder setDrink(DRINK drink){
            this.drink = drink;
            return this;
        }
        

        @Override
        public Order assemble(){
            # declare a "order" object 
            Order order = new Order(this.type, this.bread, this.drink);

            # return the result;
            return order;
        }
    }

Fifth, the example below shows how to use a OrderBuilder:

    public class PhongKaster{

        public static void main(String[] args){
            
            # declare a Order instance
            Order myOrder = new OrderBuild();

            # choose favorite food
            myOrder.setType(TYPE.TAKEAWAY);
            myOrder.setBread(BREAK.HAMBURGER);
            --no drink to choose

            # print the result to the console
            System.out.println(order);
        }
    }

Output

    Order Script
    1. TYPE: TAKEAWAY
    2. BREAK: HAMBURGER
    3. DRINK: NONE


From the code example, we could make a conclusion that builder let us choose what components will be create & won't. With parameters isn't enter, we don't have to worry about it. This is the strongest advantage of Builder pattern.


[**3.2. Using Builder To Create An Immutable Object**](#)

What is an **Immutable Object** ? In object-oriented and functional programming, an immutable object is an object whose state cannot be modified after it is created & only provides getter() methods to retrieve its properties value.

There are some important point about objects using Builder:
- Its constructor is private which means others are unable to create it directly.
- All properties of it are `private final` so you just only get them, not set them value.
- Using Builder is the only way to create it.

Example:

    public class Facebook{
        
        # all properties is "private final"
        private final String name; // mandatory
        private final String email; // mandatory
        private final boolean twoLayeredVerification;
        private final String birthday;


        # private constructor
        private Facebook(String name, String email, boolean 2LayeredVerification, birthday){
            # code....
        }


        # the "FacebookBuilder" is Facebook's gateway to instantiate itself.
        public static class FacebookBuilder{


            # It has the same properties as Facebook class
            private String name;
            private String email;
            private boolean twoLayeredVerification;
            private String birthday;



            # public constructor FacebookBuilder
            public FacebookBuilder(String name, String email){
                this.name = name;
                this.email;
            }


            # method "enable Two-layered verification"
            public FacebookBuilder enableTwoLayeredVerification(boolean twoLayeredVerification){
                this.twoLayeredVerification = twoLayeredVerification;
                return this;
            }


            # method "set birthday"
            public FacebookBuilder setBirthday(String birthday){
                this.birthday = birthday;
                return this;
            }


            # method "build" to initialize Facebook object
            public Facebook build(){
                
                # Step 1 - verify mandatory fields
                if( name.length() < 1 || email.length() < 1 )
                    throws new IllegalArgumentException("Email can't be null when client want to receive the new letter");

                Facebook myFacebook = new Facebook(
                    this.name, this.email,
                    this.twoLayeredVerification,
                    this.birthday
                );

                # Step 2 - return the result
                return myFacebook;
            }


            # toString method to print on the console
            @Override
            public String toString() {
                #code...
            }
    }

Use of Facebook class:

    public class PhongKaster{

        public static void main(String[] args){
            
            # declare a Order instance
            Facebook newFacebook = new Facebook
                                        .FacebookBuilder("Phong Kaster", "phongkaster@gmail.com")
                                        .enableTwoLayeredVerification(false)
                                        .setBirthday("01-05-2000")
                                        .build();

            # print the result
            System.out.println(newFacebook);
        }
    }

Output:

    My Facebook:
    1. Name: Phong Kaster
    2. Email: phongkaster@gmail.com
    3. Enable Two Layered Verification: false
    4. Birthday: 01-05-2000

[**4. Disadvantage**](#)

The biggest disadvantage of `Builder` is duplicating code because the need of copying Object's properties(Facebook) to Object Builder(Facebook Builder).

# [**Creational - Prototype**](#creational---prototype)

- Fluency of use: ⭐ ⭐ ⭐

[**1. Definition**](#)

Prototype is a creational design pattern that specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

Scenario: Assume you have a `Hash Map` has 100 elements. Each element has a pair `key` & `value`. Now, for exhaustive testing, you are mandatory to replace fifthly element & ninetieth element by 2 other pair key & value. If we create a new hashmap and loop through the first hash map, it's effective. Why don't we duplicate the Hash Map and just replace 2 positions as we want ?

Prototype lets you produce new objects by copying existing ones without compromising their internals. The new object is an exact copy of the prototype but permits modification without altering the original.

<p align="center">
    <img src="./photo/prototype-sample.jpeg" width="640" />
</p>
<h3 align="center">

***PROTOTYPE IS A DUPLICATION OF SOMETHING !***
</h3>

Prototype pattern is used when to create a new object requires many efforts.

In JAVA, to duplicate an object, we have to implements `interface Cloneable` & use `clone()` method to do it.

[**2. Example**](#)

In GeoComply, every single staff will be given a Macbook Pro 16 2019. There is no different among staff's laptop. All of them has the same installed programs( MacOS, Slack, Skype,....). If someone need special programmes for their own business, they'll be installed later. Installation takes long times, however, IT support department comes up with an ideal that a standard Laptop version will be create and they install this version to every laptop in the company. It is called `clone()`

First, we defines `Computer` class implementing interface `Cloneable`:

    public class Computer implements Cloneable{

        private String operatingSystem;
        private String office;
        private String others;



        # constructor
        public Computer(String operatingSystem, String office, String others){
            this.operatingSystem = operatingSystem;
            this.office = office;
            this.others = others;
        }



        # clone() method from interface Cloneable
        @Override
        protected Computer clone() {
            try 
            {
                return (Computer) super.clone();
            } 
            catch (CloneNotSupportedException e) 
            {
                e.printStackTrace();
            }
            return null;
        }


        # getter() & setter()
        ....
    }

Second,  use of Computer:


    public static void main(String[] args) {

        Computer computer1 = new Computer("MacOS", "Word 2022", "Slack");
        Computer computer2 = computer1.clone();
        computer2.setOthers("Android Studio, Firefox");
 
        System.out.println("Computer 1 has " + computer1);
        System.out.println("Computer 2 has " + computer2);
    }

Output

        Computer 1 has MacOS, Word 2022, Slack;

        Computer 2 has MacOS, Word 2022, Android Studio, Firefox;

# [**My Mentors**](#my-mentors)

<table>
        <tr>
            <td align="center">
                <a href="#">
                    <img src="./photo/mentor.jpeg" width="100px;" alt=""/>
                    <br />
                    <sub><b>Nguyễn Đăng Phát</b></sub>
                </a>
            </td>
            <td align="center">
                <a href="#">
                    <img src="./photo/mentor-2.jpeg" width="100px;" alt=""/>
                    <br />
                    <sub><b>Nguyễn Phúc Thảo</b></sub>
                </a>
            </td>
        </tr>
</table>
 

# [**Credit**](#credit)

All examples about each design pattern, I referenced from [**here**](https://gpcoder.com/4164-gioi-thieu-design-patterns/#Nhom_Creational_nhom_khoi_tao)

# [**Made with 💘 and English  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/English_language.svg/2560px-English_language.svg.png" width="60">**](#made-with--and-english)