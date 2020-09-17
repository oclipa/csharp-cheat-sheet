<div style="display: inline-block;">
<a class="link" href="http://oclipa.github.io/">&lt; home</a>
<a class="link" href="http://oclipa.github.io/toolbox.html">&lt; toolbox</a>
</div> 

## C# (work-in-progress)

&nbsp;

<button type="button" id="toggle-all" value="none">Expand All Sections</button>

&nbsp;

-------------------------------------------------------------------------------------------------------

<div id="stupid">
<button type="button" class="collapsible">+ Stupid Simple Stuff That I Keep Forgetting</button>
<div class="content" style="display: none;" markdown="1">

<div id="stupid-class">
<button type="button" class="collapsible">+ Class Syntax</button>
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace MyNamespace
{
    public abstract class MySuperClass
    {
        public MySuperClass()
        {
        }

        public abstract void Output();
    }

    public class MySubClass : MySuperClass
    {
        private int val;

        public MySubClass(int val = 5)
        {
            this.val = val;
        }

        public override void Output()
        {
            Console.WriteLine($"{this.val}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            MySuperClass myClass = new MySubClass();

            myClass.Output(); // output 5

            myClass = new MySubClass(10);

            myClass.Output(); // output 10
        }
    }
}
```

</div>
</div>

<div id="stupid-struct">
<button type="button" class="collapsible">+ Struct Syntax</button>
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace MyNamespace
{
    public struct MyStruct1
    {
        public int x;
        public int y;
    }
    
    public struct MyStruct2
    {
        public MyStruct2(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
        
        public int x;
        public int y;
    }
    
    class Program
    {
        static void Main(string[] args)
        {
            MyStruct1 myStruct1 = new MyStruct1();
            myStruct1.x = 5;
            myStruct1.y = 6;
            
            Console.WriteLine($"{myStruct1.x}, {myStruct1.y}"); // output: 5, 6
            
            MyStruct2 myStruct2 = new MyStruct2(7, 8);
            
            Console.WriteLine($"{myStruct2.x}, {myStruct2.y}"); // output: 7, 8
        }
    }
}
```

</div>
</div>

<div id="stupid-enum">
<button type="button" class="collapsible">+ Enum Syntax</button>
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace MyNamespace
{
    enum MyEnum
    {
        Val1,     // 0
        Val2,     // 1
        Val3 = 6, // 6
        Val4,     // 7
        Val5,     // 8
        Val6      // 9
    }

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(MyEnum.Val2); // output: Val2 
            int val = (int)MyEnum.Val2; // enum to int conversion
            Console.WriteLine(val); // output: 1 

            var en = (MyEnum)8; // int to enum conversion
            Console.WriteLine(en); // output: Val5 
        }
    }
}
```

</div>
</div>

<div id="stupid-switch">
<button type="button" class="collapsible">+ Switch Syntax</button>
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace MyNamespace
{
    class Program
    {
        static void Main(string[] args)
        {
            int x = 10;

            switch (x)
            { 
                case 5:
                    Console.WriteLine("Value of x is 5");
                    break;
                case 10:
                    Console.WriteLine("Value of x is 10");
                    break;
                case 15:
                    Console.WriteLine("Value of x is 15");
                    break;
                default:
                    Console.WriteLine("Unknown value");
                    break;
            }
        }
    }
}
```

</div>
</div>

<div id="stupid-switch">
<button type="button" class="collapsible">+ Event Syntax</button>
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace MyNamespace
{
    public class MyClass
    {
        public MyClass()
        {
        }

        public void TriggerEvent()
        {
            Changed(10);
        }

        public event Action<int> Changed;
    }

    class Program
    {
        static void Main(string[] args)
        {
            MyClass myClass = new MyClass();

            myClass.Changed += ChangeHandler;

            myClass.TriggerEvent(); // output: 10
        }

        static void ChangeHandler(int val)
        {
            Console.WriteLine($"{val}");
        }
    }
}
```

</div>
</div>

<div id="stupid-strings">
<button type="button" class="collapsible">+ Displaying Strings</button>
<div class="content" style="display: none;" markdown="1">

String Formatter:

```cs
Console.WriteLine(string.Format("{0} & {1}", var1, var2));
```

String Interpolation:

```cs
Console.WriteLine($"{var1} & {var2}");
```
</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="theory">
<button type="button" class="collapsible">+ Theory</button>
<div class="content" style="display: none;" markdown="1">
    
<div id="intro">
<button type="button" class="collapsible">+ What is C#?
    <code class="ex">
C# is an object-oriented, type-safe, and managed language that is compiled by .NET Framework to generate Microsoft Intermediate Language.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">
    
</div>
</div>

<div id="memory">
<button type="button" class="collapsible">+ Stack vs Heap
    <code class="ex">
Stack: contiguous memory; consists of frames, each of which corresponds to a method; frames are pushed to the stack, or popped from the stack (hence "call-stack")
Heap: dynamic memory; objects are garbage collected on occasion.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">

### Stack:
  * Contiguous memory.
  * A stack consists of frames; each frame corresponds to a method/function call.  A pointer references the current frame.
  * When a method is called, all of its value-types (and pointers) are stored as a frame which is pushed onto the top of the stack.
  * When the method returns, the frame for that method is popped off the stack (releasing the memory) and the pointer moves down to the next frame (i.e. the calling method).

### Heap:
   * Dynamic memory which can be allocated at will.
   * Can be fragmented since no guarantee which memory will be available at time objects are written.
   * Creating a reference-type objects reserves memory for the objects, plus overhead for the pointer, plus overhead for memory management.
   * When a reference-type objects is no longer referenced from the stack (or another objects), it is available to be garbage collected (which happens on occasion).

<img src="assets/images/dotnet_memory.png" />

</div>
</div>

<div id="interview-encapsulation"> 
  <button type="button" class="collapsible">+ What is Encapsulation?<br/>
    <code class="ex">data + behaviour = class</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

As the name suggestions, Encapsulation is the combination of an objects data and behaviours in a single unit, e.g. a Class.

The benefits of encapsulation are:
1. protection of data
1. control of accessibility
1. reduction of complexity (allows extensibility)
1. improved maintainability (reduces coupling between objects)

</div>
</div>

<div id="interview-inheritance"> 
  <button type="button" class="collapsible">+ What is Inheritance?<br/>
    <code class="ex">
Inheritance is the ability for multiple derived classes with similar features to be treated as objects of a common base class (or interface). 
To prevent inheritance of a class, use 'sealed class'.
To stop inheritance of a virtual or abstract member, use 'sealed override myMember'.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace Sandbox
{
    public class Car
    {
        public int Wheels { get { return 4; } }
    }

    public class Audi : Car { }
    public class BMW : Car { }

    class Program
    {
        static void Main(string[] args)
        {
            Car myAudi = new Audi();
            Car myBmw = new BMW();

            Console.WriteLine(myAudi.Wheels); // 4
            Console.WriteLine(myBmw.Wheels); // 4
        }
    }
}
```
  
</div>
</div>

<div id="interview-polymorphism"> 
  <button type="button" class="collapsible">+ What is Polymorphism?<br/>
    <code class="ex">
Polymorphism is the ability for derived classes to override properties of a common base class.
Static = Overloading
Dynamic = Interfaces, Abstract Classes, Virtual Members
   </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace Sandbox
{
    public interface IVehicle
    {
        int Wheels { get; }
    }

    public class Car : IVehicle
    {
        public int Wheels { get { return 4; } }
    }

    public class Bike : IVehicle
    {
        public int Wheels { get { return 2; } }
    }

    class Program
    {
        static void Main(string[] args)
        {
            IVehicle myCar = new Car();
            IVehicle myBike = new Bike();

            Console.WriteLine(myCar.Wheels); // 4
            Console.WriteLine(myBike.Wheels); // 2
        }
    }
}
```

</div>
</div>

<div id="interview-abstraction"> 
  <button type="button" class="collapsible">+ What is Abstraction?<br/>
    <code class="ex">
Abstraction hiding internal implementation details by making a class/interface as 'abstract' as possible.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
using System;

namespace Sandbox
{
    public interface IVehicle
    {
        void Start();
    }

    public class Car : IVehicle
    {
        public void Start() { startEngine(); }
        private void startEngine()
        {
            Console.WriteLine("Brrm brrm");
        }
    }

    public class Bike : IVehicle
    {
        public void Start() { startPeddling(); }
        private void startPeddling()
        {
            Console.WriteLine("Puff puff");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            IVehicle myCar = new Car();
            IVehicle myBike = new Bike();

            myCar.Start(); // Brrm Brrm
            myBike.Start(); // Puff puff
        }
    }
}
```
</div>
</div>

<div id="interview-classvsobj"> 
  <button type="button" class="collapsible">+ What is the difference between a Class and an Object?<br/>
    <code class="ex">
Class = Definition of an object.
Object = Instantiation of an class.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-solid"> 
  <button type="button" class="collapsible">+ What are the SOLID Principles?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="srp">    
<button type="button" class="collapsible">+ What is the Single Responsibility Principle (SRP)?
    <code class="ex">
Responsibility = "a reason to change"
Single Responsibility Principle = "A class should have only one reason to change"
A class should have one responsibility, which should be entirely encapsulated by the class.
    </code>
</button>    
<div class="content" style="display: none;" markdown="1">

As an example, consider a module that compiles and prints a report. Imagine such a module can be changed for two reasons:
1. The content of the report could change.
1. The format of the report could change. 

These two things change for very different causes; one substantive, and one cosmetic. 

The Single Responsibility Principle says that these two aspects of the problem are really two separate responsibilities, and should, therefore, be in separate classes or modules. 

It would be a bad design to couple two things that change for different reasons at different times.

The reason it is important to keep a class focused on a single concern is that it makes the class more robust. Continuing with the foregoing example, if there is a change to the report compilation process (i.e. the content), there is a greater danger that the printing (i.e. formatting) code will break if it is part of the same class.

</div>
</div>

<div id="ioc">    
<button type="button" class="collapsible">+ What is the Inversion Of Control (IoC) Principle?
    <code class="ex">
Any responsibility that is not the main responsibility of the class should not be encapsulated in the class, and should not be a direct dependency of the class.
Achieved using Dependency Inversion Principle (DIP), and the Dependency Injection (DI) and Strategy patterns.
    </code>
</button>    
<div class="content" style="display: none;" markdown="1">

IoC is a design principle which recommends the inversion of different kinds of controls in object-oriented design to achieve loose coupling between application classes.  It is closely related to the Single Responsibility Principle (SRP).

In this case, control refers to any additional responsibilities a class has, other than its main responsibility, such as control over the flow of an application, or control over the dependent object creation and binding.

The goal is that any responsibility that is not the main responsibility of the class should not be encapsulated in the class, and should not be a direct dependency of the class.

This is achieved using the Dependency Injection (DI) and Strategy patterns.

Adopting IoC is a prerequisite of TDD.
    
</div>
</div>

<div id="ioc">    
<button type="button" class="collapsible">+ What is the Dependency Inversion Principle (DIP)? 
    <code class="ex">
DIP suggests that high-level modules should not depend on low level modules. Both should depend on abstraction.
Extending this principle leading the the Dependency Injection (DI) pattern.
    </code>
</button>    
<div class="content" style="display: none;" markdown="1">

DIP is demonstrated in the following example:

First, the responsibility we want to abstract out is defined and made public.
The concrete implementation(s) of this responsibility can then be instantiated using a public factory class.

```cs
namespace MyNamespace.Dependency
{
    public interface ICustomerDataAccess
    {
        string GetCustomerName(int id);
    }
    
    internal class CustomerDataAccess: ICustomerDataAccess
    {
        public CustomerDataAccess()
        {
        }

        public string GetCustomerName(int id) {
            return "Dummy Customer Name";        
        }
    }
    
    public class DataAccessFactory
    {
        public static ICustomerDataAccess GetCustomerDataAccessObj() 
        {
            return new CustomerDataAccess();
        }
    }
}
```

The abstracted responsibility can then be referenced by a consumer without the consumer needing to be aware of the details:

```cs
using System;
using MyNamespace.Dependency;

namespace MyNamespace.Consumer
{
    public class CustomerBusinessLogic
    {
        ICustomerDataAccess _custDataAccess;

        public CustomerBusinessLogic()
        {
            _custDataAccess = DataAccessFactory.GetCustomerDataAccessObj();
        }

        public string GetCustomerName(int id)
        {
            return _custDataAccess.GetCustomerName(id);
        }
    }
    
    class Program
    {
        static void Main()
        {
            CustomerBusinessLogic customerBL = new CustomerBusinessLogic();
            Console.WriteLine(customerBL.GetCustomerName(123));
        }
    }
}
```
   
</div>
</div>

<div id="dependency">    
<button type="button" class="collapsible">+ What is the Dependency Injection (DI) pattern?
    <code class="ex">
Secondary responsibilities are injected into a class, to avoid direct dependencies or unnecessary encapsulation.
Constructor Injection, Property Injection & Method Injection.
A refinement of DI is the Strategy pattern.
    </code>
</button>   
<div class="content" style="display: none;" markdown="1">

The Dependency Injection is a pattern used to implement IoC (Inversion of Control), which allows for loosely coupled classes.

The pattern involves 3 types of classes:

  * Client Class: The client class (dependent class) is a class which depends on the service class
  * Service Class: The service class (dependency) is a class that provides service to the client class.
  * Injector Class: The injector class injects the service class object into the client class.

There are three types of Dependency Injection:

  * Constructor Injection
  * Property Injection
  * Method Injection

Each is described below.  

In each of the examples, the dependency (a.k.a. Service Class) to be injected is the following:

```cs
namespace MyNamespace.Dependency
{
    // public interface defines dependency
    public interface ICustomerDataAccess
    {
        string GetCustomerName(int id);
    }

    // INTERNAL SERVICE: concrete implementation of dependency
    internal class CustomerDataAccess : ICustomerDataAccess
    {
        public CustomerDataAccess()
        {
        }

        public string GetCustomerName(int id)
        {
            //get the customer name from the db in real application        
            return "Dummy Customer Name";
        }
    }
}
```

And the logic (a.k.a. Client Class) is consumed by the following:
```cs
using System;
using MyNamespace.Logic;

namespace MyNamespace.Consumer
{
    class Program
    {
        static void Main()
        {
            CustomerService customerService = new CustomerService();
            Console.WriteLine(customerService.GetCustomerName(123));
        }
    }
}
```

**Constructor Injection**

```cs
using MyNamespace.Dependency;

namespace MyNamespace.Logic
{  
    // INTERNAL CLIENT
    internal class CustomerBusinessLogic
    {
        ICustomerDataAccess _dataAccess;
        
        // dependency is injected into constructor
        public CustomerBusinessLogic(ICustomerDataAccess custDataAccess)
        {
            _dataAccess = custDataAccess;
        }

        public CustomerBusinessLogic()
        {
            _dataAccess = new CustomerDataAccess();
        }

        public string ProcessCustomerData(int id)
        {
            return _dataAccess.GetCustomerName(id);
        }
    }

    // PUBLIC INJECTOR
    public class CustomerService
    {
        CustomerBusinessLogic _customerBL;

        public CustomerService()
        {
            // inject dependency via constructor
            _customerBL = new CustomerBusinessLogic(new CustomerDataAccess());
        }

        public string GetCustomerName(int id)
        {
            return _customerBL.ProcessCustomerData(id);
        }
    }
}
```

**Property Injection**

```cs
using MyNamespace.Dependency;

namespace MyNamespace.Logic
{
    // INTERNAL CLIENT
    internal class CustomerBusinessLogic
    {
        public CustomerBusinessLogic()
        {
        }

        public string GetCustomerName(int id)
        {
            return DataAccess.GetCustomerName(id);
        }

        // dependency is injected into property
        public ICustomerDataAccess DataAccess { get; set; }
    }

    // PUBLIC INJECTOR
    public class CustomerService
    {
        CustomerBusinessLogic _customerBL;

        public CustomerService()
        {
            _customerBL = new CustomerBusinessLogic();
            
            // inject dependency via property
            _customerBL.DataAccess = new CustomerDataAccess();
        }

        public string GetCustomerName(int id)
        {
            return _customerBL.GetCustomerName(id);
        }
    }
}
```

**Method Injection**

```cs
using MyNamespace.Dependency;

namespace MyNamespace.Logic
{
    // INTERNAL CLIENT
    internal class CustomerBusinessLogic
    {
        ICustomerDataAccess _dataAccess;

        public CustomerBusinessLogic()
        {
        }

        public string GetCustomerName(int id)
        {
            return _dataAccess.GetCustomerName(id);
        }

        // dependency is injected into method
        public void SetDependency(ICustomerDataAccess customerDataAccess)
        {
            _dataAccess = customerDataAccess;
        }
    }

    // PUBLIC INJECTOR
    public class CustomerService
    {
        CustomerBusinessLogic _customerBL;

        public CustomerService()
        {
            _customerBL = new CustomerBusinessLogic();

            // inject dependency via method
            _customerBL.SetDependency(new CustomerDataAccess());
        }

        public string GetCustomerName(int id)
        {
            return _customerBL.GetCustomerName(id);
        }
    }
}
```

</div>
</div>

<div id="strategy">    
<button type="button" class="collapsible">+ What is the Strategy Pattern?   
    <code class="ex">
Allows algorithms to be selected at runtime.
The strategy pattern is intended to provide a means to define a family of algorithms, encapsulate each one as an object, and make them interchangeable. 
The strategy pattern lets the algorithms vary independently from clients that use them.
    </code>
</button>    
<div class="content" style="display: none;" markdown="1">
    
Building on the Dependency Injection example discussed above, an example of applying the Strategy pattern to this is the following:

```cs
using System;
using MyNamespace.Dependency;
using MyNamespace.Logic;

namespace MyNamespace.Dependency
{
    // public interface defines dependency
    public interface ICustomerDataAccess
    {
        string GetCustomerName(int id);
    }

    // identifies different algorithm types
    public enum DbAccessType
    {
        SQL,
        REST
    }

    // instantiates the requested algorithm type 
    public class DataAccessFactory
    {
        public static ICustomerDataAccess GetCustomerDataAccessObj(DbAccessType dbAccessType)
        {
            ICustomerDataAccess customerDataAccess = null;

            switch (dbAccessType)
            {
                case DbAccessType.SQL:
                    customerDataAccess = new CustomerDataAccessSQL();
                    break;
                case DbAccessType.REST:
                    customerDataAccess = new CustomerDataAccessREST();
                    break;
                default:
                    throw new Exception("unrecognized DB access type");
            }

            return customerDataAccess;
        }
    }

    // algorithm 1
    internal class CustomerDataAccessSQL : ICustomerDataAccess
    {
        public CustomerDataAccessSQL()
        {
        }

        public string GetCustomerName(int id)
        {
            //get the customer name from the db in real application        
            return "Dummy Customer Name using SQL";
        }
    }

    // algorithm 2
    internal class CustomerDataAccessREST : ICustomerDataAccess
    {
        public CustomerDataAccessREST()
        {
        }

        public string GetCustomerName(int id)
        {
            //get the customer name from the db in real application        
            return "Dummy Customer Name using REST";
        }
    }
}

namespace MyNamespace.Logic
{
    // receives and processing results of database query
    internal class CustomerBusinessLogic
    {
        ICustomerDataAccess _dataAccess;

        public CustomerBusinessLogic()
        {
        }

        public string GetCustomerName(int id)
        {
            return _dataAccess.GetCustomerName(id);
        }

        // dependency is injected into method
        public void SetDependency(ICustomerDataAccess customerDataAccess)
        {
            _dataAccess = customerDataAccess;
        }
    }

    // used by consumer to access the database using a particular type of algorithm
    public class CustomerService
    {
        CustomerBusinessLogic _customerBL;

        public CustomerService(DbAccessType dbAccessType)
        {
            _customerBL = new CustomerBusinessLogic();

            // inject dependency via method
            _customerBL.SetDependency(DataAccessFactory.GetCustomerDataAccessObj(dbAccessType));
        }

        public string GetCustomerName(int id)
        {
            return _customerBL.GetCustomerName(id);
        }
    }
}

namespace MyNamespace.Consumer
{
    class Program
    {
        static void Main()
        {
            CustomerService customerServiceREST = new CustomerService(DbAccessType.REST);
            Console.WriteLine(customerServiceREST.GetCustomerName(123));
            
            CustomerService customerServiceSQL = new CustomerService(DbAccessType.SQL);
            Console.WriteLine(customerServiceSQL.GetCustomerName(123));
        }
    }
}
```

</div>
</div>

<div id="interview-ocp"> 
  <button type="button" class="collapsible">+ What is the OCP SOLID Principle?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-lsp"> 
  <button type="button" class="collapsible">+ What is the LSP SOLID Principle?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-isp"> 
  <button type="button" class="collapsible">+ What is the ISP SOLID Principle?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>


<div id="interview-kiss"> 
  <button type="button" class="collapsible">+ What does KISS mean in OOP?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dry"> 
  <button type="button" class="collapsible">+ What does DRY mean in OOP?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-yagni"> 
  <button type="button" class="collapsible">+ What does YAGNI mean in OOP?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-tda"> 
  <button type="button" class="collapsible">+ What does TDA mean in OOP?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-builder"> 
  <button type="button" class="collapsible">+ What is the Builder Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-builder"> 
  <button type="button" class="collapsible">+ What is the Factory Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(see page 160)

</div>
</div>
  
<div id="interview-decorator"> 
  <button type="button" class="collapsible">+ What is the Decorator Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-chainofreponse"> 
  <button type="button" class="collapsible">+ What is the Chain of Responsibility Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(see page 158)

</div>
</div>

<div id="interview-adapter"> 
  <button type="button" class="collapsible">+ What is the Adapter Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-iterator"> 
  <button type="button" class="collapsible">+ What is the Iterator Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-nullobject"> 
  <button type="button" class="collapsible">+ What is the NullObject Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-visitor"> 
  <button type="button" class="collapsible">+ What is the Visitor Pattern?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-managed"> 
  <button type="button" class="collapsible">+ What is the difference between Managed and Unmanaged Code?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-strongvsweak"> 
  <button type="button" class="collapsible">+ What is the difference between Strong and Weak Typing?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-deadlocksql"> 
  <button type="button" class="collapsible">+ What is the difference between an SQL Deadlock and a C# Deadlock?<br/>
     <code class="ex">
A deadlock is  when separate threads are waiting for 2 objects, each one being locked by the other thread. So they are waiting for each other to unfreeze that object.
SQL can recover from a deadlock, because it has like a timeout by default.
C# application does not have a timeout and so it freezes and much be fixed.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Roughly speaking, SQL can recover from a deadlock because it assigns priorities to each transaction and will kill the lowest priority if a deadlock occurs.

The following is an example of C# code that will cause a deadlock:

```cs
using System.Threading;

class Program
{
    static object object1 = new object();
    static object object2 = new object();

    public static void Method1()
    {
        lock (object1)
        {
            Thread.Sleep(1000); // Wait for the Method2 to unlock objects 
            lock (object2)
            {
                Console.WriteLine("Finished Method1");
            }
        }
    }

    public static void Method2()
    {
        lock (object2)
        {
            Thread.Sleep(1000); // Wait for the Method2 to unlock objects 
            lock (object1)
            {
                Console.WriteLine("Finished Method2");
            }
        }
    }

    static void Main()
    {
        var tasks = new List<Task>();

        Action writer1 = Method1;
        // Execute a writer.
        tasks.Add(Task.Run(writer1));

        Action writer2 = Method2;
        // Execute a writer.
        tasks.Add(Task.Run(writer2));

        // Wait for all three tasks to complete.
        Task.WaitAll(tasks.ToArray()); // deadlock!

        Console.WriteLine("Finished all tasks");
    }
}
```

A suggestion for a way to avoid such a deadlock is to use System.Threading.ReaderWriteLockSlim, which allows multiple threads to read a resource while allowing exclusive access for writing.  In the following example, this approach is to use to ensure that any thread that sleeps for too long will abort.

```cs
using System;
using System.Threading;
using System.Threading.Tasks;
using System.Collections.Generic;

// See https://docs.microsoft.com/en-us/dotnet/api/system.threading.readerwriterlockslim?view=netcore-3.1
// for a fuller implementation
public class SynchronizedWriter
{
    private ReaderWriterLockSlim cacheLock = new ReaderWriterLockSlim();

    static object object1 = new object();
    static object object2 = new object();

    public bool WriteWithTimeout(string value, int millisecondsTimeout)
    {
        if (cacheLock.TryEnterWriteLock(millisecondsTimeout))
        {
            try
            {
                lock (object1)
                {
                    Thread.Sleep(1000); // Wait for the Method2 to unlock objects 
                    lock (object2)
                    {
                        Console.WriteLine(value);
                    }
                }
            }
            finally
            {
                cacheLock.ExitWriteLock();
            }
            return true;
        }
        else
        {
            Console.WriteLine($"Failed to write \"{value}\"");
            return false;
        }
    }

    ~SynchronizedWriter()
    {
        if (cacheLock != null) cacheLock.Dispose();
    }
}

class Program
{
    public static void Method1(SynchronizedWriter sw)
    {
        sw.WriteWithTimeout("Finished Method1", 500);
    }

    public static void Method2(SynchronizedWriter sw)
    {
        sw.WriteWithTimeout("Finished Method2", 500);
    }

    static void Main()
    {
        var sw = new SynchronizedWriter();
        var tasks = new List<Task>();

        Action<SynchronizedWriter> writer1 = Method1;
        // Execute a writer.
        tasks.Add(Task.Run(() => writer1(sw)));

        Action<SynchronizedWriter> writer2 = Method2;
        // Execute a writer.
        tasks.Add(Task.Run(() => writer2(sw)));

        // Wait for all three tasks to complete.
        Task.WaitAll(tasks.ToArray());

        Console.WriteLine("Finished all tasks");
    }
}
```
  
</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="basics">
<button type="button" class="collapsible">+ Coding</button>
<div class="content" style="display: none;" markdown="1">
    
<div id="structs">  
<button type="button" class="collapsible">+ Structs vs Classes
    <code class="ex">
Struct: value-type; cannot be null (unless Nullable<>); cannot have multiple objects reference the same struct (must be copied).
Class: reference-type; can consume more memory and lead to memory fragmentation; can be slower to initialize.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">

### Structs:

```csharp
public struct MyStruct
{
    public float number;
    public byte flags;
    public byte index;
}
```
   * Value-type (entire object stored in a single memory location).
   * Supports inheritance.
   * Allocated on the stack (if local to a function) or on the heap (if a class member).
   * Cannot be null (unless Nullable<> is used)
   * Memory overhead is: (total size of fields) + (memory alignment padding)
   * Unless using the `ref` keyword, structs are always copied when passed into functions.
      * When using `ref` the stack address of the value type is passed, rather than a copy of the value type.
   * Once out of scope, memory location is immediately available to be overwritten.
   * Memory is contiguous, so may improve memory access patterns and CPU caching.
  
   * Cons: 
      * Cannot usually have multiple objects reference the same struct; each requires its own copy of the struct.
      * Large structs can be slow to copy, which can impact performance.
      * Boxing a struct (i.e. converting it in an objects) can impact performance

### Classes:

```csharp
public class MyStruct
{
    public float number;
    public byte flags;
    public byte index;
}
```
   * Reference-type (object is referenced by a pointer).
   * Supports inheritance.
   * Allocated on the heap.
   * Can be null (if pointer is not assigned to a memory location)
   * Memory overhead is: (total size of fields) + (8 byte pointer) + (16 byte memory management).
   * References to a class are passed between methods (rather than the class itself).
   * Once out of scope, the memory location is available to be garbage collected (which may not happen immediately).
   * Memory can be fragmented.

  * Cons: 
     * Extra memory overhead (which may not be immediately removed when the objects is no longer referenced)
     * objects require initialization, which can impact performance.
     * Memory fragmentation can lead to slower performance.

</div>
</div>

<div id="boxing">  
<button type="button" class="collapsible">+ Boxing vs Unboxing
    <code class="ex">
Only works for value types.
box: object o = 100; // value type to reference type
unbox: int x = (int)o; // reference type to value type
Avoid; slow performance.  Use Generics.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">

Boxing is the conversion of a value type to an reference type, or any interface face type implemented by the value type.

Boxing a value type creates an object instance containing the value and stores it on the heap.

e.g. `object o = 100;`

Unboxing is the reverse of this process:

e.g. `int x = (int)o;`

</div>
</div>

<div id="delegates">   
<button type="button" class="collapsible">+ Delegate vs Action vs Func vs Predicate
    <code class="ex">
Delegate: older, generic form of Action, Func and Predicate.
Action: Accept arguments; does not return.
Func: Accept arguments; returns a value.
Predicate: Special case of Func that only returns a bool.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">

**Be sure to also read the section on Closures.**

   * ### Delegate:
      * An older, generic form of Action, Func and Predicate.
      * Nowadays, prefer Action and Func, which are generally less complex and easier to read.
      
```csharp
using System;

namespace MyNamespace
{
    class Program
    {
        public delegate int CalculateIt(int x, int y);

        static void Main(string[] args)
        {
            CalculateIt calc = Add;
            // Prints out "Result = 9"
            Console.WriteLine("Result = " + calc(4, 5));

            calc = Subtract;
            // Prints out "Result = -1"
            Console.WriteLine("Result = " + calc(1, 2));
        }

        static int Add(int a, int b)
        {
            return a + b;
        }

        static int Subtract(int a, int b)
        {
            return a - b;
        }
    }
}
```
      * TODO: A multicast delegate
      * Nowadays, prefer Action and Func, which are generally less complex and easier to read.

   * ### Action&lt;T&gt;: 
      * Return type must be `void`
      
```csharp
using System;

namespace MyNamespace
{
    class Program
    {
        static void Main(string[] args)
        {
            Action<int, int> calc = Add;
            // Prints out "Result = 9"
            calc(4, 5);

            calc = Subtract;
            // Prints out "Result = -1"
            calc(4, 5);

            Action<int, int> anonymousAction = (a, b) =>
            {
                Console.WriteLine("Result = " + (a + b));
            };

            // Prints out "Result = 9"
            anonymousAction.Invoke(4, 5);
        }

        static void Add(int a, int b)
        {
            Console.WriteLine("Result = " + (a + b));
        }

        static void Subtract(int a, int b)
        {
            Console.WriteLine("Result = " + (a - b));
        }
    }
}
```

   * ### Func&lt;T&gt;:
      * Must return a value

```csharp
using System;

namespace MyNamespace
{
    class Program
    {
        static void Main(string[] args)
        {
            // note: Func<in, in, out>
            Func<int, int, int> calc = Add;
            // Prints out "Result = 9"
            Console.WriteLine("Result = "
                               + calc(4, 5));

            calc = Subtract;
            // Prints out "Result = -1"
            Console.WriteLine("Result = "
                                + calc(4, 5));

            Func<int, int, int> anonFunc =
                     (a, b) => { return a + b; };

            // Prints out "Result = 9"
            Console.WriteLine("Result = "
                        + anonFunc.Invoke(4, 5));
        }

        static int Add(int a, int b)
        {
            return a + b;
        }

        static int Subtract(int a, int b)
        {
            return a - b;
        }
    }
}
```

   * ### Predicate&lt;T&gt;:
      * A special case of Func that only returns a bool.
      
</div>
</div>

<div id="closures">  
<button type="button" class="collapsible">+ Closures
    <code class="ex">
Closures are used to encapsulate variables within the methods that require them.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">

Closures are used to encapsulate variables within the methods that require them.  

There are two basic uses cases:
1. Storing the state of data to be used in a particular method at a later time.
1. Hiding data but leaving it accessible to a particular method.

They are particularly relevant to Delegates (including Action, Func and Predicate), since they mean that the state of arguments can be read at the time they are called, not at the time they are instantiated.  However, this does means that care must be taken to ensure the correct values are applied.  

For example, in the following code the output will be the number 10 ten times, rather than the expected 0 to 9:

```cs
using System;
using System.Collections.Generic;

namespace MyNamespace
{
    class Program
    {
        delegate void Printer();

        static void Main()
        {
            List<Printer> printers =
                     new List<Printer>();

            int i = 0;
            for (; i < 10; i++)
            {
                printers.Add(delegate
                {
                    Console.WriteLine(i);
                });
            }

            foreach (var printer in printers)
            {
                printer();
            }
        }
    }
}
```
At first glance, the above code would seem to indicate that `i` is incremented for each new delegate added to `printers`, however in practice what happens is that the compiler has associated the delegates with the variable `i` and the runtime will use whatever the value of `i` is at the time the delegate method is called (in the `foreach` loop).

Conceptually, the compiler does something like this:

```csharp
// "replace" the delegate with a closure
// that includes the method and any variables
// if depends on.
class PrinterClosure
{
    public int CurrentI;
    public void Printer() => 
          Console.WriteLine(this.currentI);
}

static void Main()
{
    // "replace" all references to
    // Printer with PrinterClosure
    List<PrinterClosure> printers = 
                new List<PrinterClosure>();
    
    int i=0;
    for(; i < 10; i++)
    {
        // PrinterClosure is assigned a value
        // for i, but doesn't use it here
        printers.Add(
            new PrinterClosure() { i } 
        );
    }

    foreach (PrinterClosure printer in printers)
    {
        // PrinterClosure now picks up the
        // value of i (10)
        printer.CurrentI = i;
        printer.printer();
    }
}
```

To avoid this, the value of `i` should be passed as an argument, rather than as a scoped variable:

```csharp
delegate void Printer(int i);

static void Main()
{
    List<Printer> printers = 
              new List<Printer>();
    
    int i=0;
    for(; i < 10; i++)
    {
        printers.Add(delegate(i) { 
            Console.WriteLine(i); 
        });
    }

    foreach (var printer in printers)
    {
        // prints out 0..9 as expected
        printer();
    }
}
```

In this case, the compiler (again, conceptually) generates a closure similar to the following:

```csharp
class PrinterClosure
{
    // i will be scoped to 
    // the Printer method
    public void Printer(int i) => {
        Console.WriteLine(i);
    };
}
```

</div>
</div>

<div id="linq">  
<button type="button" class="collapsible">+ Linq
    <code class="ex">
LINQ (Language Integrated Query) is uniform query syntax to retrieve data from different sources and formats.
Like SQL for .NET data sources.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">
      
Further info: [https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable)

### Where

```csharp
IEnumerable<TSource> result = 
    Where<TSource>(
        IEnumerable<TSource>, Func<TSource,Boolean>
    );

var result = source.Where(o => o.Prop == x);
```

### Select

```csharp
IEnumerable<TSource> result = 
    Select<TSource,TResult>(
        IEnumerable<TSource>, Func<TSource,TResult>
    );

var result = source.Select(o => new { 
                     Prop1 = o.Prop1; 
                     Prop2 = o.Prop2 
             });
```

### OrderBy

```csharp
IEnumerable<TSource> result = 
    OrderBy<TSource,TKey>(
        IEnumerable<TSource>, Func<TSource,TKey>
    );

var result = source.OrderBy(o => o.Prop);
```

### OrderByDescending

```csharp
IEnumerable<TSource> result = 
    OrderByDescending<TSource,TKey>(
        IEnumerable<TSource>, Func<TSource,TKey>
    )

var result = source.OrderByDescending(o => o.Prop);
```

### ThenByDescending

```csharp
IEnumerable<TSource> result = 
    OrderBy[...].
    ThenByDescending(
        IEnumerable<TSource>, Func<TSource,TKey>
    );

var result = source.OrderBy(o => o.Prop1).
               ThenByDescending(o => o.Prop2);
```

### Join

```csharp
var result = source1.Join(source2, 
                     o1 => o1.Prop1, 
                     o2 => o2.Prop1, 
                     (o1, o2) => new 
                         {
                             o1.Prop1,
                             o1.Prop2,
                             o2.Prop3,
                             o2.Prop4
                         }
                     );
```

### GroupBy

```csharp
var result = source1.GroupBy(o => o.Prop).
                 Select(grp => new {
                     PropId = grp.Key,
                     PropCount = grp.Count()
                 }
             );
```

### Take

```csharp
// select top 3

var result = source.Where(
                     o => o.Prop == x).
                     Take(3);
```

### Skip

```csharp
// uses a mixture of query syntax and lambda syntax

var result = (from o in source
                where o.Prop1 == x
                orderby o.Prop2
                select o).Skip(2).Take(3);
```

### Single

```csharp
// throws an exception if no elements

var result = source.Single(
                 o => o.Prop == x
             );
```

### SingleOrDefault

```csharp
// returns null if no elements

var result = source.SingleOrDefault(
                 o => o.Prop == x
             );
```

### DefaultIfEmpty

```csharp
// returns a new OClass instance if no elements

var result = source.Where(o => o.Prop == x).
                 DefaultIfEmpty(new OClass()).
                 Single();
```

### Last

```csharp
// First, Last and ElementAt used in same way

var result = source.Where(o => o.Prop == x).
                 OrderBy(o => o.Prop).
                 Last();
```

### SingleOrDefault

```csharp
// returns 0 if no elements

var result = source.Where(o => o.Prop == x).
                 Select(o => o.Prop).
                 SingleOrDefault();
```

### ToArray

```csharp
// uses query syntax

string[] result = (from o in source
                select o.Prop).ToArray();
```

### ToDictionary

```csharp
// uses lambda syntax

Dictionary<int, OClass> result = 
        source.ToDictionary(o => o.IntProp);

// uses a mixture of query syntax and 
// lambda syntax

Dictionary<string, double> result = 
  (from og in
    (from o1 in source1
     join o2 in source2 on o1.Prop equals o2.Prop
     select new { o2.StrProp, o1.DblProp})
      group og by og.StrProp into g
      select g).
        ToDictionary(g => g.Key, 
                     g => g.Max(og => og.DblProp)
        );
```

### ToList

```csharp
// uses query syntax

List<OClass> res = (from o in source
                    where o.Prop > x
                    orderby o.Prop
                   ).ToList();
```

### ToLookup

```sharp
ILookup<int, string> result = 
    source.toLookup(o => 
                    o.IntProp, o.StrProp
    );
```
</div>
</div>

<div> 
<button type="button" class="collapsible">+ Async & Await
    <code class="ex">
Async: indicates that a method performs asynchronous actions.
Await: indicates that the calling method should return immediately; the rest of the calling method will complete once the awaited method returns.
    </code>
</button>
<div class="content" style="display: none;" markdown="1">

If an `async` method calls another method or function using the `await` keyword, the calling method will return instantly at the point `await` is called; any instructions after the `await` will not complete until after the awaited method completes.

In the following example, the output from the program will be null, since `result` will not be initialized until after `Task.Delay(5)` returns, which will not happen until after WriteLine() is called.

```csharp
class Program {
  private static string result;
 
  static void Main() {
    SaySomething();
    Console.WriteLine(result);
  }
 
  static async Task<string> SaySomething() {
    await Task.Delay(5);
    result = "Hello world!";
    return “Something”;
  }
}
```

An alternative approach would be to use `Thread.Sleep(5)`, rather than `Task.Delay(5)`, since this will cause the main thread to block until the `Sleep()` method returns, so that `result` will be initialized before the `SaySomething` method returns.  In this case, the program will return `Hello world!`.

</div>
</div>

<div id="arrays">   
<button type="button" class="collapsible">+ Arrays</button>   
<div class="content" style="display: none;" markdown="1">

See: [Arrays](http://zetcode.com/lang/csharp/arrays/)
And: [Join](https://www.geeksforgeeks.org/c-sharp-join-method-set-1/)  (and Split)

* Jagged Arrays

</div>
</div>

<div>  
<button type="button" class="collapsible">+ Data Structures</button>  
<div class="content" style="display: none;" markdown="1">

Should create a separate page that goes through these in depth

### Array
### ArrayList
### Stack
### Queue
### LinkedList<T> (Doubly-Linked List)
### HashTable
### Dictionary<TKey, TValue>
### SortedSet<T> (Red-Black Tree)

See [here](https://stackoverflow.com/questions/1806511/objects-that-represent-trees).

### Singly-Linked List
### Skip List
### Binary Search Tree
### Cartesian Tree
### B-Tree
### Splay Tree
### AVL Tree
### KD Tree

</div>
</div>

<div id="interview-accessmodifiers"> 
  <button type="button" class="collapsible">+ What are access modifiers?<br/>
    <code class="ex">
public, internal protected, private, protected internal, private protected

Classes and interfaces can only be public or internal.

The default access for everything in C# is "the most restricted access you could declare for that member".
(except in a property getter or setter, which inherits from the property)
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Modifiers are used to provide some control over how the API is used.

* `public` = Accessible anywhere within the project.
* `internal` = Accessible only within the assembly.
* `protected` = Accessible only within the current class and its derived classes.
* `private` = Accessible only within the current class.
* `protected internal` = Accessible anywhere within the assembly, and within any derived classes within the project.
* `private protected` = Accessible within any derived classes within the assembly. 

Interfaces members cannot have access modifiers (they are always the same as the interface).

**Inheritance Access Modifiers**

By definition, inheritance means that a sub-class contains all members of its direct super-class (except for constructors and destructors).  This includes all private members: they are inaccessible, but still occupy memory.

In a sub-class, the methods of the super-class can be overridden using either the `new` or `override` keywords.
  * `new`: in this case, the sub-class version of the method will be called if the super-class has been downcast to the sub-class (otherwise the super-class version will be called).
  * `override`: in this case, the sub-class version of the method will always be called, even if the sub-class has been upcast to the super-class.
  
Using the `base` keyword in a sub-class method will access the super-class version of the methods.

```cs
using System;

class BaseClass
{
    public virtual void Method1()
    {
        Console.WriteLine("Base - Method1");
    }

    public void Method2()
    {
        Console.WriteLine("Base - Method2");
    }

    public virtual void Method3()
    {
        Console.WriteLine("Base - Method3");
    }
}

class DerivedClass : BaseClass
{
    public override void Method1()
    {
        Console.WriteLine("Derived - Method1");
    }

    public new void Method2()
    {
        Console.WriteLine("Derived - Method2");
    }

    public override void Method3()
    {
        base.Method3();
    }
}

class Program
{
    static void Main(string[] args)
    {
        BaseClass bc = new BaseClass();
        DerivedClass dc = new DerivedClass();
        BaseClass bcdc = new DerivedClass();

        bc.Method1();   // Base - Method1
        bc.Method2();   // Base - Method2
        bc.Method3();   // Base - Method3
        dc.Method1();   // Derived - Method1
        dc.Method2();   // Derived - Method2
        dc.Method3();   // Base - Method3
        bcdc.Method1(); // Derived - Method1
        bcdc.Method2(); // Derived - Method1
        bcdc.Method3(); // Base - Method2
    }
}
```

</div>
</div>

<div id="interview-whilevsfor"> 
  <button type="button" class="collapsible">+ What is the difference between a while and a for loop?<br/>
    <code class="ex">
For is used when number of repeats is known.
While is used when a sentinel loop is necessary.
Exactly the same after compilation.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dowhilevswhile"> 
  <button type="button" class="collapsible">+ What is the difference between do-while and a while loop?<br/>
     <code class="ex">
Do-While is used if the loop should always runs at least once.
While is used if a test should be evaluated before the loop runs.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-continuevsbreak"> 
  <button type="button" class="collapsible">+ What is the difference between continue and break?<br/>
     <code class="ex">
Break exists a loop.
Continue skips to the next iteration of a loop.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-abstractvsvirtual"> 
  <button type="button" class="collapsible">+ What is the difference between abstract and virtual?<br/>
     <code class="ex">
Abstract methods cannot have functionality.
Virtual methods provide a default implementation.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

* Abstract methods can only be declared in abstract classes.
* Abstract classes cannot be instantiated.
* An abstract sub-class can inherit from an abstract super-class without providing an implementation.

* In the abstract and virtual cases, use the `override` key word to provide an implementation in a sub-class.


```cs
using System;

public abstract class Vehicle
{
    public Vehicle() { }
    public virtual int Wheels { get { return 4; } }
}

public class Truck : Vehicle
{
    private int wheels;

    public Truck(int wheels) : base() { this.wheels = wheels; }
    public override int Wheels { get { return this.wheels; } }
}

class Program
{
    static void Main(string[] args)
    {
        Vehicle truck = new Truck(12);

        Console.WriteLine(truck.Wheels);
    }
}
```

</div>
</div>

<div id="interview-partial"> 
  <button type="button" class="collapsible">+ What is a partial class?<br/>
     <code class="ex">
A class that is constructed from functionality defined in multiple files.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The functionality from multiple partial classes can be combined into a single class at runtime. 

Partial class are declared using the `partial` keyword.

* Every part of the partial class definition should be in the same assembly and namespace, but you can use different source file name.
* Every part of the partial class definition should have the same accessibility like private, protected, etc.
* If any part of the partial class is declared as `abstract` or `sealed`, then the whole class is declared of the same type.

Generally only encountered with generated code, where a portion of the code is automatically generated but another portion may be edited by the developer.  Splitting the parts across separate files can make things cleaner.

```cs
public partial class MyPartialClass 
{ 
    public void Method1() 
    { 
    } 
}

public partial class MyPartialClass 
{ 
    public void Method2() 
    { 
    } 
}
```

After compilation, this becomes:

```cs
public class MyPartialClass 
{ 
    public void Method1() 
    { 
    } 
    
    public void Method2() 
    { 
    } 
}
```

</div>
</div>

<div id="interview-sealed"> 
  <button type="button" class="collapsible">+ What does the sealed keyword mean?<br/>
     <code class="ex">
Sealed classes cannot be inherited.
Sealed methods cannot be overrriden.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The following code will not compile:

```cs
// Creating a sealed class
sealed class Test : OptionalBaseClass 
{ 
} 

// Inheriting the Sealed Class 
class Example : Test 
{ 
}
```

Reasons for using a sealed class:

* To prevent tampering of important classes that compromise security or performance.
* If the class inherits many virtual members, it may be more efficient than sealing each individually.
* The class is an attribute that requires a very fast runtime look-up (sealed attributes have slightly better performance).

</div>
</div>

<div id="interview-interfacevsabstract"> 
  <button type="button" class="collapsible">+ What is the difference between an interface and an abstract class?<br/>
     <code class="ex">
Interfaces allow multiple inheritance (composition - "has a"); abstract classes do not (inheritance - "is a").
Abstract classes have a constructor, interfaces cannot.
Abstract classes can have static members, interfaces cannot.
The members of an abstract class can have access modifiers, those in an interface cannot.
Abstract classes can provide implementation, interfaces cannot.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-multipleinterfaces"> 
  <button type="button" class="collapsible">+ Can you implement multiple interfaces with the same method a single class?<br/>
     <code class="ex">
Yes, but they need to be accessed explicitly.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
interface T1 
{ 
    void Set(); 
} 

interface T2 
{ 
    void Set(); 
}
```

```cs
// implements both interfaces 
class Example : T1, T2
{
    void T1.Set()
    {
        Console.WriteLine("T1");
    }
    void T2.Set()
    {
        Console.WriteLine("T2");
    }
}
```

```cs
static public void Main () 
{ 
    T1 t1 = new Example(); 

    // calling T1 interface method 
    t1.Set(); 

    // Creating object of Example 
    // of T2 interface 
    T2 t2 = new Example(); 

    // calling T2 interface method 
    t2.Set(); 
}
```

**Caveat**

An alternative - but not recommended solution - is to make the shared member public:

```cs
class Example : T1, T2 
{ 
    public void Set() 
    { 
    } 
}
```

This will work, however it is ambiguous to which interface the implementation refers.

</div>
</div>

<div id="interview-static"> 
  <button type="button" class="collapsible">+ What is the difference between static and non-static?<br/>
     <code class="ex">
Static classes cannot be instantiated.
Non-static classes must be instantiated.
Only static members can be accessed from a static class.
Non-static classes can have static members but static members cannot access non-static variables.
A static constructor is called before any other constructor.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

All static objects, whether reference-type or value-type, are maintained on the **heap**, just the same as any other object, however they exist for the life of the app and so are not garbage collected (more specifically, static objects are stored in the **high-frequency heap**, which is a **loader heap**, which is separate to the normal **GC heap**).

<img src="assets/images/dotnet_memory.png" />

**Static Constructors**

Static members and classes are initialized when an app first starts.  This means that static constructors will always be called before non-static ones.

See the following example:

```cs
using System;

class Program
{
    public class TestStatic
    {
        public static int TestValue;

        public TestStatic()
        {
            if (TestValue == 0)
            {
                TestValue = 5;
            }
        }
        
        static TestStatic()
        {
            if (TestValue == 0)
            {
                TestValue = 10;
            }
        }

        public void Print()
        {
            if (TestValue == 5)
            {
                TestValue = 6;
            }
            Console.WriteLine("TestValue : " + TestValue);
        }
    }

    static void Main(string[] args)
    {
        TestStatic t = new TestStatic();
        t.Print(); // output: 10
    }
}
```

</div>
</div>

<div id="interview-const"> 
  <button type="button" class="collapsible">+ What is the difference between const and read-Only?<br/>
     <code class="ex">
const = cannot be changed after compile time; only applies to primitive types (it is implicitly static).  Should only be used if value will never, ever change.
read-only = can only be set when a class is instantiated (i.e. in the class declaration or constructor)
static readonly = effectively the same as const, although there are some significant subtleties (see inside).
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The primary difference between `const` and `static readonly` is illustrated by the following example:

Assembly A:

```cs
public class MyData
{
    public const int CONSTANT_NUMBER = 6;
    public readonly int READONLY_NUMBER = 12;
}
```

Assembly B:

```cs
public class MyLogic
{
    private int myConstantNumber;
    private int myReadOnlyNumber;

    public MyLogic()
    {
        this.myConstantNumber = MyData.CONSTANT_NUMBER;

        MyData myData = new MyData();
        this.myReadOnlyNumber = myData.READONLY_NUMBER;
    }

    public void WriteNumbers()
    {
        Console.WriteLine(string.Format("{0} & {1}", this.myConstantNumber, this.myReadOnlyNumber));
    }
}
```

Note that Assembly B depends on Assembly A.

When initially run, `WriteNumbers()` will output `6 & 12`.

Subsequently, the value of `CONSTANT_NUMBER` is changed in Assembly A, which is recompiled.  Assembly B, however, is not recompiled.

Assembly A:

```cs
public class MyData
{
    public const int CONSTANT_NUMBER = 20;
    public readonly int READONLY_NUMBER = 12;
}
```

Now, when `WriteNumbers()` is run, **the output will still be `6 & 12`**.

This is because, being a `const`, the value of `CONSTANT_NUMBER` will be "baked" into the IL of Assembly B at compile time, so it will ignore any subsequent changes to this value in Assembly A.

For this reason, it is recommended that `const` only be used if you know that this value will never, ever, *ever* change for any reason.  If you are unsure, use `readonly`. 

</div>
</div>

<div id="interview-overload"> 
  <button type="button" class="collapsible">+ What is the difference between overriding and overloading?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hiding"> 
  <button type="button" class="collapsible">+ How can a method be hidden?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-privateconstruct"> 
  <button type="button" class="collapsible">+ Why used a Private Constructor?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-privateconstruct"> 
  <button type="button" class="collapsible">+ Why use a Static Constructor?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-string"> 
  <button type="button" class="collapsible">+ What is the difference between String and StringBuilder?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-passbyvalue"> 
  <button type="button" class="collapsible">+ What is Pass By Value?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-passbyrefeence"> 
  <button type="button" class="collapsible">+ What is Pass By Reference?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-refvsout"> 
  <button type="button" class="collapsible">+ What is difference between Ref and Out?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-asvsis"> 
  <button type="button" class="collapsible">+ What is the difference between As and Is?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-exceptions"> 
  <button type="button" class="collapsible">+ What is the difference between Throw Exception and Throw?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-tryblock"> 
  <button type="button" class="collapsible">+ Can you have a Try Block without a Catch?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-finally"> 
  <button type="button" class="collapsible">+ Why would you use Finally?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-attribute"> 
  <button type="button" class="collapsible">+ What is an Attribute?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-getset"> 
  <button type="button" class="collapsible">+ What are Get and Set?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-caching"> 
  <button type="button" class="collapsible">+ What is Caching?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-genericconstraints"> 
  <button type="button" class="collapsible">+ Can you set Constraints on Generic Classes?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-extensions"> 
  <button type="button" class="collapsible">+ What are Extension Methods?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-anontype"> 
  <button type="button" class="collapsible">+ What is an Anonymous Type?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-objpool"> 
  <button type="button" class="collapsible">+ What is an Object Pool?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-defvsimed"> 
  <button type="button" class="collapsible">+ What is Deferred Execution vs Immediate Execution?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-stream"> 
  <button type="button" class="collapsible">+ What is a Stream?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-equals"> 
  <button type="button" class="collapsible">+ What is the difference between `Equals()` and `==`?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-binding"> 
  <button type="button" class="collapsible">+ What is the difference between Early-Binding and Late-Binding?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-type"> 
  <button type="button" class="collapsible">+ What is the difference between `typeof` and `GetType()`?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-linq"> 
  <button type="button" class="collapsible">+ What is the difference between LINQ and Stored Procedures?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-staticthis"> 
  <button type="button" class="collapsible">+ Can you use `this` inside a static method in C#?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-delegate"> 
  <button type="button" class="collapsible">+ What are Delegates?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-genericperf"> 
  <button type="button" class="collapsible">+ How can you improve the Performance of Generic Classes?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-reflection"> 
  <button type="button" class="collapsible">+ What is Reflection?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-yield"> 
  <button type="button" class="collapsible">+ What does `yield return` do?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-list"> 
  <button type="button" class="collapsible">+ What are some common List Interfaces?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-enumerable"> 
  <button type="button" class="collapsible">+ What is the difference between IEnumerable and IQueryable?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threadvsprocess"> 
  <button type="button" class="collapsible">+ What is the difference between a Thread and a Process?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-deadlocks"> 
  <button type="button" class="collapsible">+ How are Deadlocks handled in Multithreaded Processes?<br/>
     <code class="ex">
lock, semaphores, mutex
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threads"> 
  <button type="button" class="collapsible">+ How are Threads managed?<br/>
     <code class="ex">
SystemThread, ThreadPool, Delegate.BeginInvoke
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-interprocess"> 
  <button type="button" class="collapsible">+ How can you send data between Processes?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threadstates"> 
  <button type="button" class="collapsible">+ What states can a Thread have?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dispose"> 
  <button type="button" class="collapsible">+ What is the difference between Dispose and Finalize?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>


<div id="interview-querycomp"> 
  <button type="button" class="collapsible">+ What is Query Comprehension/Syntax?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-covar"> 
  <button type="button" class="collapsible">+ In Generics, what is the difference between Covariance and Contravariance?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-expressiontrees"> 
  <button type="button" class="collapsible">+ What are Expression Trees?<br/>
    <code class="ex">
A way of breaking down functions into a tree like structure.
Expression trees were created for the task of converting code such as a query expression into a string that can be passed to some other process and executed there.
Of particular relevance to LINQ.
   </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Given the following expression:

```cs
Expression<Func<Student, bool>> isTeenagerExpr = s => s.age > 12 && s.age < 20;
```

The compiler will break this down into:

```cs
Expression.Lambda<Func<Student, bool>>(
                Expression.AndAlso(
                    Expression.GreaterThan(Expression.Property(pe, "Age"), Expression.Constant(12, typeof(int))),
                    Expression.LessThan(Expression.Property(pe, "Age"), Expression.Constant(20, typeof(int)))),
                        new[] { pe });
```

Expressions can also be built manually.  Take the following example:

```cs
Func<Student, bool> isAdult = s => s.age >= 18;
```

This is identical to:

```cs
public bool function(Student s)
{
  return s.Age > 18;
}
```

To construct this as an expression, first the parameters are extracted:

```cs
ParameterExpression pe = Expression.Parameter(typeof(Student), "s");
```

And then the members:

```cs
MemberExpression me = Expression.Property(pe, "Age");
```

And then constants:

```cs
ConstantExpression constant = Expression.Constant(18, typeof(int));
```

And then any binary expressions:

```cs
BinaryExpression body = Expression.GreaterThanOrEqual(me, constant);
```

Finally, this can all be put together as:

```cs
// var = Expression<Func <Student, bool>>
var expressionTree = Expression.Lambda<Func<Student, bool>>(body, new[] { pe });
```

This can then be accessed in the following manner:

```cs
Console.WriteLine("Expression Tree: {0}", expressionTree); // Expression Tree: s => (s.Age >= 18)
    
Console.WriteLine("Expression Tree Body: {0}", expressionTree.Body); // Expression Tree Body: (s.Age >= 18)
    
Console.WriteLine("Number of Parameters in Expression Tree: {0}", 
                                expressionTree.Parameters.Count); // Number of Parameters in Expression Tree: 1
    
Console.WriteLine("Parameters in Expression Tree: {0}", expressionTree.Parameters[0]); // Parameters in Expression Tree: s
```

Note: the goal is not to generate a result but to generate an expression.

</div>
</div>

<div id="interview-threadparams"> 
  <button type="button" class="collapsible">+ Can a Thread have Parameters?<br/>
    <code class="ex">
Yes if thread delegate has a single object parameter.
Compiler automatically creates a ParameterizedThreadStarter.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
using System;
using System.Threading;

public class ThreadA
{
    long endTime;

    public ThreadA()
    {
        long startTime = DateTime.Now.Ticks;
        long deltaTime = TimeSpan.TicksPerSecond * 10;
        endTime = startTime + deltaTime;
    }

    // threadKiller is not required, but is added to give an
    // example of passing a delegate into a thread
    public void Run(Action<Exception> threadKiller)
    {
        while (true)
        {
            try
            {
                Thread.Sleep(1000); // wait 1 second for something to happen.

                DateTime now = DateTime.Now;

                Console.WriteLine(now.ToLongTimeString());

                if (now.Ticks > endTime) // what im waiting for...
                    threadKiller.Invoke(new OperationCanceledException());
            }
            catch
            {
                Console.WriteLine("Thread exited");
                break;
            }
        }
        //perform cleanup if there is any...
    }
}

class Program
{
    static void Main(string[] args)
    {
        FireThread();
    }

    private static void FireThread()
    {
        Action<Exception> threadKiller = (ex) =>
        {
            killTheThread(ex);
        };

        Thread thread = new Thread(startThread);
        thread.Start(threadKiller);
    }
    
    // specifying a single object as a parameter makes the
    // compiler use a ParameterizedThreadStarter, which
    // allows data to be passed to the thread.
    private static void startThread(object o)
    {
        Action<Exception> threadKiller = o as Action<Exception>;
        new ThreadA().Run(threadKiller);
    }

    private static void killTheThread(Exception ex)
    {
        throw ex;
    }
}
```

</div>
</div>

<div id="interview-overloadgeneric"> 
  <button type="button" class="collapsible">+ Can you overload a Generic Method?<br/>
    <code class="ex">
Yes - Method(), Method&lt;T&gt;(T t), Methodd&lt;T&gt;(T t, int i), Methodd&lt;T1, T2&gt;(T1 t1, T2 t2), etc.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
public class Dog
{
    public string Name { get; set; }
 
    public Dog(string name)
    {
        Name = name;
    }
 
    public void Bury(Bone b)
    {
        Console.WriteLine("{0} is burying: {1}", Name, b);
    }
 
    public void Bury(Lawyer l)
    {
        Console.WriteLine("{0} is burying: {1}", Name, l);
    }
 
    public void Bury<T>(T thing)
    {
        Console.WriteLine("{0} is burying: {1}", Name, thing);
    }
 
    public void Bury<T>(T thing, string msg)
    {
        Console.WriteLine("{0} : {1}", msg, thing);
    }
 
    public void Bury<T1, T2>(T1 thing1, T2 thing2)
    {
        Console.WriteLine("{0} is burying: {1}", Name, thing1);
        Console.WriteLine("{0} is burying: {1}", Name, thing2);
    }
}
```

```cs
Dog fido = new Dog("Fido");
 
fido.Bury(new Bone());
fido.Bury(new Lawyer());
fido.Bury<Cow>(new Cow("Bessie"));
fido.Bury<Lawyer>(new Lawyer(), "One less lawyer");
fido.Bury<Cow,Cat>(new Cow("Bessie"), new Cat("Puffy"));
```

</div>
</div>

<div id="interview-stopthread"> 
  <button type="button" class="collapsible">+ How can you stop a thread?<br/>
    <code class="ex">
Create global variable for thread to check
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
using System;
using System.Threading;

public class ThreadA
{
    long endTime;

    public ThreadA()
    {
        long startTime = DateTime.Now.Ticks;
        long deltaTime = TimeSpan.TicksPerSecond * 10;
        endTime = startTime + deltaTime;
    }

    // threadKiller is not required, but is added to give an
    // example of passing a delegate into a thread
    public void Run(Action<Exception> threadKiller)
    {
        while (true)
        {
            try
            {
                Thread.Sleep(1000); // wait 1 second for something to happen.

                DateTime now = DateTime.Now;

                Console.WriteLine(now.ToLongTimeString());

                if (now.Ticks > endTime) // what im waiting for...
                    threadKiller.Invoke(new OperationCanceledException());
            }
            catch
            {
                Console.WriteLine("Thread exited");
                break;
            }
        }
        //perform cleanup if there is any...
    }
}

class Program
{
    static void Main(string[] args)
    {
        FireThread();
    }

    private static void FireThread()
    {
        Action<Exception> threadKiller = (ex) =>
        {
            killTheThread(ex);
        };

        Thread thread = new Thread(startThread);
        thread.Start(threadKiller);
    }
    
    // specifying a single object as a parameter makes the
    // compiler use a ParameterizedThreadStarter, which
    // allows data to be passed to the thread.
    private static void startThread(object o)
    {
        Action<Exception> threadKiller = o as Action<Exception>;
        new ThreadA().Run(threadKiller);
    }

    private static void killTheThread(Exception ex)
    {
        throw ex;
    }
}
```

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="config">
<button type="button" class="collapsible">+ Configuration</button>
<div class="content" style="display: none;" markdown="1">

<div id="interview-gc"> 
  <button type="button" class="collapsible">+ How does Garbage Collection work?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-remoting"> 
  <button type="button" class="collapsible">+ What is .NET Remoting?<br/>
   <code class="ex">
Enables interprocess/domain communication (HTTP, TCP, and SMTP protocols)
Legacy feature.
Windows Communication Framework (WCF) is preferred (better performance, more flexible, HTTP, TCP, SMTP, named pipes, MSMQ)
   </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

1. Makes reference to remotable object available to a client application (using an Activation URL).
1. Client application instantiates it (by connecting to the URL) .
1. Client use the remotable object as if it were a local object, however the actual code execution happens at the server-side. 
1. Remoting runtime creates a listener for the object when the server registers the channel that is used to connect to the remotable object. 
1. At the client side, the remoting infrastructure creates a proxy that stands-in as a pseudo-instantiation of the remotable object. 
1. The client does not implement the functionality of the remotable object, but presents a similar interface. 
1. The remoting infrastructure needs to know the public interface of the remotable object beforehand. 
1. Any method calls made against the object, including the identity of the method and any parameters passed, are serialized to a byte stream and transferred over a communication protocol-dependent Channel to a recipient proxy object at the server side ("marshalled"), by writing to the Channel's transport sink.
1. At the server side, the proxy reads the stream off the sink and makes the call to the remotable object on the behalf of the client. 
1. The results are serialized and transferred over the sink to the client, where the proxy reads the result and hands it over to the calling application.
1. If the remotable object needs to make a callback to a client object for some services, the client application must mark it as remotable and have a remoting runtime host a listener for it.
1. The server can connect to it over a different Channel, or over the already existent one if the underlying connection supports bidirectional communication.
1. A channel can be composed of a number of different Channel objects, possibly with different heterogeneous transports. 
1. Remoting can also work across systems separated by an interconnection of heterogeneous networks, including the internet.
1. Type safety is enforced by the Common Type System and the .NET Remoting runtime. 
1. Remote method calls are inherently synchronous; asynchronous calls can be implemented using threading libraries. 
1. Authentication and access control can be implemented for clients by either using custom Channels or by hosting the remotable objects in IIS and then using the IIS authentication system.

</div>
</div>

<div id="interview-assemblyload"> 
  <button type="button" class="collapsible">+ When would you use `Assembly.LoadFrom()` or `Assembly.LoadslFile()`?<br/>
    <code class="ex">
LoadFrom: Searches for assembly, so could load wrong one (useful if don't know/care where assembly is)
LoadFile: Only loads from the specified path, so avoids risk of loading the wrong assembly.
   </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-strongnaming"> 
  <button type="button" class="collapsible">+ What are the benefits of Strongly Named Assemblies?<br/>
    <code class="ex">
Only strongly named assemblies can be included in GAC.
Creates a unique identifier for the assembly.
Slightly more secure than anonymous assemblies (will only access other strongly named assemblies).
Strong name verification can be disabled by user.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-cicd"> 
  <button type="button" class="collapsible">+ What is CI/CD?<br/>
    <code class="ex">
CI: Continuous Integration - every push triggers a build and then runs tests before changes are integrated into master.
CD: Continuous Deployment - CI + deploys new release build to customers.
   </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-cloud"> 
  <button type="button" class="collapsible">+ What are differences between Cloud and On-Premise?<br/>
    <code class="ex">
Cloud reduces complexity of testing and deploying app.
Cloud allows better data analysis (state + usage).
Cloud adds risk in terms of privacy and data protection.
Cloud means you are responsible for resources, rather than customer.
   </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dllvsexe"> 
  <button type="button" class="collapsible">+ What is the difference between an EXE and a DLL?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-gac"> 
  <button type="button" class="collapsible">+ What is the GAC?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-tddvsddd"> 
  <button type="button" class="collapsible">+ What are TDD and DDD?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-compilation"> 
  <button type="button" class="collapsible">+ How is C# compiled?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-serialization"> 
  <button type="button" class="collapsible">+ What is the difference between XML and Binary Serialization?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

-------------------------------------------------------------------------------------------------------

<div id="interview-mvc"> 
<button type="button" class="collapsible">+ MVC Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">
 
<div id="interview-getvspost"> 
  <button type="button" class="collapsible">+ What is the difference between GET and POST?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-controller"> 
  <button type="button" class="collapsible">+ In MVC, what is a Controller?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-requestflow"> 
  <button type="button" class="collapsible">+ In MVC, what is the Request Flow?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-mvcdesc"> 
  <button type="button" class="collapsible">+ What is MVC?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-viewvssession"> 
  <button type="button" class="collapsible">+ What is the difference between ViewState and SessionState?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-xsd"> 
  <button type="button" class="collapsible">+ What is an XSD file?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-xml"> 
  <button type="button" class="collapsible">+ What is the difference between an XML Fragment and an XML Document?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-cors"> 
  <button type="button" class="collapsible">+ What is CORS?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

<div id="interview-git"> 
<button type="button" class="collapsible">+ Git Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">
 
<div id="interview-gitreset"> 
  <button type="button" class="collapsible">+ What does `git reset` do?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-gitpush"> 
  <button type="button" class="collapsible">+ What does `git push origin master` do?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

<div id="interview-html"> 
<button type="button" class="collapsible">+ HTML Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">
 
<div id="interview-divspan"> 
  <button type="button" class="collapsible">+ What is the difference between Div and Span?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-htmlvscss"> 
  <button type="button" class="collapsible">+ Why is it a good idea to split HTML and CSS?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-classvsid"> 
  <button type="button" class="collapsible">+ What is the difference between Classes and Ids?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-marginvspadding"> 
  <button type="button" class="collapsible">+ What is the difference between Margin and Padding?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hyperlinks"> 
  <button type="button" class="collapsible">+ To which elements can a hyperlink be applied?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-doctype"> 
  <button type="button" class="collapsible">+ What is the significant of a DocType?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

<div id="interview-js"> 
<button type="button" class="collapsible">+ JavaScript Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">
 
<div id="interview-sessionvslocal"> 
  <button type="button" class="collapsible">+ What is the difference between Session Storage and Local Storage?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-strict"> 
  <button type="button" class="collapsible">+ What does Strict mean?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-nan"> 
  <button type="button" class="collapsible">+ What does NaN mean?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-timers"> 
  <button type="button" class="collapsible">+ How do Timers work?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-timers"> 
  <button type="button" class="collapsible">+ How can you enumerate data types?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-eventbubble"> 
  <button type="button" class="collapsible">+ How do you define Event Bubbling?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-eventbubble"> 
  <button type="button" class="collapsible">+ How do you define Event Bubbling?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-typescript"> 
  <button type="button" class="collapsible">+ What is the difference between TypeScript and JavaScript?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-casesensitive"> 
  <button type="button" class="collapsible">+ Is JavaScript Case Sensitive?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-objinheritance"> 
  <button type="button" class="collapsible">+ How does Object Inheritance work in JavaScript?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-this"> 
  <button type="button" class="collapsible">+ How does the `this` keyword work in JavaScript?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(also include notes from section on page 139, related to arrow functions)

</div>
</div>

<div id="interview-ajax"> 
  <button type="button" class="collapsible">+ What is Ajax?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-privatemembers"> 
  <button type="button" class="collapsible">+ Can you have private members in JavaScript?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(add notes from page 142, regarding true private methods)

</div>
</div>

<div id="interview-errors"> 
  <button type="button" class="collapsible">+ What are some types of JavaScript errors?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-arrays"> 
  <button type="button" class="collapsible">+ How can you empty an array?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hoisting"> 
  <button type="button" class="collapsible">+ What is Function Hoisting?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-deferred"> 
  <button type="button" class="collapsible">+ What is the Deferred Attribute?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-async"> 
  <button type="button" class="collapsible">+ What is the Async Attribute?<br/>
     <code class="ex">
xxxxxxxx
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-innerhtml"> 
  <button type="button" class="collapsible">+ What does `.innerHTML` do?<br/>
    <code class="ex">
Inserts free-form HTML into the DOM, requiring a complete rebuild of the parent element.
Reserve for large DOM changes (e.g. long lists).
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

As shown in the following example, using `.innerHTML` can result in cleaner code, however it can be expensive to run.

```js
myDiv.innerHTML += '<p class="paragraph" onclick="doSomething()">New Element</p>'
```

`.innerHTML` is best reserved for case where multiple changes must be made to the DOM (e.g. appending many items to a list):

```js
let newElements = ''; 
for (i = 0; i < 100; i++) { 
 newElements += `<p>New Element Number: ${i}</p>` 
} 
myDiv.innerHTML =+ newElements;
```

</div>
</div>

<div id="interview-appendchild"> 
  <button type="button" class="collapsible">+ What do `.createElement()` and `.appendChild()` do?<br/>
    <code class="ex">Add single elements to the DOM without requiring a complete rebuild.</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Using `.createElement()` and `.appendChild()` is far more efficient when doing small updates to the DOM.  

`.createElement()` is limited however, since it cannot add attributes to the element (e.g. classes or handlers).

```js
let newElement = document.createElement('p'); 
newElement.textContent = 'New Element'; 
myDiv.appendChild(newElement);
```

If multiple updates must be made to the DOM (e.g. updating a long list), using `.createElement()` and `.appendChild()` can be much less efficient that `.innerHTML`:

```js
for (i = 0; i < 100; i++) { 
 let newElement = document.createElement('p'); 
 newElement.textContent = 'New Element Number: ' + i;  
 div.appendChild(newElement); 
}
```

</div>
</div>

<div id="interview-eval"> 
  <button type="button" class="collapsible">+ What does `.eval()` do?<br/>
    <code class="ex">
It runs the interpreter, which is inefficient, and runs with elevated privileges, which can be dangerous.  Avoid.
If necessary, use `.Function()` instead, but other alternatives are preferable.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The main problem is that `.eval()` runs with the privileges of the caller, so in a server-side app, the caller could access features that are not permitted.

In client-side apps, `.eval()` is OK, although inefficient.

In server-side apps, it is a very bad idea unless you have complete control of what gets executed where.

An alternative is `.Function()`, which is both much faster and less insecure since it only runs in global scope (making it less likely to access something it shouldn't).

The best solution is to avoid whatever pattern is causing this type of function to be used.

For further information, see:
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval)

</div>
</div>

<div id="interview-hidecode"> 
  <button type="button" class="collapsible">+ How can you hide code?<br/>
    <code class="ex">
You can't!
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Do not use the following:

```html
<script language="javascript">
<!-- //
code here
//-->
</script>
```

</div>
</div>

</div>
</div>

<div id="interview-js"> 
<button type="button" class="collapsible">+ SQL Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">

<div id="interview-sqlcommands"> 
  <button type="button" class="collapsible">+ What are common SQL commands?<br/>
    <code class="ex">
SELECT, UPDATE, DELETE, INSERT INTO, CREATE DATABASE, ALTER DATABASE, CREATE TABLE, ALTER TABLE, DROP TABLE, CREATE INDEX, DROP INDEX
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

`SELECT` - extracts data from a database
`UPDATE` - updates data in a database
`DELETE` - deletes data from a database
`INSERT INTO` - inserts new data into a database
`CREATE DATABASE` - creates a new database
`ALTER DATABASE` - modifies a database
`CREATE TABLE` - creates a new table
`ALTER TABLE` - modifies a table
`DROP TABLE` - deletes a table
`CREATE INDEX` - creates an index (search key)
`DROP INDEX` - deletes an index

</div>
</div>

<div id="interview-sqlorder"> 
  <button type="button" class="collapsible">+ In what order should SQL commands be used?<br/>
    <code class="ex">
     SELECT 
     FROM 
     WHERE 
     GROUP BY 
     HAVING 
     ORDER BY
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

`WHERE` is used to filter **before** `GROUP BY`

`HAVING` is used to filter **after** `GROUP BY`

</div>
</div>

<div id="interview-sqljoin"> 
  <button type="button" class="collapsible">+ What are the different types of Join?<br/>
    <code class="ex">
(INNER) JOIN: Intersection only
LEFT (OUTER) JOIN: Intersection and Left only.
RIGHT (OUTER) JOIN: Intersection and Right only.
FULL (OUTER) JOIN : Everything.
SELF JOIN: Table is joined with itself.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Inner Join: "Select all rows from table1 and table2 where the column_name matches"

```sql
SELECT 
    column_name(s)
  FROM 
    table1
INNER JOIN 
    table2
  ON 
    table1.column_name = table2.column_name;
```

Left Join: "Select all rows from table1 plus those from table2 where the column_name matches a row in table1"

```sql
SELECT 
    column_name(s)
  FROM 
    table1
LEFT JOIN 
    table2
  ON 
    table1.column_name = table2.column_name;
```

Right Join: "Select all rows from table2 plus those from table1 where the column_name matches a row in table1"

```sql
SELECT 
    column_name(s)
  FROM 
    table1
RIGHT JOIN 
    table2
  ON 
    table1.column_name = table2.column_name;
```

Full Outer Join: "Select all rows from table1 or table2 where the column_name matches"

```sql
SELECT 
    column_name(s)
  FROM 
    table1
FULL OUTER JOIN 
    table2
  ON 
    table1.column_name = table2.column_name;
```

Self Join: "Select all rows from table1 where column_name1 does not match but column_name2 does match"

```sql
SELECT 
    column_name(s)
  FROM 
    table1 AS T1, // alias
    table1 AS T2  // alias
WHERE 
  T1.column_name1 <> T2.column_name1
AND 
  T1.column_name2 = T2.column_name2
```

</div>
</div>

<div id="interview-sqlcursor"> 
  <button type="button" class="collapsible">+ What is the SQL Cursor?<br/>
    <code class="ex">
Temporary work area containing select statement and rows to be acted on.
Effectively the same as a for/while loop (while has row, do something).
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

An SQL cursor is a temporary work area in memory where an SQL statement is executed.  The cursor knows the select statement and the rows of data accessed.

The cursor can hold multiple rows but can only access one row at a time.  The set of rows is called the Active Set.

The cursor effectively acts like a for/while loop, in that it can be used to iterate over a collection of rows.

A cursor is declared:

```sql
DECLARE 
  @person_id INT, 
  @name NVARCHAR(200);
DECLARE sample_cursor CURSOR 
FOR SELECT 
    person_id,
    name 
  FROM 
    company;
```

And used:

```sql
OPEN sample_cursor 
// get first row
FETCH NEXT FROM sample_cursor INTO 
  @person_id,
  @name; 
// while fetch is successful
WHILE @@FETCH_STATUS=0 
  BEGIN
    // do something
    
    // get next row
    FETCH NEXT FROM sample_cursor INTO 
      @person_id,
      @name;
  END; 
CLOSE sample_cursor; 
DEALLOCATE sample_cursor;
```

</div>
</div>

<div id="interview-frag"> 
  <button type="button" class="collapsible">+ What is Index Fragmentation?<br/>
    <code class="ex">
8KB pages of data no longer match logical order due to update actions.
Impact performance (Internal: unoptimized space; External: pages out of order).
5-30% = reorganize indexes.
>30% = rebuild indexes.
Base index keys on INSERT statements; don't update keys, don't use random keys; monitor database.
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

SQL databases have indexes that allow improved query performance.  There are two types:
  * Clustered Index: one index per table; determines physical order of data in table (rows are stored physically on disk in this order)
  * Non-Clustered Index: multiple indexes per table; essentially pointers to physical rows (additional indexes decrease performance)

In both cases, an index points to pages, which are the smallest unit of data in the database, with each page consisting of 8KB of data (for legacy reasons related to HDD disk block sizes).  In addition to data, each page contains pointers to the next and previous pages in the logical order.

Initially, the pages of data in a table will match the logical order of its sort keys and space will be optimized, however as actions are performed on the database (INSERT, UPDATE, DELETE) the pages will need to be split and moved around to accomodate new data.  This is what is termed Index Fragmentation.

There are two types of Index Fragmentation:
  * Internal: pages gain empty space as data is moved between pages, which increases the number of logical reads required.
  * External: the order of the pages no longer matches their logical sort order, which increases the number of physical reads required.
  
If fragmention is between 5-30%, the indexes should be reorganized (fix external fragmentation by re-ordering pages).

If fragmention is greater than 30%, the indexes should be rebuilt (fix both internal and external fragmentation by re-creating all pages from scratch).

To reduce fragmentation:
  * Choose index keys that suit most common INSERT statements.
  * Don't update index key columns.
  * Don't choose random key values.
  * Monitor and maintain the database.
</div>
</div>

</div>
</div>

&nbsp;

&nbsp;

&nbsp;

-------------------------------------------------------------------------------------------------------

**Move along; nothing to see here...**

<script type="text/javascript">

    const loadCSS = (filename) => { 

       const file = document.createElement("link");
       file.setAttribute("rel", "stylesheet");
       file.setAttribute("type", "text/css");
       file.setAttribute("href", filename);
       document.head.appendChild(file);
    };

    const loadJS = (filename) => { 

       const file = document.createElement("script");
       file.setAttribute("type", "text/javascript");
       file.setAttribute("src", filename);
       document.head.appendChild(file);
    };
   
    //just call a function to load your CSS
    //this path should be relative your HTML location
    loadCSS("../collapse.css");
    loadJS("../collapse.js");

</script>
