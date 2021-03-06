<div style="display: inline-block;">
<a class="link" href="http://oclipa.github.io/">&lt; home</a>
<a class="link" href="http://oclipa.github.io/toolbox.html">&lt; toolbox</a>
</div> 

## C# (work in progress...)

&nbsp;

<button type="button" id="toggle-all" value="none">Expand All Sections</button>

&nbsp;
<hr/>

<!-- =========================#####################################################================================ -->
<div id="stupid">
<button type="button" class="collapsible">+ Simple Stuff I Keep Forgetting</button>
<div class="content" style="display: none;" markdown="1">

<!-- =========================#####################################################================================ -->
<div id="stupid-vscode">
<button type="button" class="collapsible">+ Create a C# Console App in VSCode</button>
<div class="content" style="display: none;" markdown="1">

1. Create a folder
1. Open the folder in VSCode
1. Run the following command:
  - `dotnet new console`

**To run the app:**

Either,
   - F5
   
Or,
   - In the VSCode Terminal: 
      - `dotnet run`
   
**To compile a Release build:**

- `dotnet run -c Release`
   
</div>
</div>

<!-- =========================#####################################################================================ -->
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

<!-- =========================#####################################################================================ -->
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

<!-- =========================#####################################################================================ -->
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

<!-- =========================#####################################################================================ -->
<div id="stupid-switch">
<button type="button" class="collapsible">+ Switch Syntax</button>
<div class="content" style="display: none;" markdown="1">

NOTE: Once a case matches, **all** statements following that case (including other cases!) will be executed until a `break` or `return` statement is encountered.

It should also be noted, however, that leaving out `break` statements is generally considered bad practice.

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
                    // if there is no break statement
                    // both "15" and "20" will trigger 
                    // the "20" case
                case 20:
                    Console.WriteLine("Value of x is 15 or 20");
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

<!-- =========================#####################################################================================ -->
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

<!-- =========================#####################################################================================ -->
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

**Displaying Bytes**

To display the bytes for a number, use: `Convert.ToString(num, toBase: 2)`

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="stupid-json">
<button type="button" class="collapsible">+ Serialize to JSON</button>
<div class="content" style="display: none;" markdown="1">

```cs
using System;
using System.Text.Json;

public class Car
{
    public string Model
    {
        get { return "Volkswagon"; }
    }

    public string Make
    {
        get { return "Golf"; }
    }

    public CarDetails Details
    {
        get { return new CarDetails(); }
    }
}

public class CarDetails
{
    public int Year
    {
        get { return 2017; }
    }

    public float Price
    {
        get { return 20000f; }
    }

    public Condition Condition
    {
        get { return Condition.EXCELLENT; }
    }
}

public enum Condition
{
    EXCELLENT,
    GOOD,
    POOR
}

class Program
{
    static void Main()
    {
        Car car = new Car();
        var options = new JsonSerializerOptions { WriteIndented = true };
        Console.WriteLine(JsonSerializer.Serialize(car, typeof(Car), options));
        
        // Output:
        // {
        //     "Model": "Volkswagon",
        //     "Make": "Golf",
        //     "Details": {
        //         "Year": 2017,
        //         "Price": 20000,
        //         "Condition": 0
        //      }
        // }
    }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="stupid-parity">
<button type="button" class="collapsible">+ Checking for Parity</button>
<div class="content" style="display: none;" markdown="1">

Generally, the two fastest ways to check the parity of a number (whether it is even or odd) are the following:

**Using bitwise &amp;**

*This is normally the fastest method.*

Checks if the last binary digit of the number is 1 (in which case it is odd).

```cs
private static bool isEven(int i)
{
    return (i & 1) == 0;
}
```

**Testing the remainder**

*This can be easiest to read.*

Checks if there is any remainder after dividing by 2 (in which case it is odd).

```cs
private static bool isEven(int i)
{
    return (i % 2) == 0;
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="stupid-hashcode">
<button type="button" class="collapsible">+ Creating a Hash Code</button>
<div class="content" style="display: none;" markdown="1">

To achieve an even distribution of HashCodes, the following technique is generally used:
   * Combine the properties used to test for equality (i.e. in `Equals()`).
   * Add some prime numbers to improve the distribution.

There are several approaches to achieve this:

**Method 1: XOR and Primes**

```cs
public sealed class Point3D
{
    private readonly double x;
    private readonly double y;
    private readonly double z;
    private readonly ReadOnlyCollection<string> attrs;

    public Point3D(double x, double y, double z, IEnumerable<string> attrs)
    {
        this.x = x;
        this.y = y;
        this.z = z;
        this.attrs = new ReadOnlyCollection<string>(attrs.ToList());
    }

    public double X => this.x;
    public double Y => this.y;
    public double Z => this.z;
    public ReadOnlyCollection<string> Attrs => this.attrs;

    public override bool Equals(object other)
    {
        return other is Point3D p
            && p.X == X
            && p.Y == Y
            && p.Z == Z
            && p.Attrs == Attrs; // simplified for brevity
    }

    public override int GetHashCode()
    {
        unchecked // Allow arithmetic overflow, numbers will just "wrap around"
        {
            int hashcode = 1430287;
            hashcode = hashcode * 7302013 ^ X.GetHashCode();
            hashcode = hashcode * 7302013 ^ Y.GetHashCode();
            hashcode = hashcode * 7302013 ^ Z.GetHashCode();
            hashcode = hashcode * 7302013 ^ Attrs.GetHashCode();
            return hashcode;
        }
    }
}
```

**Method 2: Use a Tuple**

With the introduction of tuples in C# 7, this can be simplified to the following:

```cs
public sealed class Point3D
{
    private readonly double x;
    private readonly double y;
    private readonly double z;
    private readonly ReadOnlyCollection<string> attrs;

    public Point3D(double x, double y, double z, IEnumerable<string> attrs)
    {
        this.x = x;
        this.y = y;
        this.z = z;
        this.attrs = new ReadOnlyCollection<string>(attrs.ToList());
    }

    public double X => this.x;
    public double Y => this.y;
    public double Z => this.z;
    public ReadOnlyCollection<string> Attrs => this.attrs;

    public override bool Equals(object other)
    {
        return other is Point3D p
            && p.X == X
            && p.Y == Y
            && p.Z == Z
            && p.Attrs == Attrs; // simplified for brevity
    }

    public override int GetHashCode() => (X, Y, Z, Attrs).GetHashCode();
}
```

**Method 2: Helper Struct**

This following approach is taken from Rehan Saeed's "GetHasCode Made Easy":
  * https://rehansaeed.com/gethashcode-made-easy/

```cs
// MIT Licensed
// Copyright (c) 2019 Muhammad Rehan Saeed

// Permission is hereby granted, free of charge, to any person obtaining a copy
// of this software and associated documentation files (the "Software"), to deal
// in the Software without restriction, including without limitation the rights
// to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
// copies of the Software, and to permit persons to whom the Software is
// furnished to do so, subject to the following conditions:

// The above copyright notice and this permission notice shall be included in all
// copies or substantial portions of the Software.

// THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
// IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
// FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
// AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
// LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
// OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
// SOFTWARE.

/// <summary>
/// A hash code used to help with implementing <see cref="object.GetHashCode()"/>.
/// </summary>
public struct HashCode : IEquatable<HashCode>
{
    private const int EmptyCollectionPrimeNumber = 19;
    private readonly int value;

    /// <summary>
    /// Initializes a new instance of the <see cref="HashCode"/> struct.
    /// </summary>
    /// <param name="value">The value.</param>
    private HashCode(int value) => this.value = value;

    /// <summary>
    /// Performs an implicit conversion from <see cref="HashCode"/> to <see cref="int"/>.
    /// </summary>
    /// <param name="hashCode">The hash code.</param>
    /// <returns>The result of the conversion.</returns>
    public static implicit operator int(HashCode hashCode) => hashCode.value;

    /// <summary>
    /// Implements the operator ==.
    /// </summary>
    /// <param name="left">The left.</param>
    /// <param name="right">The right.</param>
    /// <returns>The result of the operator.</returns>
    public static bool operator ==(HashCode left, HashCode right) => left.Equals(right);

    /// <summary>
    /// Implements the operator !=.
    /// </summary>
    /// <param name="left">The left.</param>
    /// <param name="right">The right.</param>
    /// <returns>The result of the operator.</returns>
    public static bool operator !=(HashCode left, HashCode right) => !(left == right);

    /// <summary>
    /// Takes the hash code of the specified item.
    /// </summary>
    /// <typeparam name="T">The type of the item.</typeparam>
    /// <param name="item">The item.</param>
    /// <returns>The new hash code.</returns>
    public static HashCode Of<T>(T item) => new HashCode(GetHashCode(item));

    /// <summary>
    /// Takes the hash code of the specified items.
    /// </summary>
    /// <typeparam name="T">The type of the items.</typeparam>
    /// <param name="items">The collection.</param>
    /// <returns>The new hash code.</returns>
    public static HashCode OfEach<T>(IEnumerable<T> items) =>
        items == null ? new HashCode(0) : new HashCode(GetHashCode(items, 0));

    /// <summary>
    /// Adds the hash code of the specified item.
    /// </summary>
    /// <typeparam name="T">The type of the item.</typeparam>
    /// <param name="item">The item.</param>
    /// <returns>The new hash code.</returns>
    public HashCode And<T>(T item) => 
        new HashCode(CombineHashCodes(this.value, GetHashCode(item)));

    /// <summary>
    /// Adds the hash code of the specified items in the collection.
    /// </summary>
    /// <typeparam name="T">The type of the items.</typeparam>
    /// <param name="items">The collection.</param>
    /// <returns>The new hash code.</returns>
    public HashCode AndEach<T>(IEnumerable<T> items)
    {
        if (items == null)
        {
            return new HashCode(this.value);
        }

        return new HashCode(GetHashCode(items, this.value));
    }

    /// <inheritdoc />
    public bool Equals(HashCode other) => this.value.Equals(other.value);

    /// <inheritdoc />
    public override bool Equals(object obj)
    {
        if (obj is HashCode)
        {
            return this.Equals((HashCode)obj);
        }

        return false;
    }

    /// <summary>
    /// Throws <see cref="NotSupportedException" />.
    /// </summary>
    /// <returns>Does not return.</returns>
    /// <exception cref="NotSupportedException">Implicitly convert this struct to an <see cref="int" /> to get the hash code.</exception>
    [EditorBrowsable(EditorBrowsableState.Never)]
    public override int GetHashCode() =>
        throw new NotSupportedException(
            "Implicitly convert this struct to an int to get the hash code.");

    private static int CombineHashCodes(int h1, int h2)
    {
        unchecked
        {
            // Code copied from System.Tuple so it must be the best way to combine hash codes or at least a good one.
            return ((h1 << 5) + h1) ^ h2;
        }
    }

    private static int GetHashCode<T>(T item) => item?.GetHashCode() ?? 0;

    private static int GetHashCode<T>(IEnumerable<T> items, int startHashCode)
    {
        var temp = startHashCode;

        var enumerator = items.GetEnumerator();
        if (enumerator.MoveNext())
        {
            temp = CombineHashCodes(temp, GetHashCode(enumerator.Current));

            while (enumerator.MoveNext())
            {
                temp = CombineHashCodes(temp, GetHashCode(enumerator.Current));
            }
        }
        else
        {
            temp = CombineHashCodes(temp, EmptyCollectionPrimeNumber);
        }

        return temp;
    }
}
```

This can then be used in the following manner:

```cs
public sealed class Point3D
{
    private readonly double x;
    private readonly double y;
    private readonly double z;
    private readonly ReadOnlyCollection<string> attrs;

    public Point3D(double x, double y, double z, IEnumerable<string> attrs)
    {
        this.x = x;
        this.y = y;
        this.z = z;
        this.attrs = new ReadOnlyCollection<string>(attrs.ToList());
    }

    public double X => this.x;
    public double Y => this.y;
    public double Z => this.z;
    public ReadOnlyCollection<string> Attrs => this.attrs;

    public override bool Equals(object other)
    {
        return other is Point3D p
            && p.X == X
            && p.Y == Y
            && p.Z == Z
            && p.Attrs == Attrs; // simplified for brevity
    }

    public override int GetHashCode()
    {
        return HashCode
            .Of(this.X)
            .And(this.Y)
            .And(this.Z)
            .AndEach(this.Attrs);
    }
}
```

</div>
</div>

</div>
</div>

<hr/>

<!-- =========================#####################################################================================ -->
<div id="theory">
<button type="button" class="collapsible">+ Theory</button>
<div class="content" style="display: none;" markdown="1">
    
<!-- =========================#####################################################================================ -->
<div id="intro">
<button type="button" class="collapsible">+ What is C#?
<code class="ex">
C# is an object-oriented, type-safe, and managed language that is compiled by .NET Framework to generate Microsoft Intermediate Language.
</code>
</button>
<div class="content" style="display: none;" markdown="1">
    
</div>
</div>

<!-- =========================#####################################################================================ -->
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

<!-- =========================#####################################################================================ -->
<div id="interview-encapsulation"> 
  <button type="button" class="collapsible">+ Encapsulation<br/>
<code class="ex">
data + behaviour = class
</code>
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

<!-- =========================#####################################################================================ -->
<div id="interview-inheritance"> 
  <button type="button" class="collapsible">+ Inheritance<br/>
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

<!-- =========================#####################################################================================ -->
<div id="interview-polymorphism"> 
  <button type="button" class="collapsible">+ Polymorphism<br/>
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

<!-- =========================#####################################################================================ -->
<div id="interview-abstraction"> 
  <button type="button" class="collapsible">+ Abstraction<br/>
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

<!-- =========================#####################################################================================ -->
<div id="interview-classvsobj"> 
  <button type="button" class="collapsible">+ Class vs Object<br/>
<code class="ex">
Class = Definition of an object.
        
Object = Instantiation of an class.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-kiss"> 
  <button type="button" class="collapsible">+ KISS: Keep It Simple Stupid<br/>
<code class="ex">
Simple names and simple implementations are better than complex or obscure ones.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-dry"> 
  <button type="button" class="collapsible">+ DRY: Don't Repeat Yourself<br/>
<code class="ex">
Code in small pieces, and reuse the pieces.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-yagni"> 
  <button type="button" class="collapsible">+ YAGNI: You Ain't Gonna Need It<br/>
<code class="ex">
Don't include features "just in case".
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-tda"> 
  <button type="button" class="collapsible">+ TDA: Tell Don't Ask<br/>
<code class="ex">
Don't test an object's state and then make decisions about the methods to call.

Tell the object what you want to do and assume that it knows enough about its internal state to make the right decision.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-solid"> 
  <button type="button" class="collapsible">+ SOLID Principles<br/>
<code class="ex">
A principle is a goal, not a rule.

SRP: Single Responsibility Principle
OCP: Open-Close Principle
LSP: Liskov Substitution Principle
ISP: Interface Segregation Principle
DIP: Dependency Inversion Principle
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The SOLID principles are described in greater detail further down, however in summary:

**SRP: Single Responsibility Principle**

A class should have only one reason to change (one responsibility per class).

**OCP: Open-Close Principle**

Objects should be open for extension, but closed for modification (easy to extend implementation, but cannot be change base implementation).

**LSP: Liskov Substitution Principle**

Every sub-class should be substitutable for its super-class (a client should not need to know whether it is dealing with a sub-class or a super-class).

**ISP: Interface Segregation Principle**

A client should not be forced to depend on methods it does not use (a sub-class should not be forced to implement methods it does not use).

**DIP: Dependency Inversion Principle**

Entities must depend on abstractions not on concretions (a high level module should not depend on a low level module; they should both depend on abstractions).

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="srp">    
<button type="button" class="collapsible">+ SRP: Single Responsibility Principle
<code class="ex">
A class or function should have only one reason to change.

One responsibility per class/function, where "responsibility" means "a reason to change".

The responsibility should be entirely encapsulated by the class/function.
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

An example of code that *violates* SRP is the following:

```cs
using System;
using System.Collections.Generic;
using System.Linq;

public struct ValidatedOrder
{
    public ValidatedOrder(int customerId, int orderId, List<string> items, float price)
    {
        this.CustomerId = customerId;
        this.Id = orderId;
        this.Items = items;
        this.Price = price;
    }

    public int CustomerId;
    public int Id;
    public List<string> Items;
    public float Price;
}

// OrderManager Responsibility: Process orders
public class OrderManager
{
    private List<ValidatedOrder> orderCollection = new List<ValidatedOrder>();

    // OrderManager Responsibility 1: Validate the order
    public ValidatedOrder ValidateOrder(int customerId, int id)
    {
        //Code for validation 
        float price = 23.76f;        
        return new ValidatedOrder(customerId, id, new List<string>(), price);
    }
    
    // OrderManager Responsibility 2: Save the order
    public bool SaveOrder(ValidatedOrder order)
    {
        //Code for saving order 
        orderCollection.Add(order);
        return true;
    }

    // OrderManager Responsibility 3: Notify the customer
    public void NotifyCustomer(int customerId)
    {
        //Code for notification     
    }

    // OrderManager Responsibility 4: Produce report on orders
    public float SumOfAllCustomerOrders(int customerId)
    {
        // SumOfAllCustomerOrders Responsibility 1: Query orders    
        var orders = this.orderCollection.Where(c => c.CustomerId == customerId);
        
        // SumOfAllCustomerOrders Responsibility 2: Sum orders
        float sum = 0;
        foreach (ValidatedOrder order in orders)
        {
            sum += order.Price;
        }
        
        return sum;
    }
}

class Program
{
    static void Main()
    {
        int customerId = 2675376;
        int orderId = 157;

        OrderManager orderManager = new OrderManager();

        ValidatedOrder orderInfo = orderManager.ValidateOrder(customerId, orderId);

        orderManager.SaveOrder(orderInfo);

        orderManager.NotifyCustomer(customerId);

        float price = orderManager.SumOfAllCustomerOrders(customerId);

        Console.WriteLine($"Spent today: {price}");
    }
}
```

Note `OrderManager` does all of the following:
  1. `ValidateOrder`: Validating an order placed by customer and returns the final order
  1. `SaveOrder`: Saving an order placed by the customer and returns true/false
  1. `NotifyCustomer`: Notifies the customer order is placed

In addition, the `SumOfAllCustomerOrders()` method both queries the orders and processes the results.

To rectify this, the following changes might be made:

```cs
using System;
using System.Collections.Generic;
using System.Linq;

public struct ValidatedOrder
{
    public ValidatedOrder(int customerId, int orderId, List<string> items, float price)
    {
        this.CustomerId = customerId;
        this.Id = orderId;
        this.Items = items;
        this.Price = price;
    }

    public int CustomerId;
    public int Id;
    public List<string> Items;
    public float Price;
}

// OrderValidator Responsibility: Validate orders
public class OrderValidator
{
    // OrderValidator Responsibility 1: Validate the order
    public ValidatedOrder ValidateOrder(int customerId, int id)
    {
        //Code for validation 
        float price = 23.76f;

        return new ValidatedOrder(customerId, id, new List<string>(), price);
    }
}

// OrderDatabase Responsibility: Store order state
public class OrderDatabase
{
    private List<ValidatedOrder> orderCollection = new List<ValidatedOrder>();

    // OrderDatabase Responsibility 1: Set order state
    public bool SaveOrder(ValidatedOrder order)
    {
        //Code for saving order 
        orderCollection.Add(order);
        return true;
    }

    // OrderDatabase Responsibility 2: Get order state
    public IEnumerable<ValidatedOrder> GetOrders(int customerId)
    {
        return this.orderCollection.Where(c => c.CustomerId == customerId); ;
    }
}

// CustomerNotifier Responsibility: Notify customers
public class CustomerNotifier
{
    // CustomerNotifier Responsibility 1: Notify the customer
    public void NotifyCustomer(ValidatedOrder order)
    {
        //Code for notification     
    }
}

// OrderManager Responsibility: Process orders
public class OrderManager
{
    private readonly OrderValidator orderValidator;
    private readonly CustomerNotifier notifier;
    private readonly OrderDatabase database;

    public OrderManager(OrderValidator validator, CustomerNotifier notifier, OrderDatabase database)
    {
        this.orderValidator = validator;
        this.notifier = notifier;
        this.database = database;
    }

    // OrderManager Responsibility 1: Process an order to completion
    public bool ProcessOrder(int customerId, int orderId)
    {
        ValidatedOrder orderInfo = orderValidator.ValidateOrder(customerId, orderId);
        database.SaveOrder(orderInfo);
        notifier.NotifyCustomer(orderInfo);

        return true;
    }

    // OrderManager Responsibility 2: Produce report on orders
    public float SumOfAllCustomerOrders(int customerId)
    {
        var orders = database.GetOrders(customerId);

        float sum = 0;
        foreach (ValidatedOrder order in orders)
        {
            sum += order.Price;
        }
        return sum;
    }
}

class Program
{
    static void Main()
    {
        OrderValidator orderValidator = new OrderValidator();
        CustomerNotifier notifier = new CustomerNotifier();
        OrderDatabase database = new OrderDatabase();

        OrderManager orderManager = new OrderManager(orderValidator, notifier, database);

        int customerId = 2675376;
        int orderId = 157;

        if (orderManager.ProcessOrder(customerId, orderId))
        {
            float price = orderManager.SumOfAllCustomerOrders(customerId);

            Console.WriteLine($"Spent today: {price}");
        }
    }
}
```

As can be seen, each class and each method now has a single responsibility, which satisfies the Single Responsibility Principle.

**Rules of Thumb**

To determine if SRP is being violated, try the following:

  1. Try to write a one line description of the class or method, if the description contains words like "And, Or, But or If" then that is a problem.
    * For the violating example above: "An OrderManager class that validates orders, saves orders and notifies the customer"
  1. Does the class constructor or method take more than three arguments/parameters?
  1. Does the class or method implementation seem too long? ("too long" can be hard to pin down)
  1. Does the class have low cohesion? ("cohension" = the degree to which the elements inside a module belong together)

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-ocp"> 
  <button type="button" class="collapsible">+ OCP: Open-Close Principle<br/>
<code class="ex">
Objects should be open for extension, but closed for modification

It should be easy to extend an implementation, but it should not be possible to change the base implementation.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

An wall electrical socket is a good, real-world example of this principle.
  * Electrical devices are not attached directly to the mains, they are plugged into a standard wall socket.
  * The wall socket is always closed for modification (it cannot be changed once fitted).
  * The wall socket can be extended however, by either plugging in an extension board or by fitting an adaptor (e.g. USB adaptor).

For a code example, consider the following:

```cs
using System;

public enum AccountType
{
    Regular,
    Salary
}

public class SavingAccount
{
    private float balance;

    public SavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public float CalculateInterest(AccountType accountType)
    {
        float interest = 0;

        switch (accountType)
        {
            case AccountType.Regular:
                interest = balance * 0.04f;
                if (balance < 1000) interest -= balance * 0.02f;
                if (balance < 50000) interest += balance * 0.04f;
                break;
            case AccountType.Salary:
                interest = balance * 0.05f;
                break;
            default:
                throw new Exception("Unknown account type");
        }

        return interest;
    }
}

class Program
{
    static void Main()
    {
        float initialBalance = 10000f;

        SavingAccount acc = new SavingAccount(initialBalance);

        Console.WriteLine(acc.CalculateInterest(AccountType.Regular));
    }
}
```

In this example, the implementation is not following the Open-Closed Principle because, if tomorrow the bank introduces a new `AccountType`, the `CalculateInterest()` method is always at risk of modification.

As a side note, this method is also not following the Single Responsibility Principle since the `CalculateInterest()` method is doing more than one thing (it is calculating interest for more than one account type).

To avoid this, OCP can be applied to produce the following alternative:

```cs
using System;

public interface ISavingAccount
{
    float CalculateInterest();
}

public class RegularSavingAccount : ISavingAccount
{
    private float balance;

    public RegularSavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public float CalculateInterest()
    {
        float interest = balance * 0.04f;
        if (balance < 1000) interest -= balance * 0.02f;
        if (balance < 50000) interest += balance * 0.04f;

        return interest;
    }
}

public class SalarySavingAccount : ISavingAccount
{
    private float balance;

    public SalarySavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public float CalculateInterest()
    {
        return balance * 0.05f;
    }
}

class Program
{
    static void Main()
    {
        float initialBalance = 10000f;

        ISavingAccount acc = new RegularSavingAccount(initialBalance);

        Console.WriteLine(acc.CalculateInterest());
    }
}
```

In this case, there is no longer any need to modify the existing classes if a new account type is added; the new logic for the new account can be added by simply extending the functionality inherited from an interface.  This now satisfies the Open-Close Principle.

In addition, the Single Responsibility Principle is also satisfied since each class or function is only doing one task.

Note: An interface is created here just as an example. There could be an abstract class of SavingAccount that is implemented by a new savings account type.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-lsp"> 
  <button type="button" class="collapsible">+ LSP: Liskov Substitution Principle<br/>
<code class="ex">
Every sub-class should be substitutable for its super-class.

A client should not need to know whether it is dealing with a sub-class or a super-class.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

A real-world example of this principle - and its violation - is the act of replacing a light bulb.
  * A standard exists for light bulb socket types.
  * Assuming a new bulb meets the standard and provides the same illumination, the end user is not aware of whether the bulb is incandescent, flourescent or LED. This satisfies LSP.
  * If the illumination provided by the new bulb no longer meets the end user's expectations, this violates LSP.

A code example is the following:

```cs
using System;

public interface ISavingAccount
{
    bool CanWithdraw(float amount);
}

public class RegularSavingAccount : ISavingAccount
{
    private float balance;

    public RegularSavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public bool CanWithdraw(float amount)
    {
        float moneyAfterWithdrawal = balance - amount;
        if (moneyAfterWithdrawal >= 1000)
        {
            return true;
        }
        else
            return false;
    }
}

public class SalarySavingAccount : ISavingAccount
{
    private float balance;

    public SalarySavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public bool CanWithdraw(float amount)
    {
        float moneyAfterWithdrawal = balance - amount;
        if (moneyAfterWithdrawal >= 0)
        {
            return true;
        }
        else
            return false;
    }
}

public class FixDepositSavingAccount : ISavingAccount
{
    private float balance;

    public FixDepositSavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public bool CanWithdraw(float amount)
    {
        throw new Exception("Not supported by this account type");
    }
}

public class AccountManager
{
    public static void WithdrawFromAccount(ISavingAccount account, float amount)
    {
        try
        {
            if (account.CanWithdraw(amount))
                Console.WriteLine("Can withdraw");
            else
                Console.WriteLine("Cannot withdraw");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}

class Program
{
    static void Main()
    {
        float initialBalance = 10000f;
        float withdrawalAmount = 5000f;

        //works ok  
        AccountManager.WithdrawFromAccount(new RegularSavingAccount(initialBalance), withdrawalAmount);
        //works ok  
        AccountManager.WithdrawFromAccount(new SalarySavingAccount(initialBalance), withdrawalAmount);
        //throws exception as withdrawal is not supported  
        AccountManager.WithdrawFromAccount(new FixDepositSavingAccount(initialBalance), withdrawalAmount);
    }
}
```

In this example, the implementation is not following the Liskov Substitution Principle because `FixDepositSavingAccount` is modifying the functionality of the `CanWithdraw()` method

To avoid this, LSP can be applied to produce the following alternative:

```cs
using System;

public interface ISavingAccount
{
}

public abstract class SavingAccountWithWithdrawal : ISavingAccount
{
    public abstract bool CanWithdraw(float amount);
}

public abstract class SavingAccountWithoutWithdrawal : ISavingAccount
{
}

public class RegularSavingAccount : SavingAccountWithWithdrawal
{
    private float balance;

    public RegularSavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public override bool CanWithdraw(float amount)
    {
        float moneyAfterWithdrawal = balance - amount;
        if (moneyAfterWithdrawal >= 1000)
        {
            return true;
        }
        else
            return false;
    }
}

public class SalarySavingAccount : SavingAccountWithWithdrawal
{
    private float balance;

    public SalarySavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }

    public override bool CanWithdraw(float amount)
    {
        float moneyAfterWithdrawal = balance - amount;
        if (moneyAfterWithdrawal >= 0)
        {
            return true;
        }
        else
            return false;
    }
}

public class FixDepositSavingAccount : SavingAccountWithoutWithdrawal
{
    private float balance;

    public FixDepositSavingAccount(float initialBalance)
    {
        this.balance = initialBalance;
    }
}

public class AccountManager
{
    public static void WithdrawFromAccount(SavingAccountWithWithdrawal account, float amount)
    {
        try
        {
            if (account.CanWithdraw(amount))
                Console.WriteLine("Can withdraw");
            else
                Console.WriteLine("Cannot withdraw");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}

class Program
{
    static void Main()
    {
        float initialBalance = 10000f;
        float withdrawalAmount = 5000f;

        //works ok  
        AccountManager.WithdrawFromAccount(new RegularSavingAccount(initialBalance), withdrawalAmount);
        //works ok  
        AccountManager.WithdrawFromAccount(new SalarySavingAccount(initialBalance), withdrawalAmount);
        //compiler gives error  
        AccountManager.WithdrawFromAccount(new FixDepositSavingAccount(initialBalance), withdrawalAmount);
    }
}
```

After these changes, `FixDepositSavingAccount` is no longer able to produce unexpected behaviour, since it is constrained at compile-time.  This now satifies LSP.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-isp"> 
  <button type="button" class="collapsible">+ ISP: Interface Segregation Principle<br/>
<code class="ex">
A client should not be forced to depend on methods it does not use.

A sub-class should not be forced to implement methods it does not use.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The Interface Segregation Principle approaches a similar problem to that tackled by LSP, in that it is aimed at preventing code behaving in an unexpected manner.

In the case of LSP, the principle states that sub-classes should behave as expected based on their super-class.

In the case of ISP, the principle states that sub-classes should not be forced to implement methods that they do not use (which could again result in unexpected behaviour).

To satisfy ISP, it is better to implement many small interfaces rather than a one big interface.

A real-world example for ISP would be a dustbin:
   * A single general dustbin will end up with a mixture of different garbage types, which will make it hard to recycle.
   * Using several type-specific dustbins (e.g. paper, glass, metal) will make it much easier to recycle.

For a code example, consider the case of a bank with the following types of customers:
  * Corporate customer: For corporate people.
  * Retail customer: For individual, daily banking.
  * Potential customer: They are just a bank customer that does not yet hold a product of the bank and it is just a record that is different from corporate and retail.
  
The developer of a system defines the following interface for a customer:

<img src="assets/images/isp_violating_interface.jpg" />

Note that this interface forces the client class to implement methods that are not required, which violates ISP:
  * A potential customer, who does not yet hold any product, is forced to implement a CustomerProducts property.
  * A potential customer and a retail customer are both forced to have a CustomerStructure property, which only applies to a corporate customer.
  * A potential customer and a retail customer are both forced to implement a BusinessType, which only applies to a corporate customer.
  * A corporate customer and a potential customer are both forced to implement an Occupation property, which only applies to a retail customer.

In a case such as this, the solution is to split the interface into smaller, more targeted parts, such as in the following example:

<img src="assets/images/isp_satisfying_interfaces.jpg" />

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="ioc">    
<button type="button" class="collapsible">+ DIP: Dependency Inversion Principle 
<code class="ex">
Entities must depend on abstractions not on concretions.

A high level module should not depend on a low level module; they should both depend on abstractions.

Extending this principle leads to the Dependency Injection (DI) pattern.
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

<!-- =========================#####################################################================================ -->
<div id="ioc">    
<button type="button" class="collapsible">+ Inversion Of Control (IoC) Principle
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

<!-- =========================#####################################################================================ -->
<div id="dependency">    
<button type="button" class="collapsible">+ Dependency Injection (DI) Pattern
<code class="ex">
Secondary responsibilities are injected into a class, to avoid direct dependencies or unnecessary encapsulation.

Constructor Injection, Property Injection & Method Injection.

A refinement of DI is the Strategy pattern (ability to select algorithm at run-time)
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

<!-- =========================#####################################################================================ -->
<div id="strategy">    
<button type="button" class="collapsible">+ Strategy Pattern   
<code class="ex">
Allows algorithms to be selected at run-time.

The strategy pattern is intended to provide a means to define a family of algorithms, encapsulate each one as an object, and make them interchangeable. 

The strategy pattern lets the algorithms vary independently from clients that use them.

This is of particular relevance for the Dependency Injection pattern.
</code>
</button>    
<div class="content" style="display: none;" markdown="1">

This pattern allows algorithms to be selected a run-time, so that algorithms can vary indepentently from the clients that use them.

The Strategy pattern is of particular use when combined with the Dependency Injection pattern.

<img src="assets/images/strategy-design-pattern.png" />

**Advantages**

* More maintainable and readable (avoids switch, if, else...).
* Enables loose coupling between components.
* Easily extendable.

**Disadvantages**

* Clients must know of the existence of different strategies and must understand how the strategies differ.
* It increases the number of objects in the application. 

**Applicable When...***

This pattern is used when there are multiple similar classes that only differ in terms of how they execute the behavior.  As mentioned, this is of particular relevance when combined with the Dependency Injection pattern (where algorithms are "injected" into a client).

**Example: Accessing a Database**

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
            // NOTE: clients must be aware of the existance of the different DbAccessTypes,
            // which is a downside of the strategy pattern
            
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

<!-- =========================#####################################################================================ -->
<div id="interview-builder"> 
  <button type="button" class="collapsible">+ Builder Pattern<br/>
<code class="ex">
Separate the construction of a complex object from its representation so that the same construction process can create different representations.

Construct a complex object step by step and the final step returns the object. 

Also, the process of constructing an object should be generic so that it can be used to create different representations of the same object.

Similar to Factory pattern, but more related to enabling clients to create different representations of the same object.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

There are four main components to the Builder Pattern:

1. Builder: defines all the steps required to create a product.
1. ConcreteBuilder: implements or extends Builder.
1. Product: defines the object to be created.
1. Director: constructs an object using the Builder implementation.

<img src="assets/images/builder.png" />

**Advantages**

* More maintainable and readable
* Less prone to errors as we have a method which returns the finally constructed object.

**Disadvantages**

* Number of lines of code increases in builder pattern, but it makes sense as the effort pays off in terms of maintainability and readability.

**Applicable When...**

This pattern is chiefly of use when a constructor would otherwise have many arguments (particularly if some are optional).

**Example: Creating Toys**

```cs
using System;
using System.Text.Json;

// Defines the steps required to create a Toy
public interface IToyBuilder
{
    void SetModel();
    void SetHead();
    void SetLimbs();
    void SetBody();
    void SetLegs();
    Toy GetToy();
}

// Defines the object to be created
public class Toy
{
    public string Model
    {
        get;
        set;
    }
    public string Head
    {
        get;
        set;
    }
    public string Limbs
    {
        get;
        set;
    }
    public string Body
    {
        get;
        set;
    }
    public string Legs
    {
        get;
        set;
    }
}

// Builds Toy Model A
public class ToyABuilder : IToyBuilder
{
    Toy toy = new Toy();
    public void SetModel()
    {
        toy.Model = "TOY A";
    }
    public void SetHead()
    {
        toy.Head = "1";
    }
    public void SetLimbs()
    {
        toy.Limbs = "4";
    }
    public void SetBody()
    {
        toy.Body = "Plastic";
    }
    public void SetLegs()
    {
        toy.Legs = "2";
    }
    public Toy GetToy()
    {
        return toy;
    }
}

// Builds Toy Model B
public class ToyBBuilder : IToyBuilder
{
    Toy toy = new Toy();
    public void SetModel()
    {
        toy.Model = "TOY B";
    }
    public void SetHead()
    {
        toy.Head = "1";
    }
    public void SetLimbs()
    {
        toy.Limbs = "4";
    }
    public void SetBody()
    {
        toy.Body = "Steel";
    }
    public void SetLegs()
    {
        toy.Legs = "4";
    }
    public Toy GetToy()
    {
        return toy;
    }
}

// Manages the constructor of a Toy
public class ToyCreator
{
    private IToyBuilder _toyBuilder;
    public ToyCreator(IToyBuilder toyBuilder)
    {
        _toyBuilder = toyBuilder;
    }
    public void CreateToy()
    {
        _toyBuilder.SetModel();
        _toyBuilder.SetHead();
        _toyBuilder.SetLimbs();
        _toyBuilder.SetBody();
        _toyBuilder.SetLegs();
    }
    public Toy GetToy()
    {
        return _toyBuilder.GetToy();
    }
}

class Program
{
    static void Main()
    {
        Console.WriteLine("-------------------------------List Of Toys--------------------------------------------");
        var toyACreator = new ToyCreator(new ToyABuilder());
        toyACreator.CreateToy();
        Toy toyA = toyACreator.GetToy();
        Console.WriteLine(JsonSerializer.Serialize(toyA));

        var toyBCreator = new ToyCreator(new ToyBBuilder());
        toyBCreator.CreateToy();
        Toy toyB = toyBCreator.GetToy();
        Console.WriteLine(JsonSerializer.Serialize(toyB));
    }
}
```
</div>
</div>
 
<!-- =========================#####################################################================================ -->
<div id="interview-builder"> 
  <button type="button" class="collapsible">+ Factory Method Pattern<br/>
<code class="ex">
Allows classes to be created without client needing to know how to do it.

Similar to Builder pattern, but more related to enabling clients to create multiple different, but related, objects.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

There are four main components to the Factory Method Pattern:

1. Product: defines the the objects that factory method creates.
1. ConcreteProduct: implements Product.
1. Creator: declares the factory method (may also declare a default implementation).
1. ConcreteCreator: implements or extends Creator and overrides the factory method to returns instances of ConcreteProduct.

<img src="assets/images/factory.png" />

**Advantages**

* Enables loose coupling between components.
* Easily extendable.

**Disadvantages**

* Clients must know of the existence of different factories and must understand how the factories differ.
* It increases the number of objects in the application. 

**Applicable When...**

This pattern can be used whenever a client needs to create more than a single object.

**Example: Creating Vehicles**

```cs
using System;
using System.Collections.Generic;

// Defines the product
abstract class Vehicle
{
    public abstract string Marque { get; }
    public abstract string Model { get; }
}

// Defines a specific type of product
class Car : Vehicle
{
    private string _marque;
    private string _model;

    public Car(string marque, string model)
    {
        _marque = marque;
        _model = model;
    }

    public override string Marque
    {
        get { return _marque; }
    }

    public override string Model
    {
        get { return _model; }
    }
}

// Defines a specific type of product
class MotorCycle : Vehicle
{
    private string _marque;
    private string _model;

    public MotorCycle(string marque, string model)
    {
        _marque = marque;
        _model = model;
    }

    public override string Marque
    {
        get { return _marque; }
    }

    public override string Model
    {
        get { return _model; }
    }
}

// Defines the factory method
abstract class VehicleFactory
{
    public abstract Vehicle GetVehicle();
}

// Defines the factory for a specific product type
class CarFactory : VehicleFactory
{
    private string _marque;
    private string _model;

    public CarFactory(string marque, string model)
    {
        _marque = marque;
        _model = model;
    }

    public override Vehicle GetVehicle()
    {
        return new Car(_marque, _model);
    }
}

// Defines the factory for a specific product type
class MotorCycleFactory : VehicleFactory
{
    private string _marque;
    private string _model;

    public MotorCycleFactory(string marque, string model)
    {
        _marque = marque;
        _model = model;
    }

    public override Vehicle GetVehicle()
    {
        return new MotorCycle(_marque, _model);
    }
}

class Program
{
    static void Main()
    {
        VehicleFactory factory = null;
        string vehicleType = "car";

        switch (vehicleType.ToLower())
        {
            case "car":
                factory = new CarFactory("Honda", "Civic");
                break;
            case "motorcycle":
                factory = new MotorCycleFactory("Honda", "VFR800F");
                break;
            default:
                break;
        }

        Vehicle vehicle = factory.GetVehicle();
        Console.WriteLine("\nYour vehicle details are below : \n");
        Console.WriteLine($"Marque: {vehicle.Marque}\nModel: {vehicle.Model}");
    }
}
```
</div>
</div>
  
<!-- =========================#####################################################================================ -->
<div id="interview-decorator"> 
  <button type="button" class="collapsible">+ Decorator Pattern<br/>
<code class="ex">
An alternative to sub-classing for extending functionality dynamically.

Wrap components to override or extend functionality.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The idea of the Decorator Pattern is to wrap an existing class, add other functionality to it, then expose the same interface to the outside world. Because of this our decorator exactly looks like the original class to the people who are using it.

It is used to extend or alter the functionality at run-time. It does this by wrapping them in an object of the decorator class without modifying the original object. So it can be called a wrapper pattern.

There are four components to the Decorator Pattern:

1. Component: defines the existing API for the object that needs to be extended.
1. ConcreteComponent: implements or extends Component and defines the object to be extended.
1. Decorator: defines all of the functionalities that can be added to ConcreteComponent.
1. ConcreteDecorator: implements ONE of the functionaties that need to be added to ConcreteComponent.

<img src="assets/images/decorator.png" />

**Advantages**

* Adds functionality to existing objects dynamically
* Alternative to sub-classing
* Flexible design
* Supports Open-Closed Principle

**Disadvantages**

* Number of lines of code increases in builder pattern, but it makes sense as the effort pays off in terms of maintainability and readability.

**Applicable When...**

This pattern is particularly of use in the following situations:

* Adding functionality to a legacy system.
* Adding functionality to a control.
* Adding functionality to sealed classes.

**Example 1: Aggregating Features &amp; Cost**

```cs
using System;

// Component: defines the functionality  
public interface ICar
{
    string GetDescription();
    double GetCost();
}

// ConcreteComponent: defines an object that implements Component
public class EconomyCar : ICar
{
    public string GetDescription()
    {
        return "Economy Car";
    }

    public double GetCost()
    {
        return 450000.0;
    }
}

// ConcreteComponent: defines another object that implements Component
public class DeluxeCar : ICar
{
    public string GetDescription()
    {
        return "Deluxe Car";
    }

    public double GetCost()
    {
        return 750000.0;
    }
}

// ConcreteComponent: defines another object that implements Component
public class LuxuryCar : ICar
{
    public string GetDescription()
    {
        return "Luxury Car";
    }

    public double GetCost()
    {
        return 1000000.0;
    }
}

// Decorator: Defines the decorator wrapper than overrides or extends the Component functionality. 
public abstract class CarAccessoriesDecorator : ICar
{
    private ICar _car;

    public CarAccessoriesDecorator(ICar aCar)
    {
        this._car = aCar;
    }

    public virtual string GetDescription()
    {
        return this._car.GetDescription();
    }

    public virtual double GetCost()
    {
        return this._car.GetCost();
    }
}

// ConcreteDecorator: Overrides the Component functionality. 
public class BasicAccessories : CarAccessoriesDecorator
{
    public BasicAccessories(ICar aCar)
        : base(aCar)
    {
    }

    public override string GetDescription()
    {
        return base.GetDescription() + ", Basic Accessories Package";

    }

    public override double GetCost()
    {
        return base.GetCost() + 2000.0;
    }
}

// ConcreteDecorator: Overrides the Component functionality.   
public class AdvancedAccessories : CarAccessoriesDecorator
{
    public AdvancedAccessories(ICar aCar)
        : base(aCar)
    {
    }

    public override string GetDescription()
    {
        return base.GetDescription() + ", Advanced Accessories Package";
    }

    public override double GetCost()
    {
        return base.GetCost() + 10000.0;
    }
}

// ConcreteDecorator: Overrides or extends the Component functionality.     
public class SportsAccessories : CarAccessoriesDecorator
{
    public SportsAccessories(ICar aCar)
        : base(aCar)
    {
    }

    public override string GetDescription()
    {
        return base.GetDescription() + ", Sports Accessories Package";
    }

    public override double GetCost()
    {
        return base.GetCost() + 15000.0;
    }
}

class Program
{
    static void Main()
    {
        // Create EcomomyCar instance.   
        ICar objCar = new EconomyCar();

        // Wrap EconomyCar instance with BasicAccessories.   
        CarAccessoriesDecorator objAccessoriesDecorator = new BasicAccessories(objCar);

        // Wrap EconomyCar instance with AdvancedAccessories instance.   
        objAccessoriesDecorator = new AdvancedAccessories(objAccessoriesDecorator);

        Console.WriteLine("Car Details: " + objAccessoriesDecorator.GetDescription());
        Console.WriteLine("Total Price: " + objAccessoriesDecorator.GetCost());
    }
}
```

**Example 2: Maintaining an Audit Trail**

```cs
using System;
using System.Collections.Generic;

// Component: defines the base functionality  
abstract class RestaurantDish
{
    public abstract void Display();
}

// ConcreteComponent: defines an object that implements Component
class FreshSalad : RestaurantDish
{
    private string _greens;
    private string _cheese; //I am going to use this pun everywhere I can
    private string _dressing;

    public FreshSalad(string greens, string cheese, string dressing)
    {
        _greens = greens;
        _cheese = cheese;
        _dressing = dressing;
    }

    public override void Display()
    {
        Console.WriteLine("\nFresh Salad:");
        Console.WriteLine(" Greens: {0}", _greens);
        Console.WriteLine(" Cheese: {0}", _cheese);
        Console.WriteLine(" Dressing: {0}", _dressing);
    }
}

// ConcreteComponent: defines another object that implements Component
class Pasta : RestaurantDish
{
    private string _pastaType;
    private string _sauce;

    public Pasta(string pastaType, string sauce)
    {
        _pastaType = pastaType;
        _sauce = sauce;
    }

    public override void Display()
    {
        Console.WriteLine("\nClassic Pasta:");
        Console.WriteLine(" Pasta: {0}", _pastaType);
        Console.WriteLine(" Sauce: {0}", _sauce);
    }
}

// Decorator: Defines the decorator wrapper than overrides or extends the Component functionality. 
abstract class Decorator : RestaurantDish
{
    protected RestaurantDish _dish;

    public Decorator(RestaurantDish dish)
    {
        _dish = dish;
    }

    public override void Display()
    {
        _dish.Display();
    }
}

// ConcreteDecorator: Extends the Component functionality.   
class Available : Decorator
{
    public int NumAvailable { get; set; } //How many can we make?
    protected List<string> customers = new List<string>();
    public Available(RestaurantDish dish, int numAvailable) : base(dish)
    {
        NumAvailable = numAvailable;
    }

    public void OrderItem(string name)
    {
        if (NumAvailable > 0)
        {
            customers.Add(name);
            NumAvailable--;
        }
        else
        {
            Console.WriteLine("\nNot enough ingredients for " + name + "'s order!");
        }
    }

    public override void Display()
    {
        base.Display();

        foreach (var customer in customers)
        {
            Console.WriteLine("Ordered by " + customer);
        }
    }
}

class Program
{
    static void Main()
    {
        //Step 1: Define some dishes, and how many of each we can make
        FreshSalad caesarSalad = new FreshSalad("Crisp romaine lettuce", "Freshly-grated Parmesan cheese", "House-made Caesar dressing");
        caesarSalad.Display();

        Pasta fettuccineAlfredo = new Pasta("Fresh-made daily pasta", "Creamly garlic alfredo sauce");
        fettuccineAlfredo.Display();

        Console.WriteLine("\nMaking these dishes available.");

        //Step 2: Decorate the dishes; now if we attempt to order them once we're out of ingredients, we can notify the customer
        Available caesarAvailable = new Available(caesarSalad, 3);
        Available alfredoAvailable = new Available(fettuccineAlfredo, 4);

        //Step 3: Order a bunch of dishes
        caesarAvailable.OrderItem("John");
        caesarAvailable.OrderItem("Sally");
        caesarAvailable.OrderItem("Manush");

        alfredoAvailable.OrderItem("Sally");
        alfredoAvailable.OrderItem("Francis");
        alfredoAvailable.OrderItem("Venkat");
        alfredoAvailable.OrderItem("Diana");
        alfredoAvailable.OrderItem("Dennis"); //There won't be enough for this order.

        caesarAvailable.Display();
        alfredoAvailable.Display();
    }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-chainofreponse"> 
  <button type="button" class="collapsible">+ Chain of Responsibility Pattern<br/>
<code class="ex">
Used when one of many callers might take action on an object (e.g. a chain of approvals).

Each actor is represented by a handler, for which there is a successor.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

There are four components to the Chain of Responsibility Pattern:

1. Client: generates the request and passes it to the first Handler.
1. Handler: Defines the actor and includes a member that holds the next Handler. 
1. ConcreteHandlerA/ConcreteHandlerB: each Handler implementation contains functionality to handle some request and then pass responsibility to the next in the chain.

<img src="assets/images/chainofresponsibility.png" />

**Advantages**

* Avoids coupling the sender to the receiver.

**Disadvantages**

* ?

**Applicable When...**

Some cases when this pattern is useful:

1. Seeking approvals (Team Lead &gt; Project Lead &gt; Delivery Manager &gt; Director)
1. Triaging issues (Level &gt; Level 1 &gt; Level 2 &gt; Level 3)

Try/catch statements are also an example of this.

**Example: ATM Machine**

```cs
using System;

public abstract class Handler
{
    public Handler nextHandler;

    public void NextHandler(Handler moneyHandler)
    {
        this.nextHandler = moneyHandler;
    }

    public abstract void DispatchMoney(long requestedAmount);

    protected void outputMoney(long requestedAmount, long divisor, string handlerName)
    {
        long numberofNotesToBeDispatched = requestedAmount / divisor;

        if (numberofNotesToBeDispatched > 0)
        {
            string notes = numberofNotesToBeDispatched > 1 ? "notes are" : "note is";
            Console.WriteLine($"{numberofNotesToBeDispatched} x {divisor} {notes} dispatched by {handlerName}");
        }

        long pendingAmountToBeProcessed = requestedAmount % divisor;

        if (pendingAmountToBeProcessed > 0)
            nextHandler.DispatchMoney(pendingAmountToBeProcessed);
    }
}

public class TwoThousandHandler : Handler
{
    public override void DispatchMoney(long requestedAmount)
    {
        outputMoney(requestedAmount, 2000, "TwoThousandHandler");
    }
}

public class FiveHundredHandler : Handler
{
    public override void DispatchMoney(long requestedAmount)
    {
        outputMoney(requestedAmount, 500, "FiveHundredHandler");
    }
}

public class TwoHundredHandler : Handler
{
    public override void DispatchMoney(long requestedAmount)
    {
        outputMoney(requestedAmount, 200, "TwoHundredHandler");
    }
}

public class HundredHandler : Handler
{
    public override void DispatchMoney(long requestedAmount)
    {
        outputMoney(requestedAmount, 100, "HundredHandler");
    }
}

public class ATM
{
    private TwoThousandHandler twoThousandHandler = new TwoThousandHandler();
    private FiveHundredHandler fiveHundredHandler = new FiveHundredHandler();
    private TwoHundredHandler twoHundredHandler = new TwoHundredHandler();
    private HundredHandler hundredHandler = new HundredHandler();

    public ATM()
    {
        // Prepare the chain of Handlers
        twoThousandHandler.NextHandler(fiveHundredHandler);
        fiveHundredHandler.NextHandler(twoHundredHandler);
        twoHundredHandler.NextHandler(hundredHandler);
    }

    public void Withdraw(long requestedAmount)
    {
        twoThousandHandler.DispatchMoney(requestedAmount);
    }
}

class Program
{
    static void Main()
    {
        ATM atm = new ATM();

        Console.WriteLine("\n Requested Amount 4600");
        atm.Withdraw(4600);

        Console.WriteLine("\n Requested Amount 1900");
        atm.Withdraw(1900);

        Console.WriteLine("\n Requested Amount 600");
        atm.Withdraw(600);
    }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-adapter"> 
  <button type="button" class="collapsible">+ Adapter Pattern<br/>
<code class="ex">
Allows communication between two incompatible interfaces by acting as a bridge.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

This pattern involves a single class called adapter which is responsible for communication between two independent or incompatible interfaces.

There are four main components to the Adapter Pattern:

1. ITarget: defines the request the client wants to make.
1. Adapter: implements ITarget and inherits the Adaptee class, and translates the request for the incompatible code.
1. Adaptee: contains the incompatible code.
1. Client: wants to access the incompatible code.

<img src="assets/images/adapter.png" />

**Advantages**

* More maintainable and readable
* Supports the Open-Closed Principle (can add new adapters without disturbing existing client logic)
* Less prone to errors as we have a method which returns the finally constructed object.

**Disadvantages**

* Number of lines of code increases in the Adapter pattern, but it makes sense as the effort pays off in terms of maintainability and readability.

**Applicable When...**

This is typically used when a new system needs to communicate with an existing, independent system.

**Example**

```cs
using System;
using System.Collections.Generic;

// Define the request that the Client wishes to make 
public interface ITarget
{
    List<string> GetResponses();
}

// Translate the client's request to a form the adaptee understands
public class Adapter : ITarget
{
    public List<string> GetResponses()
    {
        return new ResponsesStore().GetResponsesRecieved();
    }
}

// The adaptee
public class ResponsesStore
{
    public List<string> GetResponsesRecieved()
    {
        var responses = new List<string>() {
            "This is a test response by user 1",
            "This is a test response by user 2",
            "This is a test response by user 3",
            "This is a test response by user 4"
        };
        return responses;
    }
}

// The client
public class Client
{
    private ITarget _target;

    public Client(ITarget target)
    {
        _target = target;
    }

    public List<string> GetResponsesRecieved()
    {
        return _target.GetResponses();
    }
}

class Program
{
    static void Main()
    {
        var client = new Client(new Adapter());
        var userResponses = client.GetResponsesRecieved();
        userResponses.ForEach(p => Console.WriteLine(p));
    }
}
```
</div>
</div>
 
<!-- =========================#####################################################================================ -->
<div id="interview-iterator"> 
  <button type="button" class="collapsible">+ Iterator Pattern<br/>
<code class="ex">
Iterator Design Pattern provides a way to access the elements of a collection object in a sequential manner without knowing its underlying structure.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The basic Iterator API allows a client to try to get the next object in a collection.

There are five components to this pattern:

1. Client: the class that contains a collection of objects, each of which can be retrieved using a Next operation.
1. Iterator: defines operators for accessing the collection elements in sequence.
1. ConcreteIterator: implements or extends Iterator.
1. Aggregate: defines an operation to create an Iterator.
1. ConcreteAggregate: implements of extends Aggregate.

<img src="assets/images/iterator-design-pattern.png" />

IEnumerable implementations are an example of this.

**Advantages**

* Client doesn't need to worry about implementation details of accessing a collection.

**Disadvantages**

* ????

**Applicable When...**

1. Allows accessing the elements of a collection object in a sequential manner without knowing its underlying structure.
1. Multiple or concurrent iterations are required over collections elements.
1. Provides a uniform interface for accessing the collection elements.

**Example**

```cs
using System;
using System.Collections;

// the client wishes to access a collection of objects
public class CollectionProcessor
{
    private IterableCollection collection;

    public CollectionProcessor()
    {
        // client has access to a collection
        this.collection = new IterableCollection();
        this.collection.Add("One");
        this.collection.Add("Two");
        this.collection.Add("Three");
        this.collection.Add("Four");
        this.collection.Add("Five");
    }

    // client iterates over contents of collection
    public void ProcessCollection()
    {
        Iterator iterator = collection.CreateIterator();
        while (iterator.Next())
        {
            string item = (string)iterator.Current;
            Console.WriteLine(item);
        }
    }
}

// defines a collection that provides an Iterator to itself
public interface IIterableCollection
{
    Iterator CreateIterator();
}

// a collection that provides an Iterator to itself
public class IterableCollection : IIterableCollection
{
    private ArrayList items = new ArrayList();

    public Iterator CreateIterator()
    {
        return new ConcreteIterator(this);
    }

    public object this[int index]
    {
        get { return items[index]; }
    }

    public int Count
    {
        get { return items.Count; }
    }

    public void Add(object o)
    {
        items.Add(o);
    }
}

// defines operators for accessing elements of a collection
public interface Iterator
{
    object Current { get; }
    bool Next();
}

// provides operators for accessing elements of a collection
public class ConcreteIterator : Iterator
{
    private IterableCollection collection;
    int index;

    public ConcreteIterator(IterableCollection collection)
    {
        this.collection = collection;
        index = -1;
    }

    public bool Next()
    {
        index++;
        return index < collection.Count;
    }

    public object Current
    {
        get
        {
            if (index < collection.Count)
                return collection[index];
            else
                throw new InvalidOperationException();
        }
    }
}

class Program
{
    static void Main()
    {
        CollectionProcessor client = new CollectionProcessor();
        client.ProcessCollection();
    }
}
```
</div>
</div>
 
<!-- =========================#####################################################================================ -->
<div id="interview-nullobject"> 
  <button type="button" class="collapsible">+ Null Object Pattern<br/>
<code class="ex">
Provides a non-functional object in place of a null reference and therefore allows methods to be called on it.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

**Advantages**

* Helps avoids null checks, which leads to cleaner code.

**Disadvantages**

* Developers can be unaware the pattern is being used, which can lead to unnecesary null checks.

**Applicable When...**

The Null Pattern is helpful in situations where we want to return an object of the expected type, yet do nothing.

**Example**

```cs
using System;

public interface IMobile
{
    void TurnOn();
    void TurnOff();
}

public abstract class AbstractPhone : IMobile
{
    protected string phoneType;

    public void TurnOff()
    {
        Console.WriteLine($"{phoneType} Turned OFF!");
    }

    public void TurnOn()
    {
        Console.WriteLine($"{phoneType} Turned ON!");
    }
}

public class SamsungGalaxy : AbstractPhone
{
    public SamsungGalaxy() { this.phoneType = "Samsung Galaxy"; }
}

public class SonyXperia : AbstractPhone
{
    public SonyXperia() { this.phoneType = "Sony Xperia"; }
}

public class AppleIPhone : AbstractPhone
{
    public AppleIPhone() { this.phoneType = "Apple iPhone"; }
}

//our null object class implementing IMobile interface as a singleton  
public class NullMobile : IMobile
{
    private static NullMobile _instance;
    private NullMobile()
    { }

    public static NullMobile Instance
    {
        get
        {
            if (_instance == null)
                _instance = new NullMobile();
            return _instance;
        }
    }

    //do nothing methods  
    public void TurnOff()
    { }

    public void TurnOn()
    { }
}

public class MobileRepository
{
    public IMobile GetMobileByName(string mobileName)
    {
        IMobile mobile = NullMobile.Instance;
        switch (mobileName)
        {
            case "sony":
                mobile = new SonyXperia();
                break;

            case "apple":
                mobile = new AppleIPhone();
                break;

            case "samsung":
                mobile = new SamsungGalaxy();
                break;
        }
        return mobile;
    }
}

class Program
{
    static void Main()
    {
        MobileRepository repo = new MobileRepository();

        repo.GetMobileByName("sony").TurnOn();
        repo.GetMobileByName("sony").TurnOff();

        repo.GetMobileByName("windows").TurnOn();
        repo.GetMobileByName("windows").TurnOff();
    }
}
```
</div>
</div>
 
<!-- =========================#####################################################================================ -->
<div id="interview-visitor"> 
  <button type="button" class="collapsible">+ Visitor Pattern<br/>
<code class="ex">
Create and perform new operations on a set of objects without changing the object structure or classes.

Used to separate business logic and algorithms from an object's data structure.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The Visitor Pattern is used to separate business logic and algorithms from an object's data structure.  This separation means that new logic can be added without changing the data structure, and vice versa.

The pattern has several components:

1. Client: has access to the ObjectStructure objects and can instruct them to accept a Visitor to perform the appropriate operations.
1. ObjectStructure: holds all of the Elements that can be used by visitors. 
1. Element: defines a method that can accept a Visitor.
1. ConcreteElement: the object that accepts visits by a Visitor.
1. Visitor: defines a method that can visit (perform an action) on an Element.
1. ConcreteVisitor: the object that contains the logic for the action to be performed on an Element.

<img src="assets/images/visitor-design-pattern.png" />

At first glance the pattern can appear complex, however at its core it enables the following:

1. A visitor object contains logic to be applied to ("visited upon") some data.
1. A data object indicates that it can accept a visit from a visitor object.
1. The visitor visits the data objects that can accept it and applies the logic to the data objects.

**Advantages**

* Loose coupling and the addition of new operations without changing the existing structure.

**Disadvantages**

* Can be complex and can have narrow applicability.

**Applicable When...**

This pattern is of particularly use in the following scenarios:
1. There are many unrelated operations that could be performed on an object.
1. New operations need to be performed on an object without changing it.
1. Operations need to be performed on the concrete class rather than on its abstraction.

**Example**

```cs
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // initialize a list of employees (elements)
        Employees e = new Employees();
        e.Attach(new Clerk());
        e.Attach(new Director());
        e.Attach(new President());

        // apply logic (visitors) to employees
        e.Accept(new IncomeVisitor());
        e.Accept(new VacationVisitor());
    }
}

#region Visitor Implementation

// defines a method that can visit (perform an action) on an element. 
interface IVisitor
{
    void Visit(Element element);
}

// a concrete visitor that can raise an employee's income
class IncomeVisitor : IVisitor
{
    public void Visit(Element element)
    {
        Employee employee = element as Employee;

        // Provide 10% pay raise
        employee.Income *= 1.10;
        Console.WriteLine("{0} {1}'s new income: {2:C}",
          employee.GetType().Name, employee.Name,
          employee.Income);
    }
}

// a concrete visitor that can raise an employee's vacation allowance
class VacationVisitor : IVisitor
{
    public void Visit(Element element)
    {
        Employee employee = element as Employee;

        // Provide 3 extra vacation days
        employee.VacationDays += 3;
        Console.WriteLine("{0} {1}'s new vacation days: {2}",
          employee.GetType().Name, employee.Name,
          employee.VacationDays);
    }
}

#endregion

#region Element Implementation

// defines a method that accepts logic to be visited upon on an element. 
abstract class Element
{
    public abstract void Accept(IVisitor visitor);
}

// a concrete element that contains details about an employee
// and can be acted upon by a visitor
class Employee : Element
{
    private string _name;
    private double _income;
    private int _vacationDays;

    // Constructor
    public Employee(string name, double income,
      int vacationDays)
    {
        this._name = name;
        this._income = income;
        this._vacationDays = vacationDays;
    }

    // Gets or sets the name
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }

    // Gets or sets income
    public double Income
    {
        get { return _income; }
        set { _income = value; }
    }

    // Gets or sets number of vacation days
    public int VacationDays
    {
        get { return _vacationDays; }
        set { _vacationDays = value; }
    }

    public override void Accept(IVisitor visitor)
    {
        visitor.Visit(this);
    }
}

// Three employee types
class Clerk : Employee
{
    public Clerk()
      : base("Hank", 25000.0, 14)
    {
    }
}

class Director : Employee
{
    public Director()
      : base("Elly", 35000.0, 16)
    {
    }
}

class President : Employee
{
    public President()
      : base("Dick", 45000.0, 21)
    {
    }
}

#endregion

// the object that maintains data about employees (elements)
class Employees
{
    private List<Employee> _employees = new List<Employee>();

    public void Attach(Employee employee)
    {
        _employees.Add(employee);
    }

    public void Detach(Employee employee)
    {
        _employees.Remove(employee);
    }

    public void Accept(IVisitor visitor)
    {
        foreach (Employee e in _employees)
        {
            e.Accept(visitor);
        }
        Console.WriteLine();
    }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-visitor"> 
  <button type="button" class="collapsible">+ Strategy vs Visitor Pattern<br/>
<code class="ex">
Strategy: one algorithm per logic object; select which logic object at run-time.

Visitor: multiple algorithms encapsulated in a single logic object; API is set at compile-time (?).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The following is based on the following discussions:
  * [http://leedrickdotnet.blogspot.com/2007/01/strategy-pattern-vs-visitor-pattern.html](http://leedrickdotnet.blogspot.com/2007/01/strategy-pattern-vs-visitor-pattern.html)
  * [https://stackoverflow.com/questions/8665295/what-is-the-difference-between-strategy-pattern-and-visitor-pattern](https://stackoverflow.com/questions/8665295/what-is-the-difference-between-strategy-pattern-and-visitor-pattern)

At first glance, there is a lot of similarity between the Strategy Pattern and the Visitor Pattern.  In both cases, logic to act on a data structure is injected into the data structure, so there is a clean separation between logic and data.  However, a significant difference exists:

* A Visitor implementation needs to be aware of the different types of elements it might encounter in a data structure.  Adding functionality to a Visitor implementation normally means an API change, which means this cannot be changed after compile-time.
* A Strategy implementation need only be aware of a specific element type within the data structure.  Adding functionality to a Strategy implementation does not normally require an API change, which means this can be done at run-time (which is the exact point of the Strategy Pattern).

By way of example, see the following:

```cs
using System;

// for the sake of demonstration, ICar can accept
// either an IRepairStrategy or an IRepairVisitor
public interface ICar
{
    String getName();
    
    void repair(IRepairStrategy repairStrategy);
    
    // This is the Visitor Pattern Accept method
    void repair(IRepairVisitor repairVisitor);
}

// specific implementation of ICar
public class Porsche : ICar
{
    public String getName()
    {
        return "Porsche";
    }

    public void repair(IRepairStrategy repairStrategy)
    {
        repairStrategy.repair(this);
    }

    // This is the Visitor Pattern Accept method
    public void repair(IRepairVisitor repairVisitor)
    {
        repairVisitor.repair(this);
    }
}

// specific implementation of ICar
public class Ferrari : ICar
{
    public String getName()
    {
        return "Ferrari";
    }

    public void repair(IRepairStrategy repairStrategy)
    {
        repairStrategy.repair(this);
    }

    // This is the Visitor Pattern Accept method
    public void repair(IRepairVisitor repairVisitor)
    {
        repairVisitor.repair(this);
    }
}

// IRepairStrategy provides a single, generic method 
public interface IRepairStrategy
{
    // This method is a Strategy Pattern Compose method
    void repair(ICar car);
}

// IRepairStrategy provides overloads, one for each possible implementation of ICar 
public interface IRepairVisitor
{
    // Each of these methods is a Visitor Pattern Visit method
    void repair(ICar car);
    void repair(Porsche car);
    void repair(Ferrari car);
}

// An IRepairStrategy specifically for a Porsche
public class PorscheRepairStrategy : IRepairStrategy
{
    // This method is the Strategy Pattern Compose method
    public void repair(ICar car)
    {
        Console.WriteLine("Repairing " + car.getName() + " with the Porsche repair strategy");
    }
}

// An IRepairStrategy specifically for a Ferrari
public class FerrariRepairStrategy : IRepairStrategy
{
    // This method is the Strategy Pattern Compose method
    public void repair(ICar car)
    {
        Console.WriteLine("Repairing " + car.getName() + " with the Ferrari repair strategy");
    }
}

// A single, generic RepairVisitor that can be applied to every (known) implementation of ICar
public class RepairVisitor : IRepairVisitor
{
    // Each of these methods is a Visitor Pattern Visit method

    public void repair(ICar car)
    {
        Console.WriteLine("Applying a very generic and abstract repair");
    }

    public void repair(Porsche car)
    {
        Console.WriteLine("Applying a very specific Porsche repair");
    }

    public void repair(Ferrari car)
    {
        Console.WriteLine("Applying a very specific Ferrari repair");
    }
}

class Program
{
    static void Main()
    {
        ICar porsche = new Porsche();
        porsche.repair(new PorscheRepairStrategy()); //Repairing Porsche with the porsche repair strategy
        porsche.repair(new RepairVisitor()); //Applying a very specific Porsche repair
    }
}
```

As can be seen, there is a choice: do we implement a single `RepairVisitor`, which must be handle all of the instances of `ICar`, or do we implement multiple instances of `IRepairStrategy`, one for each instance of `ICar`?

**Use the Visitor Pattern When:**
  * An object structure will not change often, but operations across them will.
  * You have specific, related functionality for each concrete class, and wish to encapsulate it.
  * An operation requires data that the object shouldn't know about.
  * You wish to maintain state within operations across multiple objects.
  
Example:
  * An application may change its "Skin" which will alter the way controls are drawn. The code for deciding how controls are drawn could be encapsulated in Visitor implementations. Each control will require a separate operation.

**Use the Strategy Pattern When:**
  * A few algorithms will be used by many different classes.
  * Different algorithms may be used by a class at different times.
  * An operation requires data that the object shouldn't know about.
  * Classes are using multiple conditional statements. These can be moved to an implementation of the Strategy class.
  * An object structure is likely to change often.
  
Example:
  * Different methods of calculating interest and fees will be used by clients of a bank. These algorithms can be encapsulated in Strategy implementations and associated with individual clients at run-time.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-managed"> 
  <button type="button" class="collapsible">+ Managed vs Unmanaged Code<br/>
<code class="ex">
Managed code is interpreted and runs in a secure, managed framework.

Unmanaged code is compiled to machine code and runs "as-is", with no management.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

**Managed code** is not compiled to machine code.
It is complied to an intermediate language which is interpreted and executed by some service on a machine.
This means it operates within a secure framework which handles dangerous things like memory and threads for you. 
In .NET, this is taken care by CLR, which transforms the code into IL. 

The CLR handles the following:
  * Managing memory for the objects
  * Performing type verification
  * Doing garbage collection

Unmanaged code is compiled to machine code.
The compiled code is executed by the OS directly. 
It therefore can do damaging/powerful things that Managed code can not. 

In unmanaged code a programmer is responsible for:
  * Calling the memory allocation function
  * Making sure that the casting is done right
  * Making sure that the memory is released when the work is done

**Using unsafe code in C#**

It is possible to use unmanaged code in C#, but this requires great care.  To do this, the block of code needs to be declared with the `unsafe` keyword:

```cs
static unsafe void Main(string[] args)
{ 
    int nr = 20; 
    int* pointerNr = &nr; 
}
```

Reasons for using unsafe code in C#:
  * Increase the performance of the program.
  * When using fixed buffers inside an unsafe context. With a fixed buffer, you can write and read raw memory without any of the managed overhead.
  * It provides a way to interface directly with memory.

Reasons to avoid unsafe code in C#:
  * It increase the responsibility of the programmer to check for security issues; care must be taken to avoid potential errors or security risks.
  * It bypasses security. Because the CLR maintains type safety and security, C# does not support pointer arithmetic in managed code, unlike C/C++. The `unsafe` keyword allows pointer usage, but safety is not guaranteed because strict object access rules are not followed.
  * It avoids type checking, which can lead to unstable code.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-strongvsweak"> 
  <button type="button" class="collapsible">+ Strong vs Weak Typing<br/>
<code class="ex">
Weak typing means delaying the check of variable’s type usually until run-time. 

Strong typing means checking type as soon as possible, usually at compile-time.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Most scripting languages are weakly typed (such as JavaScript)

C# is strongly typed because:  
  * All types are known at compile-time. Don’t be confused by `dynamic` here, this is still a type (just a special one).
  * An `int` cannot be used instead of a `string`, where a `string` is needed
  * You receive a compile-time error if the right type is not used.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-deadlocksql"> 
  <button type="button" class="collapsible">+ What is the difference between an SQL Deadlock and a C# Deadlock?<br/>
<code class="ex">
A deadlock is when separate threads are waiting for 2 objects, each one being locked by the other thread. So they are waiting for each other to unfreeze that object.

SQL can recover from a deadlock, because it has a timeout by default.

A C# application does not have a timeout and so it freezes and much be fixed.
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

<hr/>

<!-- =========================#####################################################================================ -->
<div id="basics">
<button type="button" class="collapsible">+ Language Features</button>
<div class="content" style="display: none;" markdown="1">
    
<!-- =========================#####################################################================================ -->
<div id="structs">  
<button type="button" class="collapsible">+ Structs vs Classes
<code class="ex">
Struct: value-type; cannot be null (unless Nullable<>); cannot have multiple objects reference the same struct (must be copied).
        
Class: reference-type; can consume more memory and lead to memory fragmentation; can be slower to initialize.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

### Structs:

```cs
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
      * Boxing a struct (i.e. casting it to another object) can impact performance

Use a struct when:

   * It logically represents a single value, similar to primitive types (integer, double, and so on).
   * It has an instance size smaller than 16 bytes.
   * It is immutable.
   * It will not have to be boxed frequently.

(although it is common for these rules to be violated)

### Classes:

```cs
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

<!-- =========================#####################################################================================ -->
<div id="tuples">  
<button type="button" class="collapsible">+ Tuples
<code class="ex">
There are two forms of tuple: Tuple and ValueTuple.

// Tuple format
Tuple &lt;int, string, string&gt; person = new Tuple &lt;int, string, string&gt;(1, "Steve", "Jobs");
Tuple &lt;int, string, string&gt; person = Tuple.Create(1, "Steve", "Jobs");

A Tuple can hold a maximum of 8 elements, however tuples can be nested (preferably with the nested tuple placed as the last element, since it can then be accessed via the Rest property).

// ValueTuple format
ValueTuple&lt;int, string, string&gt; person = (1, "Steve", "Jobs");
(int, string, string) person = (1, "Steve", "Jobs"); 

A ValueTuple can hold more than 8 values.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

**Accessing Tuples**

```cs
private void tupleTest()
{
    var myTuple = Tuple.Create("a", "b", "c", "d", "e", "f", "g", Tuple.Create(1, 2, 3, 4));

    Console.WriteLine(myTuple.Item1); // returns "a"
    Console.WriteLine(myTuple.Item2); // returns "b"
    Console.WriteLine(myTuple.Item3); // returns "c"

    Console.WriteLine(myTuple.Rest); // returns "((1, 2, 3, 4))"
    Console.WriteLine(myTuple.Rest.Item1.Item1); // returns "1"
    Console.WriteLine(myTuple.Rest.Item1.Item2); // returns "2"

    // named tuple elements
    
    var names1 = LookupName();
    Console.WriteLine($"found {names1.first} {names1.last}.");

    // or

    var names2 = (id: 1, first: "Steve", last: "Jobs");
    Console.WriteLine($"found {names2.first} {names2.last}.");

    // or

    var names1 = LookupName();
    Console.WriteLine($"found {names1.first} {names1.last}.");

    // or

    (var id1, var first1, var last1) = LookupName();
    Console.WriteLine($"found {first1} {last1}.");

    // or

    var (id2, first2, last2) = LookupName();
    Console.WriteLine($"found {first2} {last2}.");

    // or
    
    int id3 = 0;
    string first3 = "";
    string last3 = "";
    (id3, first3, last3) = LookupName();
    Console.WriteLine($"found {first3} {last3}.");
}

private (int id, string first, string last) LookupName() // tuple return type
{
    return (1, "Steve", "Jobs"); // tuple literal
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="boxing">  
<button type="button" class="collapsible">+ Boxing vs Unboxing
<code class="ex">
Only works for value types.

box: object o = 100; // value type to reference type

unbox: int x = (int)o; // reference type to value type

Avoid where possible; slow performance.  Use Generics instead.
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

<!-- =========================#####################################################================================ -->
<div id="delegates">   
<button type="button" class="collapsible">+ Delegate vs Action vs Func vs Predicate vs Event
<code class="ex">
Delegate: older, generic form of Action, Func and Predicate.

Action: Accept arguments; does not return.

Func: Accept arguments; returns a value.

Predicate: Special case of Func that only returns a bool.

Event: Special case of delegate that facilitates event-driven programming.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

**Be sure to also read the section on Closures.**

   * ### Delegate:
      * An older, generic form of Action, Func, Predicate or Event.
      * In C#, a `delegate` is actually always an instance of `MulticastDelegate`, which extends the `Delegate` base class and provides an additional invocation list.
      * `Delegate` is actually a legacy class that has never been removed.  It is rarely used directly, although some methods do still return a `Delegate` instance.  
      * See the section on "Multicast Delegates" for further info.
      * In any event, nowadays it is generally preferable to use one of the other forms (`Action`, `Func`, etc.), which are generally less complex and easier to read.
      
```cs
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

   * ### Action&lt;T&gt;:
      * Performs an action that accepts a parameter of type `T`, but does not return a value.
      * Overloads include Action&lt;T1, T2&gt;, Func&lt;T1, T2, T3&gt;, Func&lt;T1, T2, T3, T4&gt; etc.

Note that:

```cs
public delegate void DisplayMessage(string msg);

public class TestCustomDelegate
{
   public static void Main()
   {
      DisplayMessage messageTarget = Console.WriteLine;

      messageTarget("Hello, World!");
   }
}
```

Is functionally the same as:

```cs
public class TestAction
{
   public static void Main()
   {
      Action<string> messageTarget = Console.WriteLine;

      messageTarget("Hello, World!");
   }
}
```

A fuller example follows:

```cs
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

   * ### Func&lt;TResult&gt;:
      * Performs an function that must return a value of type `TResult`.
      * Overloads include Func&lt;T, TResult&gt;, Func&lt;T1, T2, TResult&gt;, Func&lt;T1, T2, T3, TResult&gt; etc.

Note that:

```cs
public delegate string CreateMessage();

public class TestCustomDelegate
{
   public static void Main()
   {
      CreateMessage = CreateHelloWorld;

      Console.WriteLine(CreateMessage());
   }

   private string CreateHelloWorld()
   {
      return "Hello, World!";
   }
}
```

Is functionally the same as:

```cs
public class TestFunc
{
   public static void Main()
   {
      Func<string> printMessage = CreateHelloWorld;

      Console.WriteLine(printMessage());
   }

   private string CreateHelloWorld()
   {
      return "Hello, World!";
   }
}
```

A fuller example follows:

```cs
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
      
   * ### Event:
      * An event is a special kind of delegate that facilitates event-driven programming.

The `event` keyword prevents unwanted access to the field.  There are two main reasons for this:
  * To avoid the event handler being replaced unexpectedly (e.g. `obj.Leave = MyLeaveHandler;`).
  * To prevent the event handler being fired directly from outside the class  (e.g. `obj.Leave(new EmployeeEventArgs())`).

An event typically relies on an `EventHandler` to react to the event.

```cs
using System;

public class EmployeeEventArgs : EventArgs
{
    public EmployeeEventArgs(int employeeId, int daysTaken) : base()
    {
        EmployeeId = employeeId;
        DaysTaken = daysTaken;
    }

    public int EmployeeId;
    public int DaysTaken;
}

public class Employees
{
    // assign empty delegate to avoid checks for null
    public event EventHandler<EmployeeEventArgs> Leave = delegate { };

    protected void OnLeave(object sender, EmployeeEventArgs e)
    {
        Leave(this, e);
    }

    public void VacationTaken(int employeeId, int daysTaken)
    {
        OnLeave(this, new EmployeeEventArgs(employeeId, daysTaken));
    }
}

class Program
{
    static void Main(string[] args)
    {
        Employees employees = new Employees();

        employees.Leave += (object sender, EmployeeEventArgs e) => Console.WriteLine($"Employee {e.EmployeeId} took {e.DaysTaken} days vacation");

        employees.VacationTaken(123, 2); // output: Employee 123 took 2 days vacation
    }
}
```

As shown in the following alternative example, the behaviour of events can be replicated using `Action`, however using `EventHandler` generally gives a clearer indication of intention:

```cs
using System;

public class EmployeeEventArgs : EventArgs
{
    public EmployeeEventArgs(int employeeId, int daysTaken) : base()
    {
        EmployeeId = employeeId;
        DaysTaken = daysTaken;
    }

    public int EmployeeId;
    public int DaysTaken;
}

public class Employees
{
    // assign empty delegate to avoid checks for null
    public event Action<EmployeeEventArgs> Leave = delegate { };

    // when using Action, no need to include sender in parameters
    protected void OnLeave(EmployeeEventArgs e)
    {
        Leave(e);
    }

    public void VacationTaken(int employeeId, int daysTaken)
    {
        // when using Action, no need to include sender in parameters
        OnLeave(new EmployeeEventArgs(employeeId, daysTaken));
    }
}

class Program
{
    static void Main(string[] args)
    {
        Employees employees = new Employees();

        // when using Action, no need to include sender in parameters
        employees.Leave += (EmployeeEventArgs e) => Console.WriteLine($"Employee {e.EmployeeId} took {e.DaysTaken} days vacation");

        employees.VacationTaken(123, 2); // output: Employee 123 took 2 days vacation
    }
}
```

</div>
</div>


<!-- =========================#####################################################================================ -->
<div id="delegates">   
<button type="button" class="collapsible">+ Multicast Delegates
<code class="ex">
Delegates (including Action, Func, Predicate and Event) can be chained together.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

Combinations of delegates can be manipulated using the `+` and `-` operators:
  * `delC = delA + delB`: delegate `delC` will perform delegate `delA` followed by delegate `delB`
  * `delD = delC - delB`: delegate `delB` will be removed from `delC`, so `delD` will perform only `delA`

Only delegates of the same type can be combined.

```cs
using System;

class Program
{
    static void Hello(string s)
    {
        Console.WriteLine("  Hello, {0}!", s);
        // return "said hello"; // if using Func
        // return true; // if using Predicate
    }

    static void Goodbye(string s)
    {
        Console.WriteLine("  Goodbye, {0}!", s);
        // return "said goodbye"; // if using Func
        // return true; // if using Predicate
    }

    delegate void CustomDelegate(string s);

    static void Main()
    {
        CustomDelegate a, b, c, d;

        // In this example, you could also replace the custom delegate with 
        // Action<string>, Func<string, string> or Predicate<string> instead.
        // Action<string> a, b, c, d;
        // Func<string, string> a, b, c, d;
        // Predicate<string> a, b, c, d;

        // Create the delegate object a that references 
        // the method Hello:
        a = Hello;

        // Create the delegate object b that references 
        // the method Goodbye:
        b = Goodbye;

        // The two delegates, a and b, are composed to form c: 
        c = a + b;

        // Remove a from the composed delegate, leaving d, 
        // which calls only the method Goodbye:
        d = c - a;

        Console.WriteLine("Invoking delegate a:");
        a("A");
        Console.WriteLine("Invoking delegate b:");
        b("B");
        Console.WriteLine("Invoking delegate c:");
        c("C");
        Console.WriteLine("Invoking delegate d:");
        d("D");

        /* Output:
        Invoking delegate a:
          Hello, A!
        Invoking delegate b:
          Goodbye, B!
        Invoking delegate c:
          Hello, C!
          Goodbye, C!
        Invoking delegate d:
          Goodbye, D!
        */
    }
}
```

**Multicast Delegates That Return Values**

* If the multicast delegate invocation includes output parameters or a return value (e.g. multiple `Func` statements), their final value will come from the invocation of the last delegate in the list.  All other return values are lost.

e.g.

```cs
using System;

class Program
{
    static string Hello(string s)
    {
        Console.WriteLine("Hello, {0}!", s);
        return "  said A";
    }

    static string Goodbye(string s)
    {
        Console.WriteLine("Goodbye, {0}!", s);
        return "  said B";
    }

    static void Main()
    {
        Func<string, string> a, b, c, d;

        a = Hello;
        b = Goodbye;
        c = a + b;
        d = b + a;

        Console.WriteLine(c("C"));
        Console.WriteLine(d("D"));

        /* Output:
        Hello, C!
        Goodbye, C!
          said B
        Goodbye, D!
        Hello, D!
          said A
        */
    }
}
```

&nbsp;
* A multicast delegate can be split into its constituent delegates using `Delegate.GetInvocationList()`.
* NOTE: Internally, the invocation list will be `null` if the delegate only encapsulates a single method, although `GetInvocationList()` will still return the single method (this may be a little confusing when viewed in a debugger).

```cs
using System;

class Program
{
    static string Hello(string s)
    {
        Console.WriteLine("Hello, {0}!", s);
        return "  said A";
    }

    static string Goodbye(string s)
    {
        Console.WriteLine("Goodbye, {0}!", s);
        return "  said B";
    }

    static void Main()
    {
        Func<string, string> a, b, c;

        a = Hello;
        b = Goodbye;
        c = a + b;

        foreach (Func<string, string> func in c.GetInvocationList())
        {
            Console.WriteLine(func("world"));
        }

        /* Output:
        Hello, world!
          said A
        Goodbye, world!
          said B
        */
    }
}
```

&nbsp;
* In practice, there are few real-world use cases for multicast delegates of functions.

**Multicast Events**

.NET events are essentially just multicast delegates, with some additional infrastructure (namely, the `add()` and `remove()` methods).

In the case of events, the `+` and `-` syntax is not supported, however it is possible to assign multiple event handlers using the `+=` operators.  Event handlers can be removed using the `=-` operator.

A use case for multicast events is in the case of asynchronous event handlers, where the requirement is that the triggering function does not continue until all of the event handlers have returned (but still allows the event handlers to run asynchronously).

```cs
using System;
using System.Threading;
using System.Threading.Tasks;

// ensure that OnMyEvent's task doesn't complete until 
// all of the registered MyEventHandlers have
class MyAsyncObject
{
    // a delegate for an event handler that will run asynchronously
    public delegate Task AsyncEventHandler(object sender, EventArgs e);

    // the event handler
    public event AsyncEventHandler MyEventHandler;

    // trigger the event asynchronously
    public async Task OnMyEvent(EventArgs e)
    {
        // ...

        // if listeners exist
        if (MyEventHandler != null)
            // convert the list of delegates to an array of tasks
            // then return a task that encapsulates the array of tasks
            // then run the task (which will run all the other tasks)
            await Task.WhenAll(
                Array.ConvertAll<Delegate, Task>(
                    MyEventHandler.GetInvocationList(),
                    d => ((AsyncEventHandler)d)(this, e)));
    }
}

class Program
{
    static void Main()
    {
        performTasks();
    }

    private static void performTasks()
    {
        MyAsyncObject myAsyncObject = new MyAsyncObject();

        // add event handlers (these would normally be added throughout
        // the application)
        myAsyncObject.MyEventHandler += async (sender, e) => { await Task.Run(() => myTask(1)); };
        myAsyncObject.MyEventHandler += async (sender, e) => { await Task.Run(() => myTask(2)); };
        myAsyncObject.MyEventHandler += async (sender, e) => { await Task.Run(() => myTask(3)); };
        myAsyncObject.MyEventHandler += async (sender, e) => { await Task.Run(() => myTask(4)); };
        myAsyncObject.MyEventHandler += async (sender, e) => { await Task.Run(() => myTask(5)); };

        // calling OnMyEvent will trigger all of the tasks
        // then wait for all of the tasks to complete
        myAsyncObject.OnMyEvent(new EventArgs()).Wait();

        Console.WriteLine("Done.");
    }

    private static void myTask(int id)
    {
        long start = DateTimeOffset.Now.ToUnixTimeMilliseconds();
        Console.WriteLine($"Task {id} started  at {start}");
        Random rnd = new Random();
        int wait = rnd.Next(1000);
        Thread.Sleep(wait);
        long end = DateTimeOffset.Now.ToUnixTimeMilliseconds();
        Console.WriteLine($"Task {id} complete at {end}");
    }
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="invoke">   
<button type="button" class="collapsible">+ `()` vs `Invoke()` vs `DynamicInvoke()`
<code class="ex">
(): The common method invoke syntax, e.g. doSomething().
Invoke(): This is effectively identical to (), e.g. doSomething.Invoke().
DynamicInvoke(): This effectively behaves the same as Invoke() but is a lot slower than Invoke().  It is used if the type of the delegate being invoked is not known at compile-time.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

**Invoke**

The `Invoke()` method is provided by the common language runtime (it is not part of the published class API) and primarily to aid Reflection.  It behaves exactly the same as `()`.  There is normally no need to call `Invoke()` directly.

```cs
using System;

class Program
{
    static Action del = () => { Console.WriteLine("del()"); };
    static Action<int> intDel = i => { Console.WriteLine($"del({i})"); };

    static void Main()
    {
        del(); // output: del()
        del.Invoke(); // output: del()
        intDel(3); // output: del3()
        intDel.Invoke(3); // output: del(3)
    }
}
```

**BeginInvoke/EndInvoke**

*NOTE: these are not supported in .NET Core!*

`Invoke()` launches a method synchronously (i.e. on the current thread).  To launch a method asynchronously (i.e. on a separate thread), `BeginInvoke()` can be used.

`EndInvoke()` can be used to wait for the invoked method to return, although, because `EndInvoke()` might block, it should never be called from threads that service the user interface.

```cs
using System;
using System.Threading;

public class AsyncDemo
{
    // The method to be executed asynchronously.
    public string TestMethod(int callDuration, out int threadId)
    {
        Console.WriteLine("Test method begins.");
        Thread.Sleep(callDuration);
        threadId = Thread.CurrentThread.ManagedThreadId;
        return String.Format("My call time was {0}.", callDuration.ToString());
    }
}

// The delegate must have the same signature as the method
// it will call asynchronously.
public delegate string AsyncMethodCaller(int callDuration, out int threadId);

class Program
{
    static Action del = () => { Console.WriteLine("del()"); };
    static Action<int> intDel = i => { Console.WriteLine($"del({i})"); };

    static void Main()
    {
        // The asynchronous method puts the thread id here.
        int threadId;

        // Create an instance of the test class.
        AsyncDemo ad = new AsyncDemo();

        // Create the delegate.
        AsyncMethodCaller caller = new AsyncMethodCaller(ad.TestMethod);

        // Initiate the asychronous call.
        IAsyncResult result = caller.BeginInvoke(3000,
            out threadId, null, null);

        Thread.Sleep(0);
        Console.WriteLine("Main thread {0} does some work.",
            Thread.CurrentThread.ManagedThreadId);

        // Call EndInvoke to wait for the asynchronous call to complete,
        // and to retrieve the results.
        string returnValue = caller.EndInvoke(out threadId, result);

        Console.WriteLine("The call executed on thread {0}, with return value \"{1}\".",
            threadId, returnValue);
    }
}
```

**DynamicInvoke()**

`DynamicInvoke()` is used if the type of the delegate is not known as compile-time, which means late-binding must be used.  

**NOTE:** It is a lot slower than `Invoke()` and must be used with care.

```cs
using System;
using System.Diagnostics;

class Program
{
    static void Main()
    {
        int v = 3;

        Func<int, int> twice = x => x * 2;

        const int LOOP = 5000000; // 5M

        var watch = Stopwatch.StartNew();

        for (int i = 0; i < LOOP; i++)
        {
            twice.Invoke(v);
        }

        watch.Stop();
        Console.WriteLine("Invoke: {0}ms", watch.ElapsedMilliseconds);

        Delegate slowTwice = twice; // this is still the same delegate instance
        object[] args = { v };

        watch = Stopwatch.StartNew();
        for (int i = 0; i < LOOP; i++)
        {
            twice.DynamicInvoke(args);
        }

        watch.Stop();
        Console.WriteLine("DynamicInvoke: {0}ms", watch.ElapsedMilliseconds);
    }
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="local-functions">  
<button type="button" class="collapsible">+ Local Functions
<code class="ex">
Private methods nested within other members.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

In C# 7, the concept of local functions was added:

```cs
public int Fibonacci(int x)
{
    if (x < 0) throw new ArgumentException("Less negativity please!", nameof(x));
    return Fib(x).current;

    (int current, int previous) Fib(int i)
    {
        if (i == 0) return (1, 0);
        var (p, pp) = Fib(i - 1);
        return (p + pp, p);
    }
}
```

A useful feature of local functions is that they can allow exceptions to surface immediately.  For example, for method iterators, exceptions are surfaced only when the returned sequence is enumerated, and not when the iterator is retrieved. For async methods, any exceptions thrown in an async method are observed when the returned task is awaited.

Compare the following:

```cs
using System;
using System.Collections.Generic;

public class IteratorWithoutLocalExample
{
   public static void Main()
   {
      IEnumerable<int> xs = OddSequence(50, 110);
      Console.WriteLine("Retrieved enumerator...");

      foreach (var x in xs)  // line 11
      {
         Console.Write($"{x} ");
      }
   }

   public static IEnumerable<int> OddSequence(int start, int end)
   {
      if (start < 0 || start > 99)
         throw new ArgumentOutOfRangeException(nameof(start), "start must be between 0 and 99.");
      if (end > 100)
         throw new ArgumentOutOfRangeException(nameof(end), "end must be less than or equal to 100.");
      if (start >= end)
         throw new ArgumentException("start must be less than end.");

      for (int i = start; i <= end; i++)
      {
         if (i % 2 == 1)
            yield return i;
      }
   }
}
// The example displays the output like this:
//
//    Retrieved enumerator...
//    Unhandled exception. System.ArgumentOutOfRangeException: end must be less than or equal to 100. (Parameter 'end')
//    at IteratorWithoutLocalExample.OddSequence(Int32 start, Int32 end)+MoveNext() in IteratorWithoutLocal.cs:line 22
//    at IteratorWithoutLocalExample.Main() in IteratorWithoutLocal.cs:line 11
```
&nbsp;
```cs
using System;
using System.Collections.Generic;

public class IteratorWithLocalExample
{
   public static void Main()
   {
      IEnumerable<int> xs = OddSequence(50, 110);  // line 8
      Console.WriteLine("Retrieved enumerator...");

      foreach (var x in xs)
      {
         Console.Write($"{x} ");
      }
   }

   public static IEnumerable<int> OddSequence(int start, int end)
   {
      if (start < 0 || start > 99)
         throw new ArgumentOutOfRangeException(nameof(start), "start must be between 0 and 99.");
      if (end > 100)
         throw new ArgumentOutOfRangeException(nameof(end), "end must be less than or equal to 100.");
      if (start >= end)
         throw new ArgumentException("start must be less than end.");

      return GetOddSequenceEnumerator();

      IEnumerable<int> GetOddSequenceEnumerator()
      {
         for (int i = start; i <= end; i++)
         {
            if (i % 2 == 1)
               yield return i;
         }
      }
   }
}
// The example displays the output like this:
//
//    Unhandled exception. System.ArgumentOutOfRangeException: end must be less than or equal to 100. (Parameter 'end')
//    at IteratorWithLocalExample.OddSequence(Int32 start, Int32 end) in IteratorWithLocal.cs:line 22
//    at IteratorWithLocalExample.Main() in IteratorWithLocal.cs:line 8
```

In addition, local functions have the following advantages over lambda expressions:

(taken from: [https://www.commentout.com/localfunc.html](https://www.commentout.com/localfunc.html))

* Local functions can be called without converting to a delegate, so you don't need to wrap them in Func or Action if you're just calling from your current method
* Local functions can be recursive
* Local functions can be iterators
* Since iterators don't start running until you start iterating over them this can be very useful if you want to do a little early-validation for your iterator method. You can stick the body of your iterator in a local function, do your validation up front, and then call your iterator.
* Local functions can be generic (e.g., bool Local<T>(T t) => t == default(T);)
* Local functions have strictly more precise definite assignment rules
* In certain cases, local functions do not need to allocate memory on the heap

(taken from: [https://stackoverflow.com/questions/40943117/local-function-vs-lambda-c-sharp-7-0](https://stackoverflow.com/questions/40943117/local-function-vs-lambda-c-sharp-7-0))

* Performance.
  * When creating a lambda, a delegate has to be created, which is an unnecessary allocation in this case. Local functions are really just functions, no delegates are necessary.
  * Also, local functions are more efficient with capturing local variables: lambdas usually capture variables into a class, while local functions can use a struct (passed using ref), which again avoids an allocation.
  * This also means calling local functions is cheaper and they can be inlined, possibly increasing performance even further.
* Local functions can be recursive.
  * Lambdas can be recursive too, but it requires awkward code, where you first assign null to a delegate variable and then the lambda. Local functions can naturally be recursive (including mutually recursive).
* Local functions can be generic.
  * Lambdas cannot be generic, since they have to be assigned to a variable with a concrete type (that type can use generic variables from the outer scope, but that's not the same thing).
* Local functions can be implemented as an iterator.
  * Lambdas cannot use the yield return (and yield break) keyword to implement IEnumerable<T>-returning function. Local functions can.
* Local functions look better
  * This is more personal preference.
  * Compare:

```cs
int add(int x, int y) => x + y;
Func<int, int, int> add = (x, y) => x + y;
```

</div>
</div>

<!-- =========================#####################################################================================ -->
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
                printer(); // 10, 10, 10 ....
            }
        }
    }
}
```
At first glance, the above code would seem to indicate that `i` is incremented for each new delegate added to `printers`, however in practice what happens is that the compiler has associated the delegates with the variable `i` and the run-time will use whatever the value of `i` is at the time the delegate method is called (in the `foreach` loop).

Conceptually, the compiler does something like this:

```cs
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
        printer.printer();  // 10, 10, 10 ....
    }
}
```

To avoid this, the value of `i` should be passed as an argument, rather than as a scoped variable:

```cs
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
        printer();  // 0, 1, 2 ....
    }
}
```

In this case, the compiler (again, conceptually) generates a closure similar to the following:

```cs
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

<!-- =========================#####################################################================================ -->
<div id="interview-objinit"> 
  <button type="button" class="collapsible">+ Object Initializer Syntax
<code class="ex">
Student student = new Student()
{
    StudentID = 1,
    StudentName = "Bill",
    Age = 20
};
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Object initializers allow you to assign values to the fields or properties at the time of creating an object without invoking a constructor.

For example:

```cs
public class Student
{
    public int StudentID { get; set; }
    public string StudentName { get; set; }
    public int Age { get; set; }
    public string Address { get; set; }
}

class Program
{
    static void Main(string[] args)
    {
        Student std = new Student()
        {
            StudentID = 1,
            StudentName = "Bill",
            Age = 20,
            Address = "New York"
        };
    }
}
```

This syntax can also be used to initialize collections:

```cs
var student1 = new Student() { StudentID = 1, StudentName = "John" };
var student2 = new Student() { StudentID = 2, StudentName = "Steve" };
var student3 = new Student() { StudentID = 3, StudentName = "Bill" } ;
var student4 = new Student() { StudentID = 3, StudentName = "Bill" };
var student5 = new Student() { StudentID = 5, StudentName = "Ron" };

IList<Student> studentList = new List<Student>() { 
                                                    student1, 
                                                    student2, 
                                                    student3, 
                                                    student4, 
                                                    student5 
                                                };
```

Or:

```cs
IList<Student> studentList = new List<Student>() { 
                    new Student() { StudentID = 1, StudentName = "John"} ,
                    new Student() { StudentID = 2, StudentName = "Steve"} ,
                    new Student() { StudentID = 3, StudentName = "Bill"} ,
                    new Student() { StudentID = 3, StudentName = "Bill"} ,
                    new Student() { StudentID = 4, StudentName = "Ram" } ,
                    new Student() { StudentID = 5, StudentName = "Ron" } 
                };
```

You can also specify `null` as an element:

```cs
IList<Student> studentList = new List<Student>() { 
                                    new Student() { StudentID = 1, StudentName = "John"} ,
                                    null
                                };
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-anontype"> 
  <button type="button" class="collapsible">+ Anonymous Types
<code class="ex">
var student = new { Id = 1, FirstName = "James", LastName = "Bond" };
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

An anonymous type is a type without any name that can contain public read-only properties only. It cannot contain other members, such as fields, methods, events, etc.

Anonymous types are created using the `new` operator with an object initializer syntax. The implicitly typed variable `var` is used to hold the reference of anonymous types.

For example:

```cs
var student = new { Id = 1, FirstName = "James", LastName = "Bond" };
```

**Note:** The properties of anonymous types are read-only and cannot be initialized with a null, anonymous function, or a pointer type. The properties can be accessed using dot (.) notation, same as object properties. However, you cannot change the values of properties as they are read-only.

The following will fail at compile-time:

```cs
var student = new { Id = 1, FirstName = "James", LastName = "Bond" };
Console.WriteLine(student.Id); // output: 1
Console.WriteLine(student.FirstName); // output: James
Console.WriteLine(student.LastName); // output: Bond

student.Id = 2; // Error: cannot change value
student.FirstName = "Steve"; // Error: cannot change value
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="linq">  
<button type="button" class="collapsible">+ LINQ
<code class="ex">
LINQ (Language Integrated Query) is uniform query syntax to retrieve data from different sources and formats.
Like SQL for .NET data sources.
Two flavours: Lambda Expressions and Query Comprehension Syntax
</code>
</button>
<div class="content" style="display: none;" markdown="1">

LINQ comes in two flavours:
  1. Lambda Expressions
  1. Query Comprehension Syntax

Both yield the same result because query expressions are translated into their lambda expressions before they’re compiled. So performance-wise, there’s no difference whatsoever between the two.

Which one you should use is mostly personal preference; many people prefer lambda expressions because they’re shorter and more concise, but some people prefer the query syntax having worked extensively with SQL. 

The following example shows the same query written using the two different syntaxes:

```cs
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        Person[] people1 = { tom, dick, harry, mary, jay, harry2 };
        Person[] people2 = { fred, barney, wilma, betty, tom2 };

        lambdaExpression(people1, people2);

        Console.WriteLine();

        queryComprehensionSyntax(people1, people2);
    }

    private static void lambdaExpression(Person[] people1, Person[] people2)
    {
        IEnumerable<string> query = people1
          .Where(p => p.Name.Contains("a"))    // Filter elements
          .OrderBy(p => p.Name.Length)         // Sort elements
          .Select(p => p.Name.ToUpper());      // Project each element

        foreach (string name in query)
            Console.Write(name + "|");

        // RESULT: JAY|MARY|HARRY|HARRY|
    }

    private static void queryComprehensionSyntax(Person[] people1, Person[] names2)
    {
        IEnumerable<string> query =
          from p in people1
          where p.Name.Contains("a")    // Filter elements
          orderby p.Name.Length         // Sort elements
          select p.Name.ToUpper();      // Project each element

        foreach (string name in query)
            Console.Write(name + "/");

        // RESULT: JAY/MARY/HARRY/HARRY/
    }

    #region data source 
    
    public struct Person
    {
        public Person(string name, int age)
        {
            Name = name;
            Age = age;
        }
        public string Name;
        public int Age;
    }

    static Person tom = new Person("Tom", 30);
    static Person dick = new Person("Dick", 23);
    static Person harry = new Person("Harry", 38);
    static Person mary = new Person("Mary", 16);
    static Person jay = new Person("Jay", 23);
    static Person harry2 = new Person("Harry", 48);

    static Person fred = new Person("Fred", 39);
    static Person barney = new Person("Barney", 35);
    static Person wilma = new Person("Wilma", 36);
    static Person betty = new Person("Betty", 35);
    static Person tom2 = new Person("Tom", 55);
    
    #endregion
}
```

**Example Expressions**

The following are just some of the most common expressions:

### Where

Applies a filter to the values in a list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Where(p => p.Name == "Tom");

    foreach (var res in query)
        Console.Write(res.Name + "/");

    // RESULT: Tom/
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p in people1
                where p.Name.Equals("Tom")
                select p;

    foreach (var res in query)
        Console.Write(res.Name + "|");

    // RESULT: Tom|
}
```

### Select

Returns values from a list encapsulated in a new object (typically an anonymous type).

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Select(p => new
    {
        Name = p.Name
    });

    foreach (var res in query)
        Console.Write(res.Name + "/");

    // RESULT: Tom/Dick/Harry/Mary/Jay/Harry/
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p in people1
                select new
                {
                    Name = p.Name
                };

    foreach (var res in query)
        Console.Write(res.Name + "|");

    // RESULT: Tom|Dick|Harry|Mary|Jay|Harry|
}
```

### OrderBy

Performs a primary, ascending sort on the values in list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.OrderBy(p => p.Name);

    foreach (var res in query)
        Console.Write(res.Name + "/");

    // RESULT: Tom/Dick/Harry/Mary/Jay/Harry/
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p in people1
                orderby p.Name
                select p;

    foreach (var res in query)
        Console.Write(res.Name + "|");

    // RESULT: Dick|Harry|Harry|Jay|Mary|Tom|
}
```

### OrderByDescending

Performs a primary, descending sort on the values in list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.OrderByDescending(p => p.Name);

    foreach (var res in query)
        Console.Write(res.Name + "/");

    // RESULT: Tom/Mary/Jay/Harry/Harry/Dick/
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p in people1
                orderby p.Name descending
                select p;

    foreach (var res in query)
        Console.Write(res.Name + "|");

    // RESULT: Tom|Mary|Jay|Harry|Harry|Dick|
}
```

### ThenByDescending

Performs a secondary, descending sort on the values in list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.OrderBy(p => p.Name).
                   ThenByDescending(p => p.Age);

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} / ");

    // RESULT: Dick - 23 / Harry - 48 / Harry - 38 / Jay - 23 / Mary - 16 / Tom - 30 /
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p in people1
                orderby p.Name ascending, p.Age descending
                select p;
    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} | ");

    // RESULT: Dick - 23 | Harry - 48 | Harry - 38 | Jay - 23 | Mary - 16 | Tom - 30 |
}
```

### Join

Joins the values in two or more lists into a new list, based on key values.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Join(people2,
                                p1 => p1.Name,
                                p2 => p2.Name,
                                (p1, p2) => new
                                {
                                    p1.Name,
                                    Age1 = p1.Age,
                                    Age2 = p2.Age
                                }
                            );

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age1} - {res.Age2} / ");

    // RESULT: Tom - 30 - 55 / 
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p1 in people1
                join p2 in people2 on p1.Name equals p2.Name
                select new { Name = p1.Name, Age1 = p1.Age, Age2 = p2.Age };

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age1} - {res.Age2} | ");

    // RESULT: Tom - 30 - 55 | 
}
```

### GroupBy

Groups the values in the list, based on a key.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.GroupBy(p => p.Name).
                     Select(grp => new
                     {
                         Name = grp.Key,
                         Count = grp.Count()
                     }
                 );

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Count} / ");

    // RESULT: Tom - 1 / Dick - 1 / Harry - 2 / Mary - 1 / Jay - 1 / 
}
```
&nbsp;
```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = from p1 in people1
                group p1 by p1.Name
                into grp
                select new { Name = grp.Key, Count = grp.Count() };

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Count} | ");

    // RESULT: Tom - 1 | Dick - 1 | Harry - 2 | Mary - 1 | Jay - 1 | 
}
```

### Take

Takes the first N values from the list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Where(
                 p => p.Name.Contains("a")).
                 Take(3);

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} / ");

    // RESULT: Harry - 38 / Mary - 16 / Jay - 23 / 
}
```
&nbsp;
**NOTE**: There is no equivalent to `Take()` in query syntax!

```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = (from p1 in people1
                 where p1.Name.Contains("a")
                 select p1)
                .Take(3); // There is no "take" in query syntax, so must use lambda

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} | ");

    // RESULT: Harry - 38 | Mary - 16 | Jay - 23 | 
}
```

### Skip

Skips the first N values in the list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Where(
                 p => p.Name.Contains("a")).
                 Skip(2);

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} / ");

    // RESULT: Jay - 23 / Harry - 48 / 
}
```
&nbsp;
**NOTE**: There is no equivalent to `Skip()` in query syntax!

```cs
private static void queryComprehensionSyntax(Person[] people1, Person[] people2)
{
    var query = (from p1 in people1
                 where p1.Name.Contains("a")
                 select p1)
                .Skip(2); // There is no "skip" in query syntax, so must use lambda

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} | ");

    // RESULT: Jay - 23 | Harry - 48 | 
}
```

### Single and SingleOrDefault

Returns the single entry from a list.

  * `Single`: If there are zero, or more than one, entries in the list, an exception is thrown.
  * `SingleOrDefault`: If there are zero entries in the list, a default value is returned; if there are more than one entry, an exception is thrown.  The default value is the default value for the type (e.g. `null` for an object, `0` for an `int` etc.). 

**NOTE**: The main (only?) reason for using this is to explicitly indicate the intent of the code. Otherwise, use `First()`, or `FirstOrDefault()`.  The `Single` methods are less efficient than the `First` methods since the `Single` methods always scan the entire list checking for duplicates (whereas the `First` methods return immediately upon identifying the first value).

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Single(
                     p => p.Name == "Tom"
                 );

    Console.WriteLine($"{query.Name} - {query.Age} / ");

    // RESULT: Tom - 30 / 

    var defaultQuery = people1.SingleOrDefault(
                     p => p.Name == "Eric"
                 );

    Console.WriteLine($"{defaultQuery.Name} - {defaultQuery.Age} / ");

    // RESULT:  - 0 / 

    try
    {
        var badQuery = people1.Single(
                         p => p.Name == "Eric"
                     );
    }
    catch (Exception x)
    {
        Console.WriteLine(x.Message);
    }

    // RESULT: Sequence contains no matching element 

    try
    {
        var badQuery = people1.Single(
                         p => p.Name == "Harry"
                     );
    }
    catch (Exception x)
    {
        Console.Write(x.Message);
    }

    // RESULT: Sequence contains more than one matching element 
}
```
&nbsp;
**NOTE**: There is no equivalent to `Single()` or `SingleOrDefault()` in query syntax!

### First or FirstOrDefault

Returns the first entry from a list.

  * `First`: If there are zero entries in the list, an exception is thrown.
  * `FirstOrDefault`: If there are zero entries in the list, a default value is returned.  The default value is the default value for the type (e.g. `null` for an object, `0` for an `int` etc.). 

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.First(
                     p => p.Name == "Tom"
                 );

    Console.WriteLine($"{query.Name} - {query.Age} / ");

    // RESULT: Tom - 30 / 

    var defaultQuery = people1.FirstOrDefault(
                     p => p.Name == "Eric"
                 );

    Console.WriteLine($"{defaultQuery.Name} - {defaultQuery.Age} / ");

    // RESULT:  - 0 / 

    try
    {
        var badQuery = people1.First(
                         p => p.Name == "Eric"
                     );
    }
    catch (Exception x)
    {
        Console.WriteLine(x.Message);
    }

    // RESULT: Sequence contains no matching element 
}
```
&nbsp;
**NOTE**: There is no equivalent to `First()` or `FirstOrDefault()` in query syntax!

### DefaultIfEmpty

Returns the specified default value if the source list is empty.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    Person defaultPerson = new Person { Name = "Default Person", Age = 0 };

    List<Person> people = new List<Person>();

    var query = people.DefaultIfEmpty(defaultPerson);

    foreach (var res in query)
        Console.Write($"{res.Name} - {res.Age} / ");

    // RESULT: Default Person - 0 / 
}
```
&nbsp;
**NOTE**: There is no equivalent to `DefaultIfEmpty()` in query syntax!

### Last or LastOrDefault

Returns the last entry from a list.

  * `Last`: If there are zero entries in the list, an exception is thrown.
  * `LastOrDefault`: If there are zero entries in the list, a default value is returned.  The default value is the default value for the type (e.g. `null` for an object, `0` for an `int` etc.). 

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    var query = people1.Last(
                     p => p.Name == "Tom"
                 );

    Console.WriteLine($"{query.Name} - {query.Age} / ");

    // RESULT: Tom - 30 / 

    var defaultQuery = people1.LastOrDefault(
                     p => p.Name == "Eric"
                 );

    Console.WriteLine($"{defaultQuery.Name} - {defaultQuery.Age} / ");

    // RESULT:  - 0 / 

    try
    {
        var badQuery = people1.Last(
                         p => p.Name == "Eric"
                     );
    }
    catch (Exception x)
    {
        Console.WriteLine(x.Message);
    }

    // RESULT: Sequence contains no matching element 
}
```
&nbsp;
**NOTE**: There is no equivalent to `Last()` or `LastOrDefault()` in query syntax!

### ToArray

Copies the returned enumerated values to an array.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    Person[] query = people1.Where(p => p.Name == "Harry").ToArray();

    foreach (var res in query)
        Console.Write(res.Name + "/");

    // RESULT: Harry/Harry/
}
```
&nbsp;
**NOTE**: There is no equivalent to `ToArray()` in query syntax!

### ToDictionary

Copies the returned enumerated values to a dictionary.

**NOTE**: An exception will be thrown if the source list contains duplicate key values.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    Person[] people3 = { tom, dick, harry, mary, harry2 };

    Dictionary<int, Person> query =
            people3.ToDictionary(p => p.Age);

    foreach (var res in query)
        Console.Write($"{res.Key} - {res.Value.Name} / ");

    // 30 - Tom / 23 - Dick / 38 - Harry / 16 - Mary / 48 - Harry /
}
```
&nbsp;
**NOTE**: There is no equivalent to `ToDictionary()` in query syntax!

### ToList

Copies the returned enumerated values a list.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    List<Person> query = people1.Where(p => p.Name == "Harry").ToList();

    foreach (var res in query)
        Console.Write(res.Name + "/");

    // RESULT: Harry/Harry/
}
```
&nbsp;
**NOTE**: There is no equivalent to `ToList()` in query syntax!

### ToLookup

```cs
    private static void lambdaExpression(Person[] people1, Person[] people2)
    {
        ILookup<char, Person> query =
                people1.ToLookup(p => Convert.ToChar(p.Name.Substring(0, 1)));

        foreach (IGrouping<char, Person> group in query)
        {
            // Print the key value of the IGrouping.
            Console.WriteLine(group.Key);
            // Iterate through each value in the IGrouping and print its value.
            foreach (Person person in group)
                Console.WriteLine($"  {person.Name} - {person.Age}");
        }

        // RESULT:
        // T
        //   Tom - 30
        // D
        //   Dick - 23
        // H
        //   Harry - 38
        //   Harry - 48
        // M
        //   Mary - 16
        // J
        //   Jay - 23
    }
```
&nbsp;
**NOTE**: There is no equivalent to `ToLookup()` in query syntax!

### Aggregate

Applies a function that aggregates all of the values in the list and returns the aggregated result.

```cs
private static void lambdaExpression(Person[] people1, Person[] people2)
{
    // Identifies the person in the array with the longest name, assuming it is longer than "Tom".
    string longestName =
        people1.Aggregate("Tom",
                        (longest, next) =>
                            next.Name.Length > longest.Length ? next.Name : longest,
        // Return the final result as an upper case string.
                        name => name.ToUpper());
                    
    Console.Write(longestName + "/");

    // RESULT: HARRY/
}
```
&nbsp;
**NOTE**: There is no equivalent to `Aggregate()` in query syntax!


**Further Information**

For further info on Lambda Expressions, see the following: 
  * [System.Linq.Enumerable API Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable)
  * [System.Linq.Queryable API Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable)

Query comprehension syntax can be summarized using the following diagram:

<img src="assets/images/query-comprehension-syntax.png" />

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-linq"> 
  <button type="button" class="collapsible">+ LINQ vs Stored Procedures
<code class="ex">
LINQ: A common query syntax to query various data sources, such as SQL Server, Oracle, XML, Collections, etc. 
LINQ: Has full type checking at compile-time and IntelliSense support in Visual Studio.
Stored Procedures: Pre-compiled SQL statements that are stored on a remote database. 
Stored Procedures: Are executed on the server side, so can be executed quickly, with reduced network traffic.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">
    
1. Unless caching is correctly enabled for LINQ, stored procedures are faster to execute and can take the full advantage of SQL features.  If LINQ caching is enabled, the performance difference is not significant.
1. Generally speaking, stored procedures are better for complex queries.
1. Stored procedures are more efficient for bulk insert and update operations.
1. LINQ supports type safety, debugging and Intellisense, which makes development and testing easier.
1. LINQ supports .NET features such as multithreading, which stored procedures do not.
1. LINQ provides a common query syntax that is independent of the backend, unlike stored procedures which need to be re-written for different databases.
1. Deploying a LINQ-based application is simpler since it generally just involves deploying DLLs, unlike stored procedures that also require scripts to update the database.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-expressiontrees"> 
  <button type="button" class="collapsible">+ Expression Trees
<code class="ex">
A way of breaking down functions into a tree like structure.
Expression trees were created for the task of converting code such as a query expression into 
a string that can be passed to some other process and executed there.
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

<!-- =========================#####################################################================================ -->
<div id="interview-defvsimed"> 
  <button type="button" class="collapsible">+ Deferred Execution vs Immediate Execution
<code class="ex">
Deferred execution: a method/function is declared but not executed until a late time.
Typically used with LINQ providers, but can also be used with in-memory collections.
An advantage is that data can be filtered before it is loaded into memory.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

A simple example is the following statement:

```cs
// the expression is built here, but not executed
var persons = context.Persons.Where(a=>a.Age > 18)
```

In this case, the function is not executed until an additional "aggregate" function is called:

```cs
// calling .Count() forces the expression to be executed
var persons = context.Persons.Where(a=>a.Age > 18).Count();
```

Note that, since execution is deferred, the results returned will match the data source at execution time, not at the time the function was defined.

A significant advantage of deferred execution is that it allows data to be filtered before it is loaded into memory. 

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-overload"> 
  <button type="button" class="collapsible">+ Overriding vs Overloading
<code class="ex">
overriding (a.k.a late binding): replace method in super-class with one in sub-class, with same signature.
overloading: provide a new method, constructor or operator body with the same name but a different signature.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

**Override**

Only methods can be overridden.

To override a method in a super-class it must be declared as `abstract` or `virtual`, and it cannot be `private`.

Overriding is also known as late binding, or run-time or dynamic polymorphism.

The following is a simple example of overriding:

```cs
using System;

public abstract class MySuperClass
{
    public virtual void MyVirtualMethod()
    {
        Console.WriteLine(" + MySuperClass.MyVirtualMethod");
    }

    public abstract void MyAbstractMethod();
}

public class MySubClass : MySuperClass
{
    public override void MyVirtualMethod()
    {
        Console.Write("MySubClass.MyVirtualMethod");
        base.MyVirtualMethod();
    }

    public override void MyAbstractMethod()
    {
        Console.WriteLine("MySubClass.MyAbstractMethod");
    }
}

class Program
{
    static void Main()
    {
        MySuperClass superClass = new MySubClass();
        MySubClass subClass = new MySubClass();

        superClass.MyVirtualMethod(); // MySubClass.MyVirtualMethod + MySuperClass.MyVirtualMethod
        superClass.MyAbstractMethod(); // MySubClass.MyAbstractMethod

        subClass.MyVirtualMethod(); // MySubClass.MyVirtualMethod + MySuperClass.MyVirtualMethod
        subClass.MyAbstractMethod(); // MySubClass.MyAbstractMethod
    }
}
```

**Overload: Methods &amp; Constructors**

Both methods and constructors can be overloaded.  The overloading can happen in either the super-class or a sub-class.

The following gives some examples of method and constructor overloading:

```cs
using System;

public class Super
{
    public Super()
    {
        Console.Write("Super()");
    }

    public Super(int param1)
    {
        Console.Write("Super(int param1)");
    }

    public void Method()
    {
        Console.Write("Super.Method()");
    }

    public void Method(int param1)
    {
        Console.Write("Super.Method(int param1)");
    }
}

public class Sub : Super
{
    public Sub() : base()
    {
        Console.WriteLine(" + Sub()");
    }

    public Sub(int param1) : base(param1)
    {
        Console.WriteLine(" + Sub(int param1)");
    }

    public Sub(int param1, int param2) : base(param1)
    {
        Console.WriteLine(" + Sub(int param1, int param2)");
    }

    public void Method(int param1, int param2)
    {
        base.Method(param1);
        Console.WriteLine(" + Sub.Method(int param1, int param2)");
    }
}

class Program
{
    static void Main()
    {
        Super superClass1 = new Super(); nl();  // Super()
        Super superClass2 = new Super(1); nl(); // Super(int param1)

        Sub subClass1 = new Sub(); nl();        // Super() +  Sub()
        Sub subClass2 = new Sub(1); nl();       // Super(int param1) +  Sub(int param1)
        Sub subClass3 = new Sub(1, 2); nl();    // Super(int param1) +  Sub(int param1, int param2)

        superClass1.Method(); nl();             // Super.Method()
        superClass1.Method(1); nl();            // Super.Method(int param1)

        superClass2.Method(); nl();             // Super.Method()
        superClass2.Method(1); nl();            // Super.Method(int param1)

        subClass1.Method(); nl();               // Super.Method()
        subClass1.Method(1); nl();              // Super.Method(int param1)
        subClass1.Method(1, 2); nl();           // Super.Method(int param1) + Sub.Method(int param1, int param2)

        subClass2.Method(); nl();               // Super.Method()
        subClass2.Method(1); nl();              // Super.Method(int param1)
        subClass2.Method(1, 2);                 // Super.Method(int param1) + Sub.Method(int param1, int param2)
    }

    private static void nl()
    {
        Console.WriteLine("\n");
    }
}
```

**Overload: Operators**

Operators can also be overloaded, however this is a little more complex, since not all operators can be overloaded:

CAN BE OVERLOADED
  * Unary operators: +, -, !, ~, ++, --
  * Binary operators: +, -, *, /, %
  * Comparison operators: ==, !=, &lt;, &gt;, &lt;=, &gt;=

CANNOT BE OVERLOADED
  * Conditional logical operators: &&, \||
  * Assignment operators: +=, -=, *=, /=, %=
  * Special operators: =, ., ?:, ->, new, is, sizeof, typeof

Using the `+` operator as an example, the general pattern for overloading an operator is the following:

```cs
public static MyObj operator+ (MyObj b, MyObj c) 
{
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-binding"> 
  <button type="button" class="collapsible">+ Early-Binding and Late-Binding
<code class="ex">
Binding is the act of associating the parameters, types, return values and function calls to an object.

Early-Binding: a method is defined at compile-time.
Late-Binding: a method is defined at run-time.

Late-binding is usually slower than early-binding.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

In the case of C#, almost everything is early-bound by default (as opposed to scripting languages, where almost everything is late-bound).

It is possible to use late-binding in C# using the following approaches:

  * Using Reflection (see below).
  * Use the `virtual` and `override` keywords.

Late-binding is usually slower than early-binding.

The following is an example of using Reflection to enable late-binding:

```cs
using System.Reflection;

class Program
{
    // Main Method 
    static void Main(string[] args)
    {
        // Declare Instance of class Assembly 
        // Call the GetExecutingAssembly method 
        // to load the current assembly 
        Assembly executing = Assembly.GetExecutingAssembly();

        // To find the type of the Class Student 
        Type studentType = executing.GetType("LateBinding.Student");

        // Create an Instance of the Student type 
        object studentObject = Activator.CreateInstance(studentType);

        // Store the info of the method in an object 
        // of class MethodInfo 
        MethodInfo getMethod = studentType.GetMethod("GetDetails");

        // To store the parameters required 
        // by Method GetDetails 
        String[] param = new String[2];
        param[0] = "1";
        param[1] = "Lisa";

        // To display the result of the method 
        String det = (String)getMethod.Invoke(studentObject, param);
        Console.WriteLine("Student Details : ");
        Console.WriteLine("Roll Number - Name \n{0}", det);
    } // end Main 
} // end Program 


public class Student
{
    public String GetDetails(String rollNumber, String name)
    {
        return rollNumber + " - " + name;
    }
} // end Student 
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-reflection"> 
  <button type="button" class="collapsible">+ Reflection
<code class="ex">
Reflection is when managed code can read its own metadata to find assemblies.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Reflection allows the contents of an assembly to be interrogated.  Its use should be avoided if not strictly necessary since there is a performance penalty.

Bear in mind:
  * Assemblies contain modules.
  * Modules contain types.
  * Types contain members.

With reflection in C#, you can:
  * Dynamically create an instance of a type and bind that type to an existing object.
  * Get the type from an existing object and access its properties.
  * Enable access to attributes.

Common use cases for reflection are:
  * Identifying members that have been marked with attributes.
  * Testing particularly difficult assemblies.
  * Debugging.
  * Implementing a system of plugins.
  * Custom serialization routines.
  
The reflection API is contained in the 'System.Reflection' namespace.  The most commonly used features are:
  * Use `Module` to get all global and non-global methods defined in the module.
  * Use `MethodInfo` to look at information such as parameters, name, return type, access modifiers and implementation details.
  * Use `EventInfo` to find out the event-handler data type, the name, declaring type and custom attributes.
  * Use `ConstructorInfo` to get data on the parameters, access modifiers, and implementation details of a constructor.
  * Use `Assembly` to load modules listed in the assembly manifest.
  * Use `PropertyInfo` to get the declaring type, reflected type, data type, name and writable status of a property or to get and set property values.
  * Use `CustomAttributeData` to find out information on custom attributes or to review attributes without having to create more instances.

**Examples**

As shown in the following, simple example, implementing reflection is a 2 step process:
  1. Get the `type` object.
  1. Browse the members of the `type` object.

```cs
// Using GetType to obtain type information:
int i = 42;
System.Type type = i.GetType();
System.Console.WriteLine(type); // output: System.Int32
```

In the following example, a new instance of the DateTime class is created from the system assembly:

```cs
// create instance of class DateTime
DateTime dateTime = (DateTime)Activator.CreateInstance(typeof(DateTime));
```

In this more complex example, a class (`Calculator`) is accessed from the `Test.dll` assembly and the property values updated:

```cs
namespace Test
{
    public class Calculator
    {
        public Calculator() { ... }
        private double _number;
        public double Number { get { ... } set { ... } }
        public void Clear() { ... }
        private void DoClear() { ... }
        public double Add(double number) { ... }
        public static double Pi { ... }
        public static double GetPi() { ... }
    }
}
```

```cs
// dynamically load assembly from file Test.dll
Assembly testAssembly = Assembly.LoadFile(@"c:\Test.dll");

// get type of class Calculator from just loaded assembly
Type calcType = testAssembly.GetType("Test.Calculator");

// create instance of class Calculator
object calcInstance = Activator.CreateInstance(calcType);

// get info about property: public double Number
PropertyInfo numberPropertyInfo = calcType.GetProperty("Number");

// get value of property: public double Number
double value = (double)numberPropertyInfo.GetValue(calcInstance, null);

// set value of property: public double Number
numberPropertyInfo.SetValue(calcInstance, 10.0, null);
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-passbyvalue"> 
  <button type="button" class="collapsible">+ Pass By Value vs Pass by Reference
<code class="ex">
Pass by value: a copy of the data is passed into a method.
Pass by reference: the original data is passed into a method.

In C#, all data is passed by value into a method by default, even reference types.
However, when passing reference types, it is a copy of the reference that is passed, not the object.
String is a special case, in that it is a reference type that (effectively) behaves like a value type.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

It is important to bear in mind that objects on the heap are always referenced by a value on the stack (hence "reference type").  When data is passed around in C#, it is normally the value on the stack that is passed around, not the object on the heap.  Accordingly, all data in C# is considered as "passed by value" by default.  When an item is passed by value, a copy is created of the item (to reiterate: for reference types, the item copied will be the reference, not the object).

This behaviour can be overridden using the `ref` and `out` keywords.

**Strings**

Strings are a special case.  Consider the following example:

```cs
using System;

class Program
{
    static void DoSomething(string strLocal)
    {
        strLocal = "local";
    }

    static void Main()
    {
        string strMain = "main";
        DoSomething(strMain);
        Console.WriteLine(strMain); // What gets printed?
    }
}
```

There are three things that need to be understood here:

1. Strings are reference types in C#.
1. Strings are immutable; a string cannot be changed. Any time a new string is "changed", a new string gets created and the existing reference is pointed at the new object. The old object gets thrown away.
1. Even though strings are reference types, `strMain` isn't passed by reference. It's a reference type, but the reference itself is passed by value. Any time a parameter is passed without the `ref` keyword (not counting `out` parameters), something has been passed by value.

So, taking this line by line:

First, an object with the value `"main"` is created on the heap, and a reference to this object called `strMain` is created on the stack:

```cs
string strMain = "main";
```

Now, the `DoSomething` method is called, which results in a child frame being created (a new, additional step on the call-stack).  The `strMain` reference variable is input into the new frame:

```cs
DoSomething(strMain);
```

Upon entry to the method/frame, the input reference to `"main"` is **copied** into a new reference called `strLocal`:

```cs
void DoSomething(string strLocal)
```

Now, the `strLocal` reference variable is re-pointed to a brand new string object with the value `"local"`:

```cs
strLocal = "local";
```

The method/frame now returns/exits.  Since the `strLocal` reference variable is not returned, this is destroyed (removed from the stack), which means the `"local"` value is lost:

Back in the parent method/frame, the `strMain` reference remains pointing to the original `"main"` value, which is what is printed:

```cs
Console.WriteLine(strMain); // output: main
```

**Why are "normal" objects different?**

The primary difference between the majority of objects and strings are that strings are immutable, while other objects are not.

For example, consider the following case where `MutableThing` is a mutable reference type (it has a property `ChangeMe` property that can be changed): 

```cs
using System;
    
class MutableThing
{
    public int ChangeMe { get; set; }
}
    
class Program
{
    static void DoSomething(MutableThing objLocal)
    {
        objLocal.ChangeMe = 0;
    }
    
    static void Main()
    {
        var objMain = new MutableThing();
        objMain.ChangeMe = 5;
        Console.WriteLine(objMain.ChangeMe); // it's 5 on objMain

        DoSomething(objMain);                // now it's 0 on objLocal
        Console.WriteLine(objMain.ChangeMe); // it's also 0 on objMain 
    }
}
```
When the `objMain` reference variable is passed into `DoSomething`, the reference variable is copied to `objLocal` but remains pointing to the original `MutableThing` instance.  So far, this is just the same as string case.  

The `DoSomething` method now follows the `objLocal` reference and updates the `ChangeMe` property of **the original object**.  At no point does a new `MutableThing` get created; only its properties have changed.

Again, as in the string case, when `DoSomething` returns, `objMain` remains pointing to the original object, with its now updated property, which is what is displayed.


The reason why this is the case is that it is not possible to update properties of a string; it is not possible, in C#, to do `strLocal[3] = 'H'`.  The only option is to create a while new string instead.

**What about the `ref` keyword?**

In the following example, the `ref` keyword is used:

```cs
void DoSomethingByReference(ref string strLocal)
{
    strLocal = "local";
}
void Main()
{
    string strMain = "main";
    DoSomethingByReference(ref strMain);
    Console.WriteLine(strMain);          // Prints "local"
}
```

In this case, rather than a copy being made of `strMain` when it is passed into `DoSomethingByReference`, the original reference is passed in.  The reference is genuinely passed by reference and stored in `strLocal`.  This means that when `strLocal` is re-pointed to a new value (`"local"`), it is actually overwriting the original object.  Hence why, in this case, `strMain` is found to have been changed to `"local"` when the stack returns to the `Main()` method. 

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-attribute"> 
  <button type="button" class="collapsible">+ Attributes
<code class="ex">
Attributes are metadata assigned to a specific object.
Defined by placing the attribute tag (enclosed in square brackets []) just about the relevant element.
Attributes should describe facts about the mechanism of the type or method, rather than their meaning.
Best practice is that all attributes be designed as sealed.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The .NET framework provides three pre-defined attributes:
  * `AttributeUsage`
    * Describes how a custom attribute class can be used.
  * `Conditional`
    * Indicates a method whose execution depends on a specified pre-processing identifier.
  * `Obsolete`
    * Marks a program entity that should not be used.

In addition it also allows for the creation of Custom Attributes.

**AttributeUsage**

The general syntax for this tag is:

```cs
[AttributeUsage (
   validon,
   AllowMultiple = allowmultiple,
   Inherited = inherited
)]
```

Where:

  * `validon` specifies the language elements on which the attribute can be placed. It is a combination of the value of an enumerator `AttributeTargets`. The default value is `AttributeTargets.All`.
  * `allowmultiple` (optional) is a boolean value that indicates whether the attribute can be applied multiple times to the same element.  The default is `false` (single-use).
  * `inherited` (optional) is a boolean value that indicates whether the attribute is inherited by derived classes. The default value is `false` (not inherited).

For example:

```cs
[AttributeUsage(
   AttributeTargets.Class |
   AttributeTargets.Constructor |
   AttributeTargets.Field |
   AttributeTargets.Method |
   AttributeTargets.Property, 
   AllowMultiple = true)]
```

**Conditional**

The general syntax for this tag is:

```cs
[Conditional(
   conditionalSymbol
)]
```
Where `conditionalSymbol` is the pre-processing identifier.

For example:

```cs
#define DEBUG
using System;
using System.Diagnostics;

public class Myclass {
   [Conditional("DEBUG")]
   
   public static void Message(string msg) {
      Console.WriteLine(msg);
   }
}
class Test {
   static void function1() {
      Myclass.Message("In Function 1.");
      function2();
   }
   static void function2() {
      Myclass.Message("In Function 2.");
   }
   public static void Main() {
      Myclass.Message("In Main function.");
      function1();
      Console.ReadKey();
   }
}
```

**Obsolete**

The general syntax for this tag is:

```cs
[Obsolete (
   message,
   iserror
)]
```

Where:

  * `message` is a string describing why the item is obsolete and what should be done instead.
  * `iserror` (optional) is a boolean value that indicates whether the compiler should treat the user of this item as an error.  The default is `false` (treat as warning).

For example:

```cs
using System;

public class MyClass {
   [Obsolete("Don't use OldMethod, use NewMethod instead", true)]
   
   static void OldMethod() {
      Console.WriteLine("It is the old method");
   }
   static void NewMethod() {
      Console.WriteLine("It is the new method"); 
   }
   public static void Main() {
      OldMethod();
   }
}
```

**Custom Attributes**

Custom attributes are used to store declarative information about an element, which can be retrieved at run-time.

There are four steps to creating a custom attribute:
   1. Declaring the attribute.
   1. Constructing the attribute.
   1. Applying the attribute to an element.
   1. Accessing the attribute through reflection.

For example, in the following example a `DebugInfo` attribute is declared:

```cs
//a custom attribute BugFix to be assigned to a class and its members
[AttributeUsage(
   AttributeTargets.Class |
   AttributeTargets.Constructor |
   AttributeTargets.Field |
   AttributeTargets.Method |
   AttributeTargets.Property,
   AllowMultiple = true)]

public sealed class DebugInfo : System.Attribute
```

Note that the class is `sealed`, to avoid it being overridden.

The class is now constructed with the following functionality:

```cs
{
   private int bugNo;
   private string developer;
   private string lastReview;
   public string message;
   
   public DebugInfo(int bg, string dev, string d) {
      this.bugNo = bg;
      this.developer = dev;
      this.lastReview = d;
   }
   public int BugNo {
      get {
         return bugNo;
      }
   }
   public string Developer {
      get {
         return developer;
      }
   }
   public string LastReview {
      get {
         return lastReview;
      }
   }
   public string Message {
      get {
         return message;
      }
      set {
         message = value;
      }
   }
}
```

It can then be applied to an element such as, in this case, `Rectangle`:

```cs
[DebugInfo(45, "Zara Ali", "12/8/2012", Message = "Return type mismatch")]
[DebugInfo(49, "Nuha Ali", "10/10/2012", Message = "Unused variable")]
class Rectangle {
   //member variables
   protected double length;
   protected double width;
   public Rectangle(double l, double w) {
      length = l;
      width = w;
   }
   [DebugInfo(55, "Zara Ali", "19/10/2012", Message = "Return type mismatch")]
   
   public double GetArea() {
      return length * width;
   }
   [DebugInfo(56, "Zara Ali", "19/10/2012")]
   
   public void Display() {
      Console.WriteLine("Length: {0}", length);
      Console.WriteLine("Width: {0}", width);
      Console.WriteLine("Area: {0}", GetArea());
   }
}
```

Finally, reflection is used to read the attributes for the element, and react accordingly:

```cs
using System.Reflection;

class Program
{
    static void Main(string[] args)
    {
        Rectangle r = new Rectangle(4.5, 7.5);
        r.Display();
        Type type = typeof(Rectangle);

        //iterating through the attribtues of the Rectangle class
        foreach (Object attributes in type.GetCustomAttributes(false))
        {
            DebugInfo dbi = attributes as DebugInfo;

            if (null != dbi)
            {
                Console.WriteLine("Bug no: {0}", dbi.BugNo);
                Console.WriteLine("Developer: {0}", dbi.Developer);
                Console.WriteLine("Last Reviewed: {0}", dbi.LastReview);
                Console.WriteLine("Remarks: {0}", dbi.Message);
            }
        }

        //iterating through the method attribtues
        foreach (MethodInfo m in type.GetMethods())
        {

            foreach (Attribute a in m.GetCustomAttributes(true))
            {
                DebugInfo dbi = a as DebugInfo;

                if (null != dbi)
                {
                    Console.WriteLine("Bug no: {0}, for Method: {1}", dbi.BugNo, m.Name);
                    Console.WriteLine("Developer: {0}", dbi.Developer);
                    Console.WriteLine("Last Reviewed: {0}", dbi.LastReview);
                    Console.WriteLine("Remarks: {0}", dbi.Message);
                }
            }
        }
        Console.ReadLine();
    }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-extensions"> 
  <button type="button" class="collapsible">+ Extension Methods
<code class="ex">
Allow additional methods to be injected into existing element at run-time.
Must be static, with the type to which it should be applied identified by the first parameter, which must be preceeded by the 'this' keyword.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Extension methods, as the name suggests, are additional methods. Extension methods allow you to inject additional methods without modifying, deriving or recompiling the original class, struct or interface. Extension methods can be added to your own custom class, .NET framework classes, or third party classes or interfaces.

**WARNING:** It is possible that a change to the implementation to which the extension method has been added could break the extension method, so they should be used carefully.

There are three significant features that define an extension method:
1. The method must be static.
1. The type of the first parameter of the method must be the type into which the method will be injected.
1. The first parameter of the method must be preceeded with the `this` keyword (all other parameters are treated as parameters of the method).

For example, in the following case, `this` indicates that the `FutureTime` method should be called on the `DateTime` object.

```cs
public static class MyExtensionMethods 
{ 
    public static DateTime FutureTime(this DateTime date, int days) 
    { 
        return date.AddDays(days); 
    } 
}
```

This can then be referenced in the code as a method of the `DateTime` object:

```cs
class Program
{
    static void Main()
    {
        // prints the date in 2 days time
        Console.WriteLine(DateTime.Now.FutureTime(2).ToShortDateString());
    }
}
```

Note that, in this case, the `this` keyword is unrelated to the `this` keyword used to identify local variables.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-stream"> 
  <button type="button" class="collapsible">+ Streams
<code class="ex">
Streams derived from System.IO.Stream and are used to read/write bytes to/from a resource.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Streams derive from the abstract `System.IO.Stream` class, which provides standard methods to transfer bytes from/to a source/target.

Common stream implementations are `FileStream`, `MemoryStream`, `BufferedStream`, etc.

In order for a stream to be accessed, it must be opened, however care must be taken to ensure it is also closed once it is no longer required.  Closing a stream is usually accomplished by wrapping it in a `using()` statement (although this could be achieved using a `try`/`finally` block as well, but in that case the `Dispose()` method will need to be called explicitly).

The following is an example of using a `FileStream` (note the `using` wrapper):

```cs
using System;
using System.IO;

class Program
{
    static void Main()
    {
        using(FileStream stream1 = File.Open("C:\\a", FileMode.Open))
        {
            Print(stream1);
        }
    }

    static void Print(Stream stream)
    {
        Console.WriteLine(stream.Length);
        Console.WriteLine(stream.Position);
    }
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-dispose"> 
  <button type="button" class="collapsible">+ `Close` vs `Dispose()` vs `Finalize()`
<code class="ex">
Close(): This is a legacy method that is typically the same as 'Dispose()'.  It is most commonly used
         to remove a connection to a resource (e.g. a file handle or stream).
Dispose(): Defined by the IDisposable interface.  Allows programmatic control of the freeing of both 
           managed and unmanaged resources.  Enables the use of the using() statement.
Finalize(): Defined on the base object class, this is automatically invoked by the Garbage Collector. 
            It should only be used to destroy unmanaged resource.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

**Close()**

The `Close()` method is the idiomatic opposite of the `Open()` method, which is typically used to open a connection to a resource.  It has subsequently been replaced by the `Dispose()` method, however remains for legacy support reasons.  It is not recommended that it be used, although conceptually it can be used in the following manner:

```cs
FileStream stream = null;
try
{
    stream = File.Open("C:\\a", FileMode.Open)
    // Do something with file   
} finally {
    stream.Close();
}
```

**Dispose()**

The `Dispose()` method, defined by the `IDisposable` interface, is the appropriate approach for disposing of managed and unmanaged resources within an object.

The following is one example of how 'Dispose()' may be called.

```cs
FileStream stream = null;
try
{
    stream = File.Open("C:\\a", FileMode.Open)
    // Do something with file   
} finally {
    stream.Dispose(); // internally calls Close()
}
```

A more sophisticated approach is to use a `using()` statement to wrap the object to be disposed.  If `IDisposable` is implemented, exiting the `using()` statement will result in `Dispose()` being called automatically.

```cs
using(FileStream file = new FileStream("C:\\a", FileMode.Open, FileAccess.Read))   
{  
    // Do something with file   
} 
```

**Finalize()**

The `Finalize()` method is also known as the destructor.  It cannot be called explicitly in the code; it can only be called by the Garbage Collector.  Also, the method cannot be implemented directly, but can be defined as a destructor (`~`) method, as shown in the following example:

```cs
public class MyClass: IDisposable {  
  
    //Construcotr   
    public MyClass() {  
        //Initialization:   
    }  
  
    //Destrucor also called Finalize   
    ~MyClass() {  
        this.Dispose();  
    }  
  
    public void Dispose() {  
        //write code to release unmanaged resource.   
    }  
} 
```

If a destructor is to be implemented, it is recommended that IDisposable also be implemented. 

The common use case for implementing a destructor is when an unmanaged resource is accessed (such as a stream or file handle).  If this resource is used in many places in the application, it may be unclear when the resource can be manually closed.  In this case, passing this responsibility to `Finaize()` means that the decision to close can be delegated to the Garbage Collector.

Note that calling `Finalize()` can be expensive, which is another reason to avoid using it unless necessary.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-string"> 
  <button type="button" class="collapsible">+ `string` vs `String` vs `StringBuilder`
<code class="ex">
In C#, there is no difference between `string` and `String` (the latter is effectively an alias for the former).
Changing (or concatentating) a `String` always results in a new `String` object.
Use `StringBuilder` for better performance when concatenating strings (except in one case, discussed inside).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

There is one case where using `String` is faster than using `StringBuilder`: if a string is created by concatenating multiple strings in the same declaration, this can be faster than producing the same string using multiple calls to `StringBuilder`.

i.e.

```cs
string a,b,c,d;
 a = b + c + d;
```

can be faster than:

```cs
string a,b,c,d;
StringBuilder e = new StringBuilder();
 e.Append(b);
 e.Append(c);
 e.Append(d);
 a = e.ToString();
```

This is because, under the covers, both `+` and `StringBuilder` defer to the same primitive, but, potentially, `StringBuilder` has a greater reallocation overhead.


Note that both of the above examples are normally faster than the following, although this can depend on how good a job the compiler does, since a well written compiler may compile this to `a = b + c + d` anyway:

```cs
string a,b,c,d;
 a = a + b;
 a = a + c;
 a = a + d;
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-equals"> 
  <button type="button" class="collapsible">+ `Equals()` vs `==`
<code class="ex">
Theorectically:
  Equals() : value comparison
        == : identify comparison
Although, for reference types the behaviour depends on the implementation, which can be overridden.
Particular care is required with a String that has been upcast to object.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Conceptually, `Equals()` checks whether two instances have equivalent values (a value comparison), while `==` checks whether two references are actually pointing at the same object (an identity comparison).

However, in practice the behaviour depends on the instances being tested.

  * For value types, both `Equals()` and `==` are functionally equivalent; both approaches check whether two instances have the same value.

  * For reference types, the behaviour of both of these equality tests depends on the underlying implementation, which can be overridden.
    * A notable exception to this rule is `String`, which is a reference type but behaves as a value type (and hence always performs a value comparison).
      * An exception to the exception is a `String` that has been upcast to `object`, in which case `==` will perform an identify comparison (when this occurs, a compile-time warning will be produced suggesting that the object should be explicitly cast to a 'String').

As a general rule of thumb, prefer `Equals()` if a value comparison is required and `==` if an identify comparison is required.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-type"> 
  <button type="button" class="collapsible">+ `typeof` vs `GetType()`
<code class="ex">
typeof(): get type at compile-time (can only be used on a class name)
GetType(): get type as run-time (can be used on a class name or instance)
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
object obj = "hello";
Console.WriteLine(typeof(object)); // ==> System.Object
//Console.WriteLine(typeof(obj)); // ==> compile-time error 
Console.WriteLine(obj.GetType()); // ==> System.String
```
</div>
</div>


<!-- =========================#####################################################================================ -->
<div id="interview-twoscomplement"> 
  <button type="button" class="collapsible">+ Two's Complement
<code class="ex">
A system for storing binary numbers that simplifies arithmetic.
The left-most (or "most signficant") bit indicates the parity of the number (0 = positive; 1= negative).
For negative binary numbers, 0 is treated as 1, and 1 is treated as 0.
For two's complement storage, 1 is added to the negative number.

Positive Number:  37 = 0 0 1 0 0 1 0 1
   Flipped Bits: ~37 = 1 1 0 1 1 0 1 0 (flipped using bitwise NOT operator: ~)
Negative Number: -37 = 1 1 0 1 1 0 1 1 (stored using two's complement, i.e. + 1)
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

To find the two's complement of a binary number, flip all of the bits (i.e. using `~`) and add one.

e.g., using 37 (only 8 bits are used, for brevity):

```
 37: 0 0 1 0 0 1 0 1
~37: 1 1 0 1 1 0 1 0
 +1: 1 1 0 1 1 0 1 1
```

So, in summary, `~37 + 1` equals `-37`.

To convert the resulting binary number back to base 10, ignore the left-most bit, then invert all bits (i.e. treat 0 as 1, and 1 as 0), then calculate from base 2 as normal.

**NOTE**: A shorthand way to calculate the two's complement is to find the first 1 when reading from the right and then flip all of the following digits.

To confirm that `11011010` is the inverse of `0100101`, calculate `37 + -37`:

```
   37:   0 0 1 0 0 1 0 1
+ -37:   1 1 0 1 1 0 1 0
   +1: 1 0 0 0 0 0 0 0 0
```

Since these integers only hold 8 bits, the 9th digit (1) is dropped, so the answer is 0 (as would be expected).

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-bitwise"> 
  <button type="button" class="collapsible">+ Bitwise Operators
<code class="ex">
Operators that operate on `int` and `uint` at a binary level. 
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

* `&` (bitwise AND)
* `|` (bitwise OR)
* `~` (bitwise NOT)
* `^` (bitwise XOR)
* `<<` (bitwise left shift)
* `>>` (bitwise right shift)

**NOTE**: 
  * Normally, an `int` and a `uint` take up 4 bytes, or 32 bits.  For the sake of simplicity, some of the following examples pretend that they take up only 1 byte, or 8 bits.
  * Reminder: 1 = true; 0 = false
  
In practice, in C#, bitwise operators are rarely used, except in very high-performance applications.  When used, they can also lead to confusing code, and so shoudl probably be avoided unless absolutely necessary.

<div id="interview-bitwise-amp"> 
  <button type="button" class="collapsible">+ &amp; (AND)
<code class="ex">
Compares the binary digits of two integers and returns 1 when both of the digits are 1 (a AND b).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

e.g.  `37 & 23`:

```
  37: 0 0 1 0 0 1 0 1
& 23: 0 0 0 1 0 1 1 1
=  5: 0 0 0 0 0 1 0 1
```

A common example of its use is to check the parity of a number (since the last binary digit is always 1 for an odd number):

```cs
private static bool isEven(int i)
{
    return (i & 1) == 0;
}
```

</div>
</div>

<div id="interview-bitwise-pipe"> 
  <button type="button" class="collapsible">+ &vert; (OR)
<code class="ex">
Compares the binary digits of a two integers and returns 1 when any of the digits are 1 (a OR b).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">
    
e.g.  `37 | 23`:

```
  37: 0 0 1 0 0 1 0 1
| 23: 0 0 0 1 0 1 1 1
= 55: 0 0 1 1 0 1 1 1
```

A practical example of its use is when indicating which combination of buttons to display on a dialog:

```cs
public partial class PopUpWindow : Form
{
    private static const int YES = 1;    // 00000001
    private static const int NO = 2;     // 00000010
    private static const int OKAY = 4;   // 00000100
    private static const int CANCEL = 8; // 00001000

    public static void ShowPopup(int buttons) // receives 00001011
    {
        if (buttons & YES)    // does 00001011 contain 00000001
        {
            // add YES button
        }

        if (buttons & NO)     // does 00001011 contain 00000010
        {
            // add NO button
        }
        
        if (buttons & OKAY)   // does 00001011 contain 00000100
        {
            // add NO button
        }
        
        if (buttons & CANCEL) // does 00001011 contain 00001000
        {
            // add NO button
        }
    }
}

class Program
{
    static void Main()
    {
        // passes an int that is 00001011
        PopupWindow.Show(PopupWindow.YES | PopupWindow.NO | PopupWindow.CANCEL);
    }
}
```

</div>
</div>

<div id="interview-bitwise-tilde"> 
  <button type="button" class="collapsible">+ ~ (NOT)
<code class="ex">
Inverts the parity of all of the bits in a number.
See the section on Two's Complement.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

e.g.  `~37`:

```
 37: 0 0 1 0 0 1 0 1
~37: 1 1 0 1 1 0 1 0
```

If the number is a `uint`, this result is 218 (2 + 8 + 16 + 64 + 128). As the type suggests, this will always be a positive number.

However, if the number is an `int`, the conversion is little more complex because the left-most (most signficant) binary digit of an `int` indicates the sign of the number.  To account for this, negative numbers are stored using the **two's complement** system.

To find the two's complement of a binary number, flip all of the bits (i.e. using `~`) and add one.

e.g., using 37:

```
 37: 0 0 1 0 0 1 0 1
~37: 1 1 0 1 1 0 1 0
 +1: 1 1 0 1 1 0 1 1
```

So, in summary, `~37 + 1` equals `-37`.

</div>
</div>

<div id="interview-bitwise-uparrow"> 
  <button type="button" class="collapsible">+ ^ (XOR)
<code class="ex">
Compares the binary digits of a two integers and returns 1 when one (and only one) of the digits are 1, otherwise it returns 0 (a XOR b).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

e.g.  `37 ^ 23`:

```
  37: 0 0 1 0 0 1 0 1
^ 23: 0 0 0 1 0 1 1 1
= 50: 0 0 1 1 0 0 1 0
```

XOR operator is actually quite a powerful operator, however use cases for it are not common (it was more common when systems were more memory-constrained).  

In C#, the most likely place to encounter it is when generating hash-codes:

```cs
public override int GetHashCode()
{
    unchecked // Overflow is fine, just wrap
    {
        int hash = 3049; // Start value (prime number).

        // Suitable nullity checks etc, of course :)
        hash = hash * 5039 + field1.GetHashCode();
        hash = hash * 883 + field2.GetHashCode();
        hash = hash * 9719 + field3.GetHashCode();
        return hash;
    }
}
```

Some things worth noting:

  * A^B == B^A
  * A^B^A == B
  * If you know A^B then it's impossible to tell what A and B are, but if you know one of them, you can calculate the other
  * The operator doesn't suffer from any overflows like multiplication/division/addition/subtraction.

One interesting edge-case: swapping two integer variables without an intermediary variable:

```cs
A = A^B // A is now XOR of A and B
B = A^B // B is now the original A
A = A^B // A is now the original B
```

</div>
</div>

<div id="interview-bitwise-lala"> 
  <button type="button" class="collapsible">+ &lt;&lt; (Bitshift Left)
<code class="ex">
Shifts the digits of a binary number to the left (and fills the gaps with 0).
Is the same as multiplying the base 10 number by 2 to the power of N.
e.g.  37 << 3 == 37 * Math.pow(2,3) == 37 * 8
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

e.g.  `37 << 3`:

(using a 32bit digit to avoid losing digits)

```
   37: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 1
 << 3: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0
= 296: 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 1 0 1 0 0 0
```

A practical use of `<<` is that it is significantly quicker than using `Math.Pow()`, if the goal is to multiply a number by 2 to the power of N.

e.g.

```cs
using System;
using System.Diagnostics;

class Program
{
    private static int iterations = 5000000;

    static void Main()
    {
        doCalc(useShift); // 22ms
        doCalc(usePow); // 180ms
    }

    private static double usePow()
    {
        return 37 * Math.Pow(2, 3);
    }

    private static double useShift()
    {
        return 37 << 3;
    }

    private static void doCalc(Func<double> calculator)
    {
        double x = 0;
        int iterLimit = iterations - 1;
        Stopwatch s = new Stopwatch();
        s.Start();

        for (int i = 0; i < iterLimit; i++)
            x = calculator();

        s.Stop();

        Console.WriteLine($"{x} : {s.ElapsedMilliseconds}");
    }
}
```

</div>
</div>

<div id="interview-bitwise-rara"> 
  <button type="button" class="collapsible">+ &gt;&gt; (Bitshift Right)
<code class="ex">
Shifts the digits of a binary number to the right (and fills the gaps with 0 if the number is positive, and with 1 if the number is negative).
Is the same as dividing the base 10 number by 2 to the power of N.
e.g.  37 >> 3 == 37 / Math.pow(2,3) == 37 / 8
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

e.g.  `37 >> 3`:

```
  37: 0 0 1 0 0 1 0 1
>> 3: 0 0 0 0 1 0 0 0
 = 4: 0 0 0 0 0 1 0 0
```

**NOTE**: `>>` only operates on `int`, so any decimal values will be lost (`37 / 8` = `4.625`, however `37 >> 3` = `4`).

A practical use of `<<` is that it is significantly quicker than using `Math.Pow()`, if the goal is to divide a number by 2 to the power of N.

e.g.

```cs
using System;
using System.Diagnostics;

class Program
{
    private static int iterations = 5000000;

    static void Main()
    {
        doCalc(useShift); // 22ms
        doCalc(usePow); // 180ms
    }

    private static double usePow()
    {
        return 37 * Math.Pow(2, 3);
    }

    private static double useShift()
    {
        return 37 << 3;
    }

    private static void doCalc(Func<double> calculator)
    {
        double x = 0;
        int iterLimit = iterations - 1;
        Stopwatch s = new Stopwatch();
        s.Start();

        for (int i = 0; i < iterLimit; i++)
            x = calculator();

        s.Stop();

        Console.WriteLine($"{x} : {s.ElapsedMilliseconds}");
    }
}
```

</div>
</div>

</div>
</div>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="data-structures">
<button type="button" class="collapsible">+ Data Structures</button>
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

<div>  
<button type="button" class="collapsible">+ Misc</button>  
<div class="content" style="display: none;" markdown="1">

Should create a separate page that goes through these in depth

### Array
See: [Arrays](http://zetcode.com/lang/csharp/arrays/)
And: [Join](https://www.geeksforgeeks.org/c-sharp-join-method-set-1/)  (and Split)

* Jagged Arrays


### ArrayList
### Stack
### Queue
### LinkedList<T> (Doubly-Linked List)

<!-- =========================#####################################################================================ -->
<div id="hashtable">
<button type="button" class="collapsible">+ Hash Tables</button>
<div class="content" style="display: none;" markdown="1">

There are three data structures based on hash table in C#:
   * `HashSet<T>`: Represents a set of values.  Uses generics.
   * `Hashtable`: Represents a collection of key/value pairs that are organized based on the hash code of the key.  It will return null if a key is not present.
   * `Dictionary<TKey, TValue>`: Similar to `Hashtable` but is generic.  It will throw an exception if a key is not present.  It is faster than `Hashtable` because there is no boxing or unboxing.

**Hash Table Principles**

* Hash tables assumes that each object has an associated hash code.
* Having the same hash code does not guarantee that two objects are equal, however two objects that are equal should have the same hash code.
* The main (if not only) purpose of a hash code is to be used as a key in a hash table (e.g. Dictionary<TKey, TValue>, HashSet<T>, etc.).
* Hash tables place items in buckets based on their hash code; the lookup efficiency depends on how evenly the items are distributed across the buckets.
* To ensure even distribution, the hash codes for the object should be similarly evenly distributed.
* The performance of hash tables can be increased if their capacity is known in advance (for example, the default capacity for a Dictionary is 16).

The pseudo-logic to add an item to a hash table is similar to the following:

```cs
// Calculate the hash code of the key
H = key.GetHashCode()
// Calculate the index of the bucket where the entry should be added
bucketIndex = H % B
// Add the entry to that bucket
buckets[bucketIndex].Add(entry)
```

The pseudo-logic to lookup an item in a hash table is similar to the following:

```cs
// Calculate the hash code of the key
H = key.GetHashCode()
// Calculate the index of the bucket where the entry would be, if it exists
bucketIndex = H % B
// Enumerate entries in the bucket to find one whose key is equal to the
// key we're looking for
entry = buckets[bucketIndex].Find(key)
```

Note that the lookup is essentially a lookup by index (`O(1)`), followed by an iterative search over a (hopefully) small number of items in the bucket (`O(n)`).

See the section on "Creating a Hash Code" for further details.

</div>
</div>

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

<!-- =========================#####################################################================================ -->
<div id="interview-list"> 
  <button type="button" class="collapsible">+ Common List Interfaces
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-enumerable"> 
  <button type="button" class="collapsible">+ IEnumerable vs IQueryable
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="keywords">
<button type="button" class="collapsible">+ Keywords</button>
<div class="content" style="display: none;" markdown="1">
    
<!-- =========================#####################################################================================ -->
<div id="interview-accessmodifiers"> 
  <button type="button" class="collapsible">+ Access Modifiers
<code class="ex">
public, internal protected, private, protected internal, private protected

Classes and interfaces can only be public or internal.

The default access for everything in C# is "the most restricted access you could declare for that member" (except in a property getter or setter, which inherits from the property).
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

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-privateconstruct"> 
  <button type="button" class="collapsible">+ Private Constructors
<code class="ex">
Private constructors are used to prevent a class being instantiated from outside.
This is most commonly encountered in singletons, or when used as base constructors.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

```cs
public class Foo
{
    private Foo() { }

    private static Foo FooInstance { get; set; }

    public static Foo GetFooInstance()
    {
        if (FooInstance == null) { FooInstance = new Foo(); }
        return FooInstance;
    }
}

class Program
{
    static void Main()
    {
        Foo foo = Foo.GetFooInstance();
    }
}
```

In addition to their use in singletons, private constructors can also be used as base constructors:

```cs
public class MyClass
{
    private MyClass(object data1, string data2) { }

    public MyClass(object data1)
        : this(data1, null) { }

    public MyClass(string data2)
        : this(null, data2) { }
        
    public MyClass()
        : this(null, null) { }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-partial"> 
  <button type="button" class="collapsible">+ Classes: `partial`
<code class="ex">
A class that is constructed from functionality defined in multiple files.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The functionality from multiple partial classes can be combined into a single class at run-time. 

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

<!-- =========================#####################################################================================ -->
<div id="interview-interfacevsabstract"> 
  <button type="button" class="collapsible">+ Classes: `interface` vs `abstract`
<code class="ex">
Interfaces allow multiple inheritance (composition - "has a"); abstract classes do not (inheritance - "is a").
Abstract classes have a constructor, interfaces cannot.
Abstract classes can have static members, interfaces cannot.
The members of an abstract class can have access modifiers, those in an interface cannot.
Abstract classes can provide implementation, interfaces cannot.

It is possible for a class to inherit methods with the same signature from multiple interfaces, however each method implementation needs to be accessed explicitly.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

An example of inheriting the same method signature from multiple interfaces:

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

<!-- =========================#####################################################================================ -->
<div id="interview-inheritaccessmodifiers"> 
  <button type="button" class="collapsible">+ Methods: `abstract`, `virtual`, `override` &amp; `new` 
<code class="ex">
a.k.a Inheritance Access Modifiers

abstract: cannot have functionality but can be overridden.
virtual: can provide a default implementation and can be overridden.
override: overrides the underlying implementation (but can access it via the base keyword).
new: renders the underlying implementation inaccessible.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

By definition, inheritance means that a sub-class contains all members of its direct super-class (except for constructors and destructors).  This includes all private members: they are inaccessible, but still occupy memory.

**`abstract` &amp; `virtual`**

* Abstract methods can only be declared in abstract classes.
* Virtual methods can be declared in any class.
* Abstract classes cannot be instantiated.
* An abstract sub-class can inherit from an abstract super-class without providing an implementation.
* A virtual method must provide a base implementation (even if that does nothing).

* In the abstract and virtual cases, use the `override` key word to provide an implementation in a sub-class.

**`new` &amp; `override`**

In a sub-class, the methods of the super-class can be overridden using either the `new` or `override` keywords.
  * `new`: in this case, the sub-class version of the method will be called if the super-class has been downcast to the sub-class (otherwise the super-class version will be called).
  * `override`: in this case, the sub-class version of the method will always be called, even if the sub-class has been upcast to the super-class.

**`base`**

Using the `base` keyword in a sub-class method will access the super-class version of the methods.

**Example**

*An example using `abstract` and `virtual`*:

```cs
using System;

public abstract class Vehicle
{
    public Vehicle() { }
    public abstract float MaxLoad { get; }
    public virtual int Wheels { get { return 4; } }
}

public class Truck : Vehicle
{
    private int wheels;
    private float loadPerWheel = 2500.0f;

    public Truck(int wheels) : base() { this.wheels = wheels; }
    public override float MaxLoad { get { return this.wheels * this.loadPerWheel; } }
    public override int Wheels { get { return this.wheels; } }
}

class Program
{
    static void Main(string[] args)
    {
        Vehicle truck = new Truck(12);
        Console.WriteLine($"The vehicle has {truck.Wheels} wheels and can carry {truck.MaxLoad} kgs");
    }
}
```

*An example using `new` and `override`*:

```cs
using System;

class BaseClass
{
    // can be overridden
    public virtual void Method1()
    {
        Console.WriteLine("Base - Method1");
    }

    // is not flagged as overridable
    public void Method2()
    {
        Console.WriteLine("Base - Method2");
    }

    // can be overridden
    public virtual void Method3()
    {
        Console.WriteLine("Base - Method3");
    }
}

class DerivedClass : BaseClass
{
    // override super-class
    public override void Method1()
    {
        Console.WriteLine("Derived - Method1");
    }

    // hide super-class
    public new void Method2()
    {
        Console.WriteLine("Derived - Method2");
    }

    // override super-class, but internally defer to super-class
    public override void Method3()
    {
        base.Method3();
    }
}

class Program
{
    static void Main(string[] args)
    {
        BaseClass bc = new BaseClass();       // instance of super-class
        DerivedClass dc = new DerivedClass(); // instance of sub-class
        BaseClass bcdc = new DerivedClass();  // instance of super-class downcast to sub-class

        bc.Method1();   // super-class dominates: "Base - Method1"
        bc.Method2();   // super-class dominates: "Base - Method2"
        bc.Method3();   // super-class dominates: "Base - Method3"
        
        dc.Method1();   // sub-class dominates: "Derived - Method1"
        dc.Method2();   // sub-class dominates: "Derived - Method2:"
        dc.Method3();   // sub-class defers to super-class: "Base - Method3"
        
        bcdc.Method1(); // sub-class dominates: "Derived - Method1"
        bcdc.Method2(); // super-class dominates: "Base - Method2"
        bcdc.Method3(); // sub-class defers to super-class: "Base - Method3"
    }
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-sealed"> 
  <button type="button" class="collapsible">+ Classes/Methods: `sealed`
<code class="ex">
Sealed classes cannot be inherited.
Sealed methods cannot be overridden.
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
* The class is an attribute that requires a very fast run-time look-up (sealed attributes have slightly better performance).

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-static"> 
  <button type="button" class="collapsible">+ Classes/Methods: `static`
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

Static constructors are typically used to initialize static fields, particularly if there are dependencies between static fields (using a static constructors allows the order of initialization to be controlled).

There are some rules governing static constructors:
  * A static constructor does not take access modifiers or have parameters.
  * A static constructor is called automatically to initialize the class before the first instance is created or any static members are referenced.
  * A static constructor cannot be called directly.
  * The user has no control on when the static constructor is executed in the program.

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

**Can you use `this` inside a static method in C#?**

No ...and yes.

Generally, no; in a static class there is no instance, so there is nothing for `this` to reference.

However, the `this` keyword is used in the context of extension methods, which are static, however the meaning is different.  In this case, `this` identifies the method as an extension and indicates the type on which the extension method should be called.

For example, in the following case, `this` indicates that the `FutureTime` method should be called on the `DateTime` object.

```cs
public static class MyExtensionMethods 
{ 
    public static DateTime FutureTime(this DateTime date, int days) 
    { 
        return date.AddDays(days); 
    } 
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-const"> 
  <button type="button" class="collapsible">+ Variables: `const` vs `read-only`
<code class="ex">
const: cannot be changed after compile-time; only applies to primitive types (it is implicitly static).  
       Should only be used if value will never, ever change.
read-only: can only be set when a class is instantiated (i.e. in the class declaration or constructor)
static readonly: effectively the same as const, although there are some significant subtleties (see inside).
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

This is because, being a `const`, the value of `CONSTANT_NUMBER` will be "baked" into the IL of Assembly B at compile-time, so it will ignore any subsequent changes to this value in Assembly A.

For this reason, it is recommended that `const` only be used if you know that this value will never, ever, *ever* change for any reason.  If you are unsure, use `readonly`. 

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-whilevsfor"> 
  <button type="button" class="collapsible">+ `while` vs `for`<br/>
<code class="ex">
For is used when number of repeats is known.
While is used when a sentinel loop is necessary.
Exactly the same after compilation.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-dowhilevswhile"> 
  <button type="button" class="collapsible">+ `while` vs `do-while`<br/>
<code class="ex">
Do-While is used if the loop should always runs at least once.
While is used if a test should be evaluated before the loop runs.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-continuevsbreak"> 
  <button type="button" class="collapsible">+ `continue` vs `break`
<code class="ex">
Break exists a loop.
Continue skips to the next iteration of a loop.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="async-await"> 
<button type="button" class="collapsible">+ `async` &amp; `await`
<code class="ex">
async: indicates that a method performs asynchronous actions.
await: indicates that the calling method should return immediately; 
       the rest of the calling method will complete once the awaited method returns.
</code>
</button>
<div class="content" style="display: none;" markdown="1">

If an `async` method calls another method or function using the `await` keyword, the calling method will return instantly at the point `await` is called; any instructions after the `await` will not complete until after the awaited method completes.

In the following example, the output from the program will be null, since `result` will not be initialized until after `Task.Delay(5)` returns, which will not happen until after WriteLine() is called.

```cs
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

<!-- =========================#####################################################================================ -->
<div id="interview-refvsout"> 
  <button type="button" class="collapsible">+ `ref` vs `out` vs `in`
<code class="ex">
ref: forces an existing object to be passed by reference into a method (in C#7, can also return by ref)
out: forces a method to assign a value to a variable before returning.
in: prevents a method from changing the passed in object.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

**`ref`**

The object being passed in must be initialized (even if only to `null`) before being passed in.

```cs
void DoSomething(ref string strLocal)
{
    strLocal = "local";
}
void Main()
{
    string strMain = "main";      // "main"
    DoSomething(ref strMain);
    Console.WriteLine(strMain);   // Prints "local"
}
```

In addition, in C# 7, the concept of a `ref` return was introduced:

```cs
public ref int Find(int number, int[] numbers)
{
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] == number) 
        {
            return ref numbers[i]; // return the memory location, not the value
        }
    }
    throw new IndexOutOfRangeException($"{nameof(number)} not found");
}

void Main()
{
    int[] array = { 1, 15, -39, 0, 7, 14, -12 };
    ref int place = ref Find(7, array); // returns memory location of 7 in the array
    place = 9; // overwrite memory location with 9
    Console.WriteLine(array[4]); // prints 9
}
```


**`out`**

The object being passed in need not be initialized before being passed in, however it must be assigned a value before the method returns.

```cs
void DoSomething(out string strLocal)
{
    strLocal = "local";
}
void Main()
{
    string strMain;        // null
    DoSomething(out strMain);
    Console.WriteLine(strMain);   // Prints "local"
}
```

**`in`**

`in` is a more recent addition to the language.  It is chiefly used for performance reasons when decalring a struct, to avoid it being modified.

Note that it only prevents a new reference being assigned; properties of reference types can still be updated.

```cs
  static void Enroll(in Student student)
  {
    // With in assigning a new object, this would throw a compilation error
    // student = new Student();

    // We can still do this with reference types though
    student.Enrolled = true;
  }
  
  static void Main()
  {
    var student = new Student
    {
      Name = "Susan",
      Enrolled = false
    };

    Enroll(student);
  }
```

For further information on `in`, see here:
  * [https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-7.2/readonly-ref#motivation](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-7.2/readonly-ref#motivation)

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-asvsis"> 
  <button type="button" class="collapsible">+ `as` vs `is`
<code class="ex">
is: verify that an object is of the specified type.
as: cast an object to the specified type; will return null if the object cannot be cast (or is null).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Generally speaking, `as` is a safer alternative to a traditional cast (e.g. `(List)myObject`), since it will not throw an exception if the cast cannot proceed.

**NOTE**: `as` cannot be used with value types.

**NOTE**: See the section on "Pattern Matching" for an additional use of `is`.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-patterns"> 
  <button type="button" class="collapsible">+ Pattern Matching (`is`, `when`)
<code class="ex">
is: verify that an object is of the specified type.
as: cast an object to the specified type; will return null if the object cannot be cast (or is null).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

In C# 7, the concept of pattern matching was introduced:

```cs
public void PrintStars(object o)
{
    if (o is null) return;     // constant pattern "null"
    if (!(o is int i)) return; // type pattern "int i"; if pattern match is successful, assign o to i
    WriteLine(new string('*', i));
}
```

The `when` keyword can be used in `switch` statements:

```cs
public void PrintArea(object shape)
{
    switch(shape)
    {
        case Circle c:
            WriteLine($"circle with radius {c.Radius}");
            break;
        case Rectangle s when (s.Length == s.Height):
            WriteLine($"{s.Length} x {s.Height} square");
            break;
        case Rectangle r:
            WriteLine($"{r.Length} x {r.Height} rectangle");
            break;
        default:
            WriteLine("<unknown shape>");
            break;
        case null:
            throw new ArgumentNullException(nameof(shape));
    }
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-exceptions"> 
  <button type="button" class="collapsible">+ `throw`
<code class="ex">
A stack-trace will start at the point that an exception is thrown (e.g. throw new Exception();).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

If an exception is caught, with the intention to rethrow, there are two approaches, each of which affects the stack-trace differently.

```cs
public void Method2() 
{ 
    try 
    { 
        Method1();
    } 
    catch (Exception) 
    {
        throw; // maintains the existing stack-trace
    } 
}
```
&nbsp;
```cs
public void Method2() 
{ 
    try 
    { 
        Method1();
    } 
    catch (Exception ex) 
    {
        throw ex; // resets the base of the stack-trace to this point
    } 
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-tryblock"> 
  <button type="button" class="collapsible">+ `try`, `catch` &amp; `finally`
<code class="ex">
try: to be useful, a try block requires either a catch or finally block (or both).
catch: this is optional; if missing, the exception will simply be thrown up the call-stack.
finally: this is optional; if the exception in the try block kills this process, this will not be executed!
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

A delegate can be used to create a try/catch method that can wrap any other method:

```cs
private void MyMethod()
{
    ...etc...

    if (TryExecute( () => AnotherMethod(myArg1, myArg2) ))
    {
        ...etc...
    }
}

private bool TryExecute(Action method)
{
    try
    {
        method();

        return true;
    }
    catch (Exception ex)
    {
        ...etc...
    }

    return false;
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-getset"> 
  <button type="button" class="collapsible">+ `get` &amp; `set`
<code class="ex">
Property getters and setters are used to provide a layer of abstraction on top of the internal private properties of class.

</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

The long-form of a property looks like this:

```cs
private string _firstName; 

public string FirstName 
{ 
    get 
    { 
        return this._firstName; 
    } 
    set 
    { 
        this._firstName = value; 
    } 
}
```

For trivial cases, this can be simplied to the following, which is known as an auto-implemented property:

```cs
public string FirstName { get; set; };
```

Since C# 6, it is possible to initialize auto-implemented properties in the following manner:

```cs
public string FirstName { get; set; } = "Jane";
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-yield"> 
  <button type="button" class="collapsible">+ `yield return`
<code class="ex">
Returns the current element of a list and waits for the next element to be requested.
For a method to use yield return, the return type must be IEnumerable or IEnumerable&lt;T&gt;.
The list resets to the beginning each time GetEnumerator() is called.
The Reset() method only works if this has been explicitly implemented in the enumerator (which it is not by default).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Consider the following example:

```cs
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        doTest(newEnumerator);      // ><
        doTest(reuseEnumerator);    // >he<
        doTest(foreachEnumerator);  // >hello<
    }

    private static void doTest(Action testYield)
    {
        Console.Write(">");
        testYield();
        Console.WriteLine("<");
    }

    private static IEnumerable<string> sayHello()
    {
        yield return "h";
        yield return "e";
        yield return "l";
        yield return "l";
        yield return "o";
    }
    
    // ...enumerator test methods...
}
```

In this first case, calling `GetEnumerator()` each time results in a new enumerator being created each time.  This means that the enumerator never moves beyond the first value.

Resulting output: `><`

```cs
    private static void newEnumerator()
    {
        Console.Write(sayHello().GetEnumerator().Current);
        sayHello().GetEnumerator().MoveNext();
        Console.Write(sayHello().GetEnumerator().Current);
        sayHello().GetEnumerator().MoveNext();
        Console.Write(sayHello().GetEnumerator().Current);
    }
 ```

In this second case, the same instance of `GetEnumerator()` is used for each call, which means that the enumerator processes across the list.

Resulting output: `>he<`

```cs
    private static void reuseEnumerator()
    {
        IEnumerator<string> text = sayHello().GetEnumerator();
        Console.Write(text.Current);
        text.MoveNext();
        Console.Write(text.Current);
        text.MoveNext();
        Console.Write(text.Current);
    }
```

In this third case, `foreach` automatically processes across the entire list.

Resulting output: `>hello<`

```cs
    private static void foreachEnumerator()
    {
        foreach (string c in sayHello())
            Console.Write(c);
    }
```

**Incomplete Lists**

A useful feature of lists that implement `yield return` is that the list can be processed even if it is not yet full (for example, in the case of a long running process).  As long at the elements already added to the list do not change, the enumerator can continue (otherwise an exception will be thrown and the enumerator invalidated).

Although `IEnumerator` does not have a `HasNext()` method, there is nothing to prevent the `Current` property being polled until an object is available (at which point `MoveNext()` can be called)

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-lazy"> 
  <button type="button" class="collapsible">+ `Lazy&lt;T&gt;`
<code class="ex">
Replaces: get { if (foo == null) foo = new Foo(); return foo; }
For example: Lazy&lt;Foo&gt; obj = new Lazy&lt;Foo&gt;(() => new Foo());

Access the object using: Foo foo = obj.Value;

Lazy&lt;T&gt; is thread-safe (however the object produced is not guaranteed to be thread-safe).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">
An alternative example:
  
```cs
public class Foo
{
    public int Id { get; set; }
    public Lazy<IList<Bar>> Bars => new Lazy<IList<Bar>>(() => GetBar(this.Id));
    private IList<Bar> GetBar(int Id)
    {
      // Write code here to retrieve all Bar details for the specified id.
    }
}
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-volatile"> 
  <button type="button" class="collapsible">+ `volatile`
<code class="ex">
Indicates that the field of a class of struct might be modified by multiple threads simultaneously.

Can be applied to most types, but not all (see inside).
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">
Can be applied to:
- Reference types.
- Pointer types (in an unsafe context). Note that although the pointer itself can be volatile, the object that it points to cannot. In other words, you cannot declare a "pointer to volatile."
- Simple types such as sbyte, byte, short, ushort, int, uint, char, float, and bool.
- An enum type with one of the following base types: byte, sbyte, short, ushort, int, or uint.
- Generic type parameters known to be reference types.
- IntPtr and UIntPtr.

Other types, including double and long, cannot be marked volatile because reads and writes to fields of those types cannot be guaranteed to be atomic. To protect multi-threaded access to those types of fields, use the Interlocked class members or protect access using the lock statement.
</div>
</div>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="performance"> 
  <button type="button" class="collapsible">+ Performance</button>   
<div class="content" style="display: none;" markdown="1">

<!-- =========================#####################################################================================ -->
<div id="interview-tips"> 
  <button type="button" class="collapsible">+ General Tips
<code class="ex">
All of these are rules of thumb and should not be taken as gospel (always benchmark!).
    
* Avoid instantiating large numbers of new objects (see the section on Object Pools)
* Avoid large structs.
* Prefer structs over classes for small, immutable objects.
* Prefer arrays over lists.
* Avoid boxing/unboxing.
* Prefer StringBuilder over string concatenation.
* Prefer for over foreach loops.
* Avoid performing calculations in the condition of a while/for loop.
* Prefer bitshift operators for arithmetic using powers of 2.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-caching"> 
  <button type="button" class="collapsible">+ Caching
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-objpool"> 
  <button type="button" class="collapsible">+ Object Pools
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-genericperf"> 
  <button type="button" class="collapsible">+ Generics<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="generics"> 
  <button type="button" class="collapsible">+ Generics</button>   
<div class="content" style="display: none;" markdown="1">
    
<!-- =========================#####################################################================================ -->
<div id="interview-genericconstraints"> 
  <button type="button" class="collapsible">+ Constraints on Generic Classes
<code class="ex">
public class MyGenericClass&lt;T&gt; where T : &lt;constraint&gt;
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Some examples:
 
  * public class MyGenericClass<T> where T : <interface name>
    * T must implement the specified interface

  * public class MyGenericClass<T> where T : <base class name>
    * T must extend the specified base class

  * public class MyGenericClass<T> where T : new()
    * T must have a parameterless constructor

  * public class MyGenericClass<T, U> where T : U 
    * T must derive from U

  * public class MyGenericClass<A, B, C> where B : C
    * B must derive from C

It is also possible to apply multiple constraints to the same class:

```cs
public class MyGenericClass<T, U> 
    where U : new() 
    where T : BaseClass, new()
```

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-covar"> 
  <button type="button" class="collapsible">+ Covariance vs Contravariance
<code class="ex">
Covariance and contravariance enable implicit reference conversion for array types, delegate types, and generic type arguments.

Covariance: Applies to return types; return a sub-class where a super-class is expected.

Contravariance: Applies to parameter types; accept a super-class where a sub-class is expected.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO: requires more explanation</span>

The following is taken from: [msdn-covariance-contravariance](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/covariance-contravariance/)

```cs
// Assignment compatibility.
string str = "test";  
// An object of a more derived type is assigned to an object of a less derived type.
object obj = str;  
  
// Covariance.
IEnumerable<string> strings = new List<string>();  
// An object that is instantiated with a more derived type argument
// is assigned to an object instantiated with a less derived type argument.
// Assignment compatibility is preserved.
IEnumerable<object> objects = strings;  
  
// Contravariance.
// Assume that the following method is in the class:
// static void SetObject(object o) { }
Action<object> actObject = SetObject;  
// An object that is instantiated with a less derived type argument
// is assigned to an object instantiated with a more derived type argument.
// Assignment compatibility is reversed.
Action<string> actString = actObject;
```

The following is taken from: [covariance-and-contravariance-real-world-example](https://stackoverflow.com/questions/2662369/covariance-and-contravariance-real-world-example)

```cs
// Contravariance
interface IGobbler<in T> {
    void gobble(T t);
}

// Since a QuadrupedGobbler can gobble any four-footed
// creature, it is OK to treat it as a donkey gobbler.
IGobbler<Donkey> dg = new QuadrupedGobbler();
dg.gobble(MyDonkey());

// Covariance
interface ISpewer<out T> {
    T spew();
}

// A MouseSpewer obviously spews rodents (all mice are
// rodents), so we can treat it as a rodent spewer.
ISpewer<Rodent> rs = new MouseSpewer();
Rodent r = rs.spew();
```

```cs
// Invariance
interface IHat<T> {
    void hide(T t);
    T pull();
}

// A RabbitHat…
IHat<Rabbit> rHat = RabbitHat();

// …cannot be treated covariantly as a mammal hat…
IHat<Mammal> mHat = rHat;      // Compiler error
// …because…
mHat.hide(new Dolphin());      // Hide a dolphin in a rabbit hat??

// It also cannot be treated contravariantly as a cottontail hat…
IHat<CottonTail> cHat = rHat;  // Compiler error
// …because…
rHat.hide(new MarshRabbit());
cHat.pull();                   // Pull a marsh rabbit out of a cottontail hat??
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-overloadgeneric"> 
  <button type="button" class="collapsible">+ Overloading a Generic Method
<code class="ex">
Method()
Method&lt;T&gt;(T t)
Method&lt;T&gt;(T t, int i)
Method&lt;T1, T2&gt;(T1 t1, T2 t2)
etc.
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

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="multithreading"> 
  <button type="button" class="collapsible">+ Multithreading</button>   
<div class="content" style="display: none;" markdown="1">
    
<!-- =========================#####################################################================================ -->
<div id="interview-threadvsprocess"> 
  <button type="button" class="collapsible">+ Thread vs Process
<code class="ex">
Process: the running program.
Thread: runs in the content of a process.
    
A thread is the basic unit to which the operating system allocates processor time. 
A thread can execute any part of the process code, including parts currently being executed by another thread.

Threads share heap memory with other threads, while processes have an isolated memory space.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

To start a process:

```cs
Process.Start("notepad.exe");
```

To start a thread:

```cs
Thread t = new Thread( ()=>{ 
            //code 
        } 
    ); 
t.Start();
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-deadlocks"> 
  <button type="button" class="collapsible">+ Locks, Semaphores &amp; Mutexes
<code class="ex">
lock: process-wide; locks a block of code so that only one thread can access it at a time.
    * Typically used to prevent deadlocks and concurrent access to memory.
semaphore: process-wide; locks a block of code so that a specific number of threads can access it at a time .
    * This is good for limiting memory use by an intensive task.
mutex: system-wide; locks a resource at an OS-level so that only one thread from one process can access it at a time.
    * A mutex can be used to synchronize access to a file, a database and so on.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

**Lock Example**

```cs
private readonly object syncLock = new object();
public void ThreadSafeMethod() {
    lock(syncLock) {
        /* critical code */
    }
}
```

**Semaphore Example** (taken from [what-is-a-semaphore](https://stackoverflow.com/questions/34519/what-is-a-semaphore)):

*Think of semaphores as bouncers at a nightclub. There are a dedicated number of people that are allowed in the club at once. If the club is full no one is allowed to enter, but as soon as one person leaves another person might enter.*

*It's simply a way to limit the number of consumers for a specific resource. For example, to limit the number of simultaneous calls to a database in an application.*

```cs
using System;
using System.Collections.Generic;
using System.Text;
using System.Threading;

namespace TheNightclub
{
    public class Program
    {
        public static Semaphore Bouncer { get; set; }

        public static void Main(string[] args)
        {
            // Create the semaphore with 3 slots, where 3 are available.
            Bouncer = new Semaphore(3, 3);

            // Open the nightclub.
            OpenNightclub();
        }

        public static void OpenNightclub()
        {
            for (int i = 1; i <= 50; i++)
            {
                // Let each guest enter on an own thread.
                Thread thread = new Thread(new ParameterizedThreadStart(Guest));
                thread.Start(i);
            }
        }

        public static void Guest(object args)
        {
            // Wait to enter the nightclub (a semaphore to be released).
            Console.WriteLine("Guest {0} is waiting to entering nightclub.", args);
            Bouncer.WaitOne();          

            // Do some dancing.
            Console.WriteLine("Guest {0} is doing some dancing.", args);
            Thread.Sleep(500);

            // Let one guest out (release one semaphore).
            Console.WriteLine("Guest {0} is leaving the nightclub.", args);
            Bouncer.Release(1);
        }
    }
}
```

**Mutex Example**

Taken from [what-is-a-good-pattern-for-using-a-global-mutex-in-c](https://stackoverflow.com/questions/229565/what-is-a-good-pattern-for-using-a-global-mutex-in-c):

```cs
using System.Runtime.InteropServices;   //GuidAttribute
using System.Reflection;                //Assembly
using System.Threading;                 //Mutex
using System.Security.AccessControl;    //MutexAccessRule
using System.Security.Principal;        //SecurityIdentifier

static void Main(string[] args)
{
    // get application GUID as defined in AssemblyInfo.cs
    string appGuid =
        ((GuidAttribute)Assembly.GetExecutingAssembly().
            GetCustomAttributes(typeof(GuidAttribute), false).
                GetValue(0)).Value.ToString();

    // unique id for global mutex - Global prefix means it is global to the machine
    string mutexId = string.Format( "Global\\{{{0}}}", appGuid );

    // Need a place to store a return value in Mutex() constructor call
    bool createdNew;

    // example of setting up security for multi-user usage
    // works also on localized systems (don't use just "Everyone") 
    var allowEveryoneRule =
        new MutexAccessRule( new SecurityIdentifier( WellKnownSidType.WorldSid
                                                   , null)
                           , MutexRights.FullControl
                           , AccessControlType.Allow
                           );
    var securitySettings = new MutexSecurity();
    securitySettings.AddAccessRule(allowEveryoneRule);

    // avoid race condition on security settings
    using (var mutex = new Mutex(false, mutexId, out createdNew, securitySettings))
    {
        var hasHandle = false;
        try
        {
            try
            {
                // note, may want to time out here instead of waiting forever
                // mutex.WaitOne(Timeout.Infinite, false);
                hasHandle = mutex.WaitOne(5000, false);
                if (hasHandle == false)
                    throw new TimeoutException("Timeout waiting for exclusive access");
            }
            catch (AbandonedMutexException)
            {
                // Log the fact that the mutex was abandoned in another process,
                // it will still get acquired
                hasHandle = true;
            }

            // Perform your work here.
        }
        finally
        {
            if(hasHandle)
                mutex.ReleaseMutex();
        }
    }
}
```

Additionally, a helper class for the mutex:

```cs
class SingleGlobalInstance : IDisposable
{
    //edit by user "jitbit" - renamed private fields to "_"
    public bool _hasHandle = false;
    Mutex _mutex;

    private void InitMutex()
    {
        string appGuid = ((GuidAttribute)Assembly.GetExecutingAssembly().GetCustomAttributes(typeof(GuidAttribute), false).GetValue(0)).Value;
        string mutexId = string.Format("Global\\{{{0}}}", appGuid);
        _mutex = new Mutex(false, mutexId);

        var allowEveryoneRule = new MutexAccessRule(new SecurityIdentifier(WellKnownSidType.WorldSid, null), MutexRights.FullControl, AccessControlType.Allow);
        var securitySettings = new MutexSecurity();
        securitySettings.AddAccessRule(allowEveryoneRule);
        _mutex.SetAccessControl(securitySettings);
    }

    public SingleGlobalInstance(int timeOut)
    {
        InitMutex();
        try
        {
            if(timeOut < 0)
                _hasHandle = _mutex.WaitOne(Timeout.Infinite, false);
            else
                _hasHandle = _mutex.WaitOne(timeOut, false);

            if (_hasHandle == false)
                throw new TimeoutException("Timeout waiting for exclusive access on SingleInstance");
        }
        catch (AbandonedMutexException)
        {
            _hasHandle = true;
        }
    }


    public void Dispose()
    {
        if (_mutex != null)
        {
            if (_hasHandle)
                _mutex.ReleaseMutex();
            _mutex.Close();
        }
    }
}
```

Usage:

```cs
using (new SingleGlobalInstance(1000)) //1000ms timeout on global lock
{
    //Only 1 of these runs at a time
    RunSomeStuff();
}
```
</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-threads"> 
  <button type="button" class="collapsible">+ Thread Management
<code class="ex">
SystemThread, ThreadPool, Delegate.BeginInvoke
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-interprocess"> 
  <button type="button" class="collapsible">+ Interprocess Communication
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-threadstates"> 
  <button type="button" class="collapsible">+ Thread States
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-threadparams"> 
  <button type="button" class="collapsible">+ Thread Parameters
<code class="ex">
Thread delegate can have a single object parameter.
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

<!-- =========================#####################################################================================ -->
<div id="interview-stopthread"> 
  <button type="button" class="collapsible">+ Stopping a Thread
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

<hr/>

<!-- =========================#####################################################================================ -->
<div id="config">
<button type="button" class="collapsible">+ Configuration</button>
<div class="content" style="display: none;" markdown="1">

<!-- =========================#####################################################================================ -->
<div id="interview-gc"> 
  <button type="button" class="collapsible">+ Garbage Collection<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-remoting"> 
  <button type="button" class="collapsible">+ .NET Remoting<br/>
<code class="ex">
Enables interprocess/domain communication (HTTP, TCP, and SMTP protocols)
Legacy feature.
Windows Communication Framework (WCF) is preferred (better performance, more flexible, HTTP, TCP, SMTP, named pipes, MSMQ)
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">WIP - requires expansion/clarification</span>

1. Makes reference to remotable object available to a client application (using an Activation URL).
1. Client application instantiates it (by connecting to the URL) .
1. Client use the remotable object as if it were a local object, however the actual code execution happens at the server-side. 
1. Remoting run-time creates a listener for the object when the server registers the channel that is used to connect to the remotable object. 
1. At the client side, the remoting infrastructure creates a proxy that stands-in as a pseudo-instantiation of the remotable object. 
1. The client does not implement the functionality of the remotable object, but presents a similar interface. 
1. The remoting infrastructure needs to know the public interface of the remotable object beforehand. 
1. Any method calls made against the object, including the identity of the method and any parameters passed, are serialized to a byte stream and transferred over a communication protocol-dependent Channel to a recipient proxy object at the server side ("marshalled"), by writing to the Channel's transport sink.
1. At the server side, the proxy reads the stream off the sink and makes the call to the remotable object on the behalf of the client. 
1. The results are serialized and transferred over the sink to the client, where the proxy reads the result and hands it over to the calling application.
1. If the remotable object needs to make a callback to a client object for some services, the client application must mark it as remotable and have a remoting run-time host a listener for it.
1. The server can connect to it over a different Channel, or over the already existent one if the underlying connection supports bidirectional communication.
1. A channel can be composed of a number of different Channel objects, possibly with different heterogeneous transports. 
1. Remoting can also work across systems separated by an interconnection of heterogeneous networks, including the internet.
1. Type safety is enforced by the Common Type System and the .NET Remoting run-time. 
1. Remote method calls are inherently synchronous; asynchronous calls can be implemented using threading libraries. 
1. Authentication and access control can be implemented for clients by either using custom Channels or by hosting the remotable objects in IIS and then using the IIS authentication system.

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-assemblyload"> 
  <button type="button" class="collapsible">+ `Assembly.LoadFrom()` or `Assembly.LoadsFile()`<br/>
<code class="ex">
LoadFrom: Searches for assembly, so could load wrong one (useful if don't know/care where assembly is)
LoadFile: Only loads from the specified path, so avoids risk of loading the wrong assembly.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-strongnaming"> 
  <button type="button" class="collapsible">+ Strongly Named Assemblies<br/>
<code class="ex">
Only strongly named assemblies can be included in GAC.
Creates a unique identifier for the assembly.
Slightly more secure than anonymous assemblies (will only access other strongly named assemblies).
Strong name verification can be disabled by user.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO: how to strongly name an assembly</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-cicd"> 
  <button type="button" class="collapsible">+ CI &amp; CD<br/>
<code class="ex">
CI: Continuous Integration - every push triggers a build and then runs tests before changes are integrated into master.
CD: Continuous Deployment - CI + deploys new release build to customers.
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-cloud"> 
  <button type="button" class="collapsible">+ Cloud vs On-Premise<br/>
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

<!-- =========================#####################################################================================ -->
<div id="interview-dllvsexe"> 
  <button type="button" class="collapsible">+ EXE vs DLL<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-gac"> 
  <button type="button" class="collapsible">+ The GAC<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-tddvsddd"> 
  <button type="button" class="collapsible">+ TDD &amp; DDD<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-compilation"> 
  <button type="button" class="collapsible">+ Compilation<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

<!-- =========================#####################################################================================ -->
<div id="interview-serialization"> 
  <button type="button" class="collapsible">+ XML vs Binary Serialization<br/>
<code class="ex">
TODO
</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

<span class="todo">TODO</span>

</div>
</div>

</div>
</div>

<hr/>

<!-- =========================#####################################################================================ -->
<div id="csharp8"> 
  <button type="button" class="collapsible">+ C# 8 Updates</button>   
<div class="content" style="display: none;" markdown="1">

[CSharp8CheatSheetUpdated.pdf](https://oclipa.github.io/assets/pdf/CSharp8CheatSheetUpdated.pdf)

* Default interface methods.
* Nullable reference types.
* Pattern matching enhancements.
* Asynchronous streams.
* Using declarations.
* Enhancement of interpolated verbatim strings.
* Null-coalescing assignment.
* Static local functions.
* Indices and ranges.
* Unmanaged constructed types.
* Readonly members.
* Stackalloc in nested expressions.
* Disposable ref structs.

</div>
</div>


<hr/>

&nbsp;

&nbsp;

&nbsp;

<hr/>

<strong>Move along; nothing to see here...</strong>

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

<!-- Default Statcounter code for C# Cheat Sheet
https://oclipa.github.io/csharp-cheat-sheet/ -->
<script type="text/javascript">
var sc_project=12408535; 
var sc_invisible=1; 
var sc_security="e03c2fdd"; 
</script>
<script type="text/javascript"
src="https://www.statcounter.com/counter/counter.js"
async></script>
<noscript><div class="statcounter"><a title="free web stats"
href="https://statcounter.com/" target="_blank"><img
class="statcounter"
src="https://c.statcounter.com/12408535/0/e03c2fdd/1/"
alt="free web stats"></a></div></noscript>
<!-- End of Statcounter Code -->
