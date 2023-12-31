# Design patterns

Design patterns are well known solutions to recurring problems.

- This way there is no need to reinvent the wheel.
- Use best practices, lower cost and increase quality

## Characteristics

- Language neutral: use in any OOP language
- Dynamic: revise existing ones if needed
- Intentionally incomplete to allow customization

## Types

### Creational Patterns

- To build objects systematically
- Benefit of flexibility. Different object types from same class can be created at runtime
- This uses polymorphism often

### Structural Patters

- To establish relationships between software components
- Meet functional (what it does) and non-functional (how well does it do) requirements
- Different requirements lead to different structures
- This uses inheritance often

### Behavioral Patterns

- How the objects interact with each other
- Meet functional and non-functional requirements
- Focus is to define protocols between objects when working together to meet a requirement
- This heavily uses methods and their signatures

## Pattern Context

- Participants: The classes involved to form a design pattern
- Quality attributes: Non-functional requirements such as reliability and performance. This has an effect on the
  software and architectural solutions address them.
- Forces: Factors or trade-offs to consider. This is manifested in quality attributes and if not dealt with, could
  result in unintended consequences
- Consequences: E.g. Worse performance

## Patterns

<table>
  <tr>
    <th>Pattern</th>
    <th>Use cases</th>
    <th>Components</th>
  </tr>
  <tr>
    <td><strong>Factory</strong>: This is a creational pattern used to provide abstraction. Instead of client code 
directly creating objects, it delegates responsibility to a Factory Method e.g. ordering a combo meal at a restaurant.
      <ul>
        <li>Decoupling client code from concrete classes. Placing redundant code e.g. create burger into a class and 
calling it from multiple places would be 'Simple Factory', but then we would have to modify the class when new items 
need to be added, and also would need to know the class type e.g. CheeseBurger meal when calling.</li>
        <li>Flexibility of creation of object without specifying exact class</li>
        <li>Extensibility by adding new product classes</li>
      </ul>
    </td>
    <td>
    <ul>
      <li>Library Frameworks: It’s commonly used in library frameworks, allowing developers to extend and customize the behavior of a library.</li>
      <li>Plug-in Architectures: When building applications with extensible plug-in architectures, the Factory Method pattern simplifies the addition of new plug-ins without modifying existing code.</li>
      <li>Testing: Factories can be used to create mock objects for unit testing.</li>
    </ul>
    </td>
    <td>
      <ul>
        <li>Product Interface: Defines an abstract class or interface for the product. For example, Burger.</li>
        <li>Concrete Product: Implements concrete Products e.g. VeganBurger, CheeseBurger etc.</li>
        <li>Creator Interface: Defines an abstract creator class or interface that has a FactoryMethod e.g. getBurger() 
but without the implementation</li>
        <li>Concrete Creator: Implements the creator and FactoryMethod e.g. CheeseBurgerCreator</li>
      </ul>
      Now when a new Burger type is added, the FactoryMethod in Creator Interface doesn't change.
    </td>
  </tr>


  <tr>
    <td><strong>Singleton</strong>: This is a creational pattern and is used when you only want one instance of a class. 
For example if we want a shared state globally using objects or only one instance is needed e.g. logger.</td>
    <td>
      <ul>
        <li>Database Connection Pools: Enhancing database interaction efficiency via a unified connection pool.</li>
        <li>Logger Services: Centralizing application logging through a single logger instance.</li>
        <li>Configuration Management: Ensuring a solitary configuration manager instance oversees application settings.</li>
        <li>Hardware Access: Controlling access to hardware resources, such as a printer or sensor, through a single instance.</li>
      </ul>
    </td>
    <td>
    <ul>
      Singleton Class with:
      <li>A private static variable of its own type to hold the single instance</li>
      <li>A private constructor that restricts public instantiation from outside</li>
      <li>A public static method e.g. getInstance() that returns the unique instance</li>
    </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Builder</strong>: This is a creational pattern that solves situation of a telescoping constructor, which
occurs when a developer builds a complex object using an excessive number of constructors. For example create a meal 
object with drink, mains, dessert etc. It has some overlap with the Factory pattern in that it had high level view of say 
different kinds of meals. But in this case we could have large set of drinks, mains etc. Subclassing and making a new kind 
of meal for each variation would not be practical and we might want to have some granular control. Also, if there was a new 
course in the meal, then we would need to update the constructor. In this Builder pattern we will add what is needed, step by step.</td>
    <td>
      <ul>
        <li>Protocol Buffers - In data serialization, the Builder pattern is employed to construct complex data 
structures. Protocol buffers define structured data in a simpler, yet efficient way compared to XML or JSON. This enables 
step-by-step construction of objects, especially handy for nested data structures and handling optional or repeated fields.</li>
        <li>Meal Order Systems - Different meals might have different components (starters, mains, drinks, desserts) and preparation steps.</li>
        <li>Video Game Character Creation - The builder pattern is popular in the context of video games which allow 
crafting a custom character where a player can choose a character's weapons, armor, accessories, and abilities.</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>Abstract Builder: Class or interface needed to build a product</li>
        <li>Concrete Builders: Inherits from abstract builder and implements the details for each specific product</li>
        <li>Product: An object being built e.g. meal</li>
        <li>Director: Uses the builder to build a product</li>
      </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Adapter</strong>: This is a structural pattern that converts interface of a class to one that client is 
expecting. The purpose here is to take two classes and make them compatible. Lets say we have used a JSONLogger in our code 
everywhere, but now we want to use XMLLogger as well. It would be convenient if both logger had same interface. 
    <td>
      <ul>
        <li>Legacy System Integration: When you need to integrate a legacy system or library with modern code, the Adapter pattern can make the transition smoother. It allows you to wrap the legacy code with an adapter, ensuring it conforms to the expected interface of the new system.</li>
        <li>Third-Party Libraries: When working with third-party libraries or APIs that do not align with your system’s requirements, adapters can serve as intermediaries. They translate the third-party interface into one that your codebase understands.</li>
        <li>Interface Evolution: As your software evolves, you may encounter situations where the interfaces of existing classes need to change. Adapters can help maintain backward compatibility by presenting the old interface while internally implementing the new one.</li>
      </ul>
    </td>
    <td>
    Object Adapter takes on interface of one object while wrapping the behavior of other. Class Adapter relies on inheritance, inheriting interfaces form both objects, overriding methods, but only available in C++.
    <ul>
      <li>Target Interface: The target interface defines the contract that the client code expects. It is the interface the adapter will conform to, allowing the client to interact with the adaptee (XMLLogger) seamlessly.</li>
      <li>Adaptee: The adaptee is the class or component with an incompatible interface. It’s the object you want to make use of but cannot interact with directly from the client. Usually a 3rd party or legacy service.</li>
      <li>Adapter: The intermediary that bridges the gap between the target interface and the adaptee. It translates calls from the client in a way that the adaptee can understand and respond to.</li>
    </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Decorator</strong>: This is a structural pattern that add features to existing objects dynamically without 
changing structures. In Adapter pattern it was about compatibility, but about adding or changing behavior. Lets say 
there is a Beverage class, with many methods and attributes. Eventually this becomes a God class. Another approach is 
turnkey methods inherited like BeverageWithMilk class which has its own problems. Instead a Decorator is used. </td>
    <td>
      <ul>
        <li>Point of Sale Systems - As discussed in our example, point of sale systems can make use of the decorator 
design pattern to compute the cost of the overall purchase, with discounts and add-ons etc.</li>
        <li>Graphical User Interfaces - The decorator pattern is very common when adding visual or behavior functionalities 
to GUI components dynamically. For example, making a window scrollable, adding borders, colors and modifying fonts, 
etc all can be achieved through decorators.</li>
        <li>Middleware in Web Development - Implementing middleware to augment request and response objects in web 
frameworks by adding functionalities like authentication, authorization, logging and error handling.</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>Component (abstract class or interface): Lets say we have a Beverage abstract class.</li>
        <li>Concrete component: Implements the Abstract component. The methods here can be altered by decorators. A LightRoast and DarkRoast extends the 
Beverage class for two types of beans. </li>
        <li>Decorator (abstract class): An abstract class that extends the Abstract component. In our case lets say its called BeverageDecorator.</li>
        <li>Concrete Decorator: Implements the decorator. We can now have ExpressoDecorator, CreamDecorator, FoamDecorator 
that extend BeverageDecorator. Now ExpressoDecorator could wrap DarkRoast (to say add its cost) and CreamDecorator 
(add another $0.2) and FoamDecorator (add another $0.1)</li>
      </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Facade</strong>: This is a structural pattern that is a wrapper without a very clear purpose unlike Adapter 
or Decorator. Basically make it simple for clients to use called e.g. API design e.g. like GraphQl where you go through 
one endpoint and query for specific data you need, as opposed to REST where you request directly to a resource. E.g. in a 
SmartHome you can expose some presents like movie mode or focus mode as opposed to enabling setting temperature and lights.</td>
    <td>
      <ul>
        <li>API Wrappers - Many times, third-party libraries provide APIs that are very granular or complex. For example, 
X (formerly Twitter) provides a comprehensive API but it can be cumbersome, especially for those unfamiliar with 
intricacies of OAuth, endpoints structures. Tweepy is a python library, which acts as a facade, simplifying authentication and the process of sending tweets.</li>
        <li>GUI Libraries - Complex GUI libraries can have intricate setups for creating windows, shapes etc. A facade 
might be used to allow the developers to make simplified calls to abstract these details, allowing developers to create UI elements with simple method calls.</li>
        <li>Database Access using ORM - Instead of writing raw SQL queries, developers can use high-level methods to retrieve, insert or update records. 
For example, a piece of code like user = DB.get_record('users', 5) abstracts away the details of forming the SQL query, 
executing the query, fetching the result and handling potential errors.</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>SubSystem classes: The classes that the facade aims to simplify for the client. For example a SmartHomeSystem has intricate details like setBrightness() </li>
        <li>Facade: Serves as a gateway as a higher level interface, encapsulating complexities. For example a SmartHomeFacade that uses the SmartHomeSystem and maybe other systems as well</li>
      </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Strategy</strong>: This is a behavioral pattern that offers a family of algorithms/behaviors that can be 
extended and used to change behavior at runtime. Inheritance is good for sharing behaviors, but when there needs to be both 
shared and differing behaviors for say a method, we can use strategy pattern.</td>
    <td>
      <ul>
        <li>Payment Processing Systems - any system where users can choose to pay with credit card, PayPal, Bitcoin etc.</li>
        <li>Travel Routes - We can customize our routes when traveling. For example, we might choose a route without highways, the shortest route, or the fastest route. Each of these routes have different strategies.</li>
        <li>Shipping Options - Each shipping method has its own category and its own strategy for determining cost and delivery time.</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>Context (Navigator Class): Instead of determining the behaviors directly through conditions, it delegates the 
responsibility to Strategy. This allows the Context (e.g. Door) to change behavior dynamically. There could be Doors like SlidingDoor that extends the Door.</li>
        <li>Strategy Interface: Abstract class for all strategies. In general it could have some variation of execute() method. 
In our example it can be Lockable and Openable interface that can be used to define locking and opening door behaviors.</li>
        <li>Concrete strategy: Implements each strategy</li>
      </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Observer</strong>: This is a behavioral pattern that is about notifications. It establishes 1:many 
relationship between a subject and multiple observers. A subject needs to be monitored, and the observers need to be 
notified when there is a change in the subject. pub/sub would be a good example and a bad way to do this would be polling.</td>
    <td>
      <ul>
        <li>Home Automation Systems - In a smart home, various devices can act as observers. For instance, a temperature sensor might monitor room temperature. When the temperature crosses a certain threshold, the air conditioning system, an observer, gets activated automatically.</li>
        <li>Gaming - Achievement Systems - In many video games, players can earn achievements or trophies for completing specific tasks or challenges. The game can use the Observer pattern to monitor various game metrics or player actions. When a particular metric meets the criteria for an achievement, the corresponding observer triggers, granting the player the achievement.</li>
        <li>Subscription Services - Systems where users can subscribe to receive news, updates, or other information. When new content is available, all subscribed users (observers) receive a notification, such as an email or a push notification.</li>
        <li>Real-Time Data Monitoring - Applications that monitor real-time data, such as stock market applications, can use the Observer pattern. When the stock price changes, all subscribed clients (observers) are immediately notified and can update their displays or perform other actions.</li>
      </ul>
    </td>
    <td>
      <ul>
        <li>Subject (Publisher): abstract class that has interface that allows operations like attach/registerObserver, detach/removeObserver, notifyObservers</li>
        <li>Concrete Subject: Implements the Subject, manages list of observers and the data they are interested in.</li>
        <li>Observer (Interface/abstract class): This class has the update method that is used to inform observers.</li>
        <li>Concrete Observer: Implements the observer which has the reference to the Subject and registers itself. It implements the update method.</li>
      </ul>
    </td>
  </tr>


  <tr>
    <td><strong>Prototype</strong>: Useful when instantiating many identical objects could be expensive, instead clone them.</td>
    <td></td>
    <td><ul><li>Prototypical instance</li><li>Clone</li></ul></td>
  </tr>

  <tr>
    <td><strong>Proxy</strong>: To create a highly resource intensive object</td>
    <td><ul><li>Postpone object creation unless absolutely necessary</li><li>Find a placeholder</li></ul></td>
    <td><ul><li>Clients: wait to interact with a proxy</li><li>Proxy: Responsible for creating resource intensive Producer objects</li><li>Producer: resource intensive object</li></ul></td>
  </tr>

  <tr>
    <td><strong>Composite</strong>: Maintains a tree data structure to represent part whole relationships</td>
    <td></td>
    <td>Recursive data structure with elements having sub elements Menu &rarr; submenu &rarr; subsubmenu <ul><li>Component: Abstract class</li><li>Child: Concrete component class</li><li>Composite: Concrete component class with child objects</li></td>
  </tr>
  <tr>
    <td><strong>Bridge</strong>: Helps untangle unnecessarily complicated class hierarchy, especially when implementation classes are mixed with implementation independent classes</td>
    <td></td>
    <td>Implementation independent and dependant circle abstraction</td>
  </tr>

  <tr>
    <td><strong>Visitor</strong>: Allows adding new features to existing clas hierarchy without changing it.</td>
    <td></td>
    <td>
    <ul>
      <li>Visitor</li>
      <li>Location being visited</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td><strong>Iterator</strong>: Allows a client to have sequential access to aggregate object without exposing underlying structure.</td>
    <td></td>
    <td>
    </td>
  </tr>

  <tr>
    <td><strong>Chain of responsibility</strong>: Opens possibilities of processing for a request. It decouples request and its processing. <strong>Composite pattern</strong> is related to this pattern. </td>
    <td></td>
    <td>
      <ul>
      <li>Abstract handler: stores a successor that handles the request if the current handler does not handle it</li>
      <li>Concrete handler: implements checking if it can handle the request</li>
      </ul>
    </td>
  </tr>
</table>

### How each patterns differ

<table>
  <tr>
    <th>Adapter Pattern</th>
    <th>Other Pattern</th>
  </tr>
  <tr>
    <td>Ensures interface compatibility between classes with incompatible interfaces.</td>
    <td><strong>Bridge:</strong> Separates abstraction from implementation to enable independent variations.</td>
  </tr>
  <tr>
    <td>Ensures interface compatibility through adaptation and translation.</td>
    <td><strong>Decorator:</strong> Dynamically adds responsibilities to objects without interface changes, often extending functionality at runtime.</td>
  </tr>
  <tr>
    <td>Translates calls to ensure compatibility between interfaces.</td>
    <td><strong>Proxy:</strong> Controls object access, serving as a protective barrier with a focus on access control and lazy loading.</td>
  </tr>
  <tr>
    <td>Ensures compatibility between existing interfaces without altering source code.</td>
    <td><strong>Facade:</strong> Simplifies client interactions by providing a unified, higher-level interface to a group of interfaces, focusing on a streamlined experience rather than individual conversions.</td>
  </tr>
</table>

