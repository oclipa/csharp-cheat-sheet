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
