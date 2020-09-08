<div style="display: inline-block;">
<a class="link" href="http://oclipa.github.io/">&lt; home</a>
<a class="link" href="http://oclipa.github.io/toolbox.html">&lt; toolbox</a>
</div> 

## C# (work-in-progress)

&nbsp;

<button type="button" id="toggle-all" value="none">Expand All Sections</button>

&nbsp;

-------------------------------------------------------------------------------------------------------

<div id="intro">  
<button type="button" class="collapsible">+ What is C#?</button>
<div class="content" style="display: none;" markdown="1">

C# is an object-oriented, type-safe, and managed language that is compiled by .Net framework to generate Microsoft Intermediate Language.

</div>
</div>

<div id="memory">
<button type="button" class="collapsible">+ Stack vs Heap</button>
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

</div>
</div>

<div id="structs">  
<button type="button" class="collapsible">+ Structs vs Classes</button>  
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
<button type="button" class="collapsible">+ Boxing vs Unboxing</button>
<div class="content" style="display: none;" markdown="1">

Boxing is the conversion of a value type to an reference type, or any interface face type implemented by the value type.

Boxing a value type creates an object instance containing the value and stores it on the heap.

e.g. `object o = 100;`

Unboxing is the reverse of this process:

e.g. `int x = (int)o;`

</div>
</div>

<div id="dependency">    
<button type="button" class="collapsible">+ Dependency Injection</button>   
<div class="content" style="display: none;" markdown="1">

* Constructor dependency
* Property dependency
* Method dependency

</div>
</div>

<div id="delegates">   
<button type="button" class="collapsible">+ Delegate vs Action vs Func vs Predicate</button>   
<div class="content" style="display: none;" markdown="1">

**Be sure to also read the section on Closures.**

   * ### Delegate:
      * An older, generic form of Action, Func and Predicate.
      * Nowadays, prefer Action and Func, which are generally less complex and easier to read.
      
```csharp
class Program
{
    public delegate int CalculateIt(int x, in y);

    static void Main(string[] args)
    {
        CalculateIt calc = Add;
        // Prints out "Result = 9"
        Console.WriteLine("Result = " + calc(4, 5));    

        calc = Subtract;
        // Prints out "Result = -1"
        Console.WriteLine("Result = " + calc(1, 2));
    }

    static int Add(int a, in b)
    {
        return a + b;
    }

    static void Subtract(int a, in b)
    {
        return a - b;
    }
}
```
      * TODO: A multicast delegate
      * Nowadays, prefer Action and Func, which are generally less complex and easier to read.

   * ### Action&lt;T&gt;: 
      * Return type must be `void`
      
```csharp
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

        Action<int, int> anonymousAction = (a, b) => { 
          Console.WriteLine("Result = " + (a + b)); 
        };

        // Prints out "Result = 9"
        anonymousAction.Invoke(4, 5);  
    }

    static void Add(int a, in b)
    {
        Console.WriteLine("Result = " + (a + b));
    }

    static void Subtract(int a, in b)
    {
        Console.WriteLine("Result = " + (a - b));
    }
}
```

   * ### Func&lt;T&gt;:
      * Must return a value

```csharp
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

    static int Add(int a, in b)
    {
        return a + b;
    }
    
    static int Subtract(int a, in b)
    {
        return a - b;
    }
}
```

   * ### Predicate&lt;T&gt;:
      * A special case of Func that only returns a bool.
      
</div>
</div>

<div id="closures">  
<button type="button" class="collapsible">+ Closures</button> 
<div class="content" style="display: none;" markdown="1">

Closures are used to encapsulate variables with the methods that require them.  

There are two basic uses cases:
1. Storing the state of data to be used in a particular method at a later time.
1. Hiding data but leaving it accessible to a particular method.

They are particularly relevant to Delegates (including Action, Func and Predicate), since they mean that the state of arguments can be read at the time they are called, not at the time they are instantiated.  However, this does means that care must be taken to ensure the correct values are applied.  

For example, in the following code the output will be the number 10 ten times, rather than the expected 0 to 9:

```csharp
delegate void Printer();

static void Main()
{
    List<Printer> printers = 
             new List<Printer>();
    
    int i=0;
    for(; i < 10; i++)
    {
        printers.Add(delegate { 
            Console.WriteLine(i); 
        });
    }

    foreach (var printer in printers)
    {
        printer();
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
<button type="button" class="collapsible">+ Linq</button> 
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
<button type="button" class="collapsible">+ Async & Await</button> 
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

<div id="static"> 
<button type="button" class="collapsible">+ Static Members</button>   
<div class="content" style="display: none;" markdown="1">

See [here](https://www.toptal.com/c-sharp/interview-questions) - see example using TestStatic class

</div>
</div>

<div id="interview-csharp"> 
<button type="button" class="collapsible">+ C# Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">

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

<div id="interview-accessmodifiers"> 
  <button type="button" class="collapsible">+ What are Class Access Modifiers?<br/>
    <code class="ex">
    public, internal protected, private, protected internal, private protected
    </code>
  </button>   
<div class="content" style="display: none;" markdown="1">

Modifiers are used to provide some control over how the API is used.

* `public` = Accessible anywhere within the project.
* `internal` = Accessible only within the assembly.
* `protected` = Accessible only within the current class and its derived classes.
* `private` = Accessible only within the current class.
* `protected internal` = Accessible anywhere within the assembly, and in any derived classes in the project.
* `private protected` = Accessible within any derived classes in the assembly. 

</div>
</div>

<div id="interview-whilevsfor"> 
  <button type="button" class="collapsible">+ What is the difference between a While and a For loop?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dowhilevswhile"> 
  <button type="button" class="collapsible">+ What is the difference between Do-While and a While loop?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-continuevsbreak"> 
  <button type="button" class="collapsible">+ What is the difference between Continue and Break?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-abstractvsvirtual"> 
  <button type="button" class="collapsible">+ What is the difference between Abstract and Virtual?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-partial"> 
  <button type="button" class="collapsible">+ What is a Partial Class?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-sealed"> 
  <button type="button" class="collapsible">+ What is a Sealed Class?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>


<div id="interview-interfacevsabstract"> 
  <button type="button" class="collapsible">+ What is the difference between an Interface and an Abstract Class?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-accessmodifiers"> 
  <button type="button" class="collapsible">+ What are Interface Access Modifiers?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-multipleinterfaces"> 
  <button type="button" class="collapsible">+ How can you use multiple Interfaces in a single Class?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-static"> 
  <button type="button" class="collapsible">+ What is the difference between Static and Non-Static?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-const"> 
  <button type="button" class="collapsible">+ What is the difference between Const and Read-Only?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-overload"> 
  <button type="button" class="collapsible">+ What is the difference between Overriding and Overloading?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hiding"> 
  <button type="button" class="collapsible">+ How can a method be hidden?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-privateconstruct"> 
  <button type="button" class="collapsible">+ Why used a Private Constructor?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-privateconstruct"> 
  <button type="button" class="collapsible">+ Why use a Static Constructor?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-string"> 
  <button type="button" class="collapsible">+ What is the difference between String and StringBuilder?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-passbyvalue"> 
  <button type="button" class="collapsible">+ What is Pass By Value?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-passbyrefeence"> 
  <button type="button" class="collapsible">+ What is Pass By Reference?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-refvsout"> 
  <button type="button" class="collapsible">+ What is difference between Ref and Out?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-boxing"> 
  <button type="button" class="collapsible">+ What are Boxing and Unboxing?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-structvsclass"> 
  <button type="button" class="collapsible">+ What is the difference between Struct and Class?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-asvsis"> 
  <button type="button" class="collapsible">+ What is the difference between As and Is?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-exceptions"> 
  <button type="button" class="collapsible">+ What is the difference between Throw Exception and Throw?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-tryblock"> 
  <button type="button" class="collapsible">+ Can you have a Try Block without a Catch?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-finally"> 
  <button type="button" class="collapsible">+ Why would you use Finally?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-attribute"> 
  <button type="button" class="collapsible">+ What is an Attribute?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-getset"> 
  <button type="button" class="collapsible">+ What are Get and Set?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-closure"> 
  <button type="button" class="collapsible">+ When would you use a Closure?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-caching"> 
  <button type="button" class="collapsible">+ What is Caching?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-genericconstraints"> 
  <button type="button" class="collapsible">+ Can you set Constraints on Generic Classes?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-extensions"> 
  <button type="button" class="collapsible">+ What are Extension Methods?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-anontype"> 
  <button type="button" class="collapsible">+ What is an Anonymous Type?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dllvsexe"> 
  <button type="button" class="collapsible">+ What is the difference between an EXE and a DLL?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-gac"> 
  <button type="button" class="collapsible">+ What is the GAC?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-objpool"> 
  <button type="button" class="collapsible">+ What is an Object Pool?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-defvsimed"> 
  <button type="button" class="collapsible">+ What is Deferred Execution vs Immediate Execution?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-stream"> 
  <button type="button" class="collapsible">+ What is a Stream?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-tddvsddd"> 
  <button type="button" class="collapsible">+ What are TDD and DDD?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-kiss"> 
  <button type="button" class="collapsible">+ What does KISS mean in OOP?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dry"> 
  <button type="button" class="collapsible">+ What does DRY mean in OOP?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-yagni"> 
  <button type="button" class="collapsible">+ What does YAGNI mean in OOP?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-tda"> 
  <button type="button" class="collapsible">+ What does TDA mean in OOP?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-inheritaccessmod"> 
  <button type="button" class="collapsible">+ What are Inheritance Access Modifiers?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-managed"> 
  <button type="button" class="collapsible">+ What is the difference between Managed and Unmanaged Code?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-stackvsheap"> 
  <button type="button" class="collapsible">+ What is the difference between the Stack and the Heap?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-compilation"> 
  <button type="button" class="collapsible">+ How is C# compiled?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-strongvsweak"> 
  <button type="button" class="collapsible">+ What is the difference between String and Weak Typing?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-equals"> 
  <button type="button" class="collapsible">+ What is the difference between `Equals()` and `==`?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-binding"> 
  <button type="button" class="collapsible">+ What is the difference between Early-Binding and Late-Binding?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-type"> 
  <button type="button" class="collapsible">+ What is the difference between `typeof` and `GetType()`?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-linq"> 
  <button type="button" class="collapsible">+ What is the difference between LINQ and Stored Procedures?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-staticthis"> 
  <button type="button" class="collapsible">+ Can you use `this` inside a static method in C#?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-delegate"> 
  <button type="button" class="collapsible">+ What are Delegates?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-serialization"> 
  <button type="button" class="collapsible">+ What is the difference between XML and Binary Serialization?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-genericperf"> 
  <button type="button" class="collapsible">+ How can you improve the Performance of Generic Classes?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-deadlocksql"> 
  <button type="button" class="collapsible">+ What is the difference between an SQL Deadlock and a C# Deadlock?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-reflection"> 
  <button type="button" class="collapsible">+ What is Reflection?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-yield"> 
  <button type="button" class="collapsible">+ What does `yield return` do?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-list"> 
  <button type="button" class="collapsible">+ What are some common List Interfaces?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-enumerable"> 
  <button type="button" class="collapsible">+ What is the difference between IEnumerable and IQueryable?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threadvsprocess"> 
  <button type="button" class="collapsible">+ What is the difference between a Thread and a Process?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-deadlocks"> 
  <button type="button" class="collapsible">+ How are Deadlocks handled in Multithreaded Processes?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threads"> 
  <button type="button" class="collapsible">+ How are Threads managed?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-interprocess"> 
  <button type="button" class="collapsible">+ How can you send data between Processes?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threadstates"> 
  <button type="button" class="collapsible">+ What states can a Thread have?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-solid"> 
  <button type="button" class="collapsible">+ What are the SOLID Principles?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-srp"> 
  <button type="button" class="collapsible">+ What is the SRP SOLID Principle?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-ocp"> 
  <button type="button" class="collapsible">+ What is the OCP SOLID Principle?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-lsp"> 
  <button type="button" class="collapsible">+ What is the LSP SOLID Principle?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-isp"> 
  <button type="button" class="collapsible">+ What is the ISP SOLID Principle?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-isp"> 
  <button type="button" class="collapsible">+ What is the DIP SOLID Principle?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-di"> 
  <button type="button" class="collapsible">+ What is Dependency Injection (DI)?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-ioc"> 
  <button type="button" class="collapsible">+ What is Inversion Of Control (IoC)?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-dispose"> 
  <button type="button" class="collapsible">+ What is the difference between Dispose and Finalize?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-gc"> 
  <button type="button" class="collapsible">+ How does Garbage Collection work?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-querycomp"> 
  <button type="button" class="collapsible">+ What is Query Comprehension/Syntax?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-covar"> 
  <button type="button" class="collapsible">+ In Generics, what is the difference between Covariance and Contravariance?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-remoting"> 
  <button type="button" class="collapsible">+ What is .NET Remoting?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(include comment about preference for WCF)

</div>
</div>

<div id="interview-assemblyload"> 
  <button type="button" class="collapsible">+ When would you use `Assembly.LoadFrom()` or `Assembly.LoadslFile()`?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-strongnaming"> 
  <button type="button" class="collapsible">+ What are the benefits of Strongly Named Assemblies?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-expressiontrees"> 
  <button type="button" class="collapsible">+ What are Expression Trees?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-cicd"> 
  <button type="button" class="collapsible">+ What is CI/CD?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-cloud"> 
  <button type="button" class="collapsible">+ What are differences between Cloud and On-Premise?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-threadparams"> 
  <button type="button" class="collapsible">+ Can a Thread have Parameters?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-overloadgeneric"> 
  <button type="button" class="collapsible">+ Can you overload a Generic Method?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-stopthread"> 
  <button type="button" class="collapsible">+ How can you Stop a Thread?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

<div id="interview-patterns"> 
<button type="button" class="collapsible">+ Patterns Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">
 
<div id="interview-builder"> 
  <button type="button" class="collapsible">+ What is the Builder Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-builder"> 
  <button type="button" class="collapsible">+ What is the Factory Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(see page 160)

</div>
</div>
  
<div id="interview-decorator"> 
  <button type="button" class="collapsible">+ What is the Decorator Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-chainofreponse"> 
  <button type="button" class="collapsible">+ What is the Chain of Responsibility Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(see page 158)

</div>
</div>

<div id="interview-adapter"> 
  <button type="button" class="collapsible">+ What is the Adapter Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-iterator"> 
  <button type="button" class="collapsible">+ What is the Iterator Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-nullobject"> 
  <button type="button" class="collapsible">+ What is the NullObject Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>
 
<div id="interview-visitor"> 
  <button type="button" class="collapsible">+ What is the Visitor Pattern?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>


</div>
</div>

<div id="interview-mvc"> 
<button type="button" class="collapsible">+ MVC Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">
 
<div id="interview-getvspost"> 
  <button type="button" class="collapsible">+ What is the difference between GET and POST?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-controller"> 
  <button type="button" class="collapsible">+ In MVC, what is a Controller?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-requestflow"> 
  <button type="button" class="collapsible">+ In MVC, what is the Request Flow?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-mvcdesc"> 
  <button type="button" class="collapsible">+ What is MVC?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-viewvssession"> 
  <button type="button" class="collapsible">+ What is the difference between ViewState and SessionState?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-xsd"> 
  <button type="button" class="collapsible">+ What is an XSD file?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-xml"> 
  <button type="button" class="collapsible">+ What is the difference between an XML Fragment and an XML Document?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-cors"> 
  <button type="button" class="collapsible">+ What is CORS?<br/>
    <code class="ex">xxxxxxxx</code>
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
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-gitpush"> 
  <button type="button" class="collapsible">+ What does `git push origin master` do?<br/>
    <code class="ex">xxxxxxxx</code>
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
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-htmlvscss"> 
  <button type="button" class="collapsible">+ Why is it a good idea to split HTML and CSS?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-classvsid"> 
  <button type="button" class="collapsible">+ What is the difference between Classes and Ids?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-marginvspadding"> 
  <button type="button" class="collapsible">+ What is the difference between Margin and Padding?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hyperlinks"> 
  <button type="button" class="collapsible">+ To which elements can a hyperlink be applied?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-doctype"> 
  <button type="button" class="collapsible">+ What is the significant of a DocType?<br/>
    <code class="ex">xxxxxxxx</code>
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
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-strict"> 
  <button type="button" class="collapsible">+ What does Strict mean?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-nan"> 
  <button type="button" class="collapsible">+ What does NaN mean?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-timers"> 
  <button type="button" class="collapsible">+ How do Timers work?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-timers"> 
  <button type="button" class="collapsible">+ How can you enumerate data types?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-eventbubble"> 
  <button type="button" class="collapsible">+ How do you define Event Bubbling?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-eventbubble"> 
  <button type="button" class="collapsible">+ How do you define Event Bubbling?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-typescript"> 
  <button type="button" class="collapsible">+ What is the difference between TypeScript and JavaScript?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-casesensitive"> 
  <button type="button" class="collapsible">+ Is JavaScript Case Sensitive?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-objinheritance"> 
  <button type="button" class="collapsible">+ How does Object Inheritance work in JavaScript?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-this"> 
  <button type="button" class="collapsible">+ How does the `this` keyword work in JavaScript?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(also include notes from section on page 139, related to arrow functions)

</div>
</div>

<div id="interview-ajax"> 
  <button type="button" class="collapsible">+ What is Ajax?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-privatemembers"> 
  <button type="button" class="collapsible">+ Can you have private members in JavaScript?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

(add notes from page 142, regarding true private methods)

</div>
</div>

<div id="interview-errors"> 
  <button type="button" class="collapsible">+ What are some types of JavaScript errors?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-arrays"> 
  <button type="button" class="collapsible">+ How can you empty an array?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hoisting"> 
  <button type="button" class="collapsible">+ What is Function Hoisting?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-deferred"> 
  <button type="button" class="collapsible">+ What is the Deferred Attribute?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-async"> 
  <button type="button" class="collapsible">+ What is the Async Attribute?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-innerhtml"> 
  <button type="button" class="collapsible">+ What does `.innerHTML()` do?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-appendchild"> 
  <button type="button" class="collapsible">+ What does `.appendChild()` do?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-eval"> 
  <button type="button" class="collapsible">+ What does `.eval()` do?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-hidecode"> 
  <button type="button" class="collapsible">+ How can you hide code?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

</div>
</div>

<div id="interview-js"> 
<button type="button" class="collapsible">+ SQL Interview Questions</button>   
<div class="content" style="display: none;" markdown="1">

<div id="interview-sqlcommands"> 
  <button type="button" class="collapsible">+ What are common SQL commands?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-sqlorder"> 
  <button type="button" class="collapsible">+ In what order should SQL commands be used?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-sqljoin"> 
  <button type="button" class="collapsible">+ What are the different types of Join?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-sqlcursor"> 
  <button type="button" class="collapsible">+ What is the SQL Cursor?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

</div>
</div>

<div id="interview-frag"> 
  <button type="button" class="collapsible">+ What is Index Fragmentation?<br/>
    <code class="ex">xxxxxxxx</code>
  </button>   
<div class="content" style="display: none;" markdown="1">

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
