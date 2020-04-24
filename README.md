<script type="text/javascript">

    function loadCSS(filename){ 

       var file = document.createElement("link");
       file.setAttribute("rel", "stylesheet");
       file.setAttribute("type", "text/css");
       file.setAttribute("href", filename);
       document.head.appendChild(file);
    }

   //just call a function to load your CSS
   //this path should be relative your HTML location
   loadCSS("collapse.css");
   
</script>  

<div>
    
<button type="button" class="collapsible">+ Stack vs Heap</button>
    
<div class="content" style="display: none;" markdown="1">

### Stack:
  * Contiguous memory.
  * A stack consists of frames; each frame corresponds to a method/function call.  A pointer references the current frame.
  * When a method is called, all of its value-types (and pointers) are stored as a frame which is pushed onto the top of the stack.
  * When the method returns, the frame for that method is popped off the stack (releasing the memory) and the pointer moves down to the next frame (i.e. the calling method).

### Heap:
   * Dynamic memory which can be allocated at will.
   * Can be fragmented since no guarantee which memory will be available at time oects are written.
   * Creating a reference-type oect reserves memory for the oect, plus overhead for the pointer, plus overhead for memory management.
   * When a reference-type oect is no longer referenced from the stack (or another oect), it is available to be garbage collected (which happens on occasion).

</div>

</div>

<div>
    
<button type="button" class="collapsible">+ Structs vs Classes</button>
    
<div class="content" style="display: none;" markdown="1">

### Structs:
```C#
public struct MyStruct
{
    public float number;
    public byte flags;
    public byte index;
}
```
  * Value-type (entire oect stored in a single memory location).
  * Allocated on the stack (if local to a function) or on the heap (if a class member).
  * Cannot be null (unless wrapped in a Nullable<> class)
  * Memory overhead is: (total size of fields) + (memory alignment padding)
  * Unless using the `ref` keyword, structs are always copied when passed into functions.
     * When using `ref` the stack address of the value type is passed, rather than a copy of the value type.
  * Once out of scope, memory location is immediately available to be overwritten.
  * Memory is contiguous, so may improve memory access patterns and CPU caching.
  
  * Cons: 
     * Cannot usually have multiple oects reference the same struct; each requires its own copy of the struct.
     * Large structs can be slow to copy, which can impact performance.
     * Boxing a struct (i.e. converting it in an oect) can impact performance

### Classes:
```C#
public class MyStruct
{
    public float number;
    public byte flags;
    public byte index;
}
```
   * Reference-type (oect is referenced by a pointer).
   * Allocated on the heap.
   * Can be null (if pointer is not assigned to a memory location)
   * Memory overhead is: (total size of fields) + (8 byte pointer) + (16 byte memory management).
   * References to a class are passed between methods (rather than the class itself).
   * Once out of scope, the memory location is available to be garbage collected (which may not happen immediately).
   * Memory can be fragmented.

  * Cons: 
     * Extra memory overhead (which may not be immediately removed when the oect is no longer referenced)
     * oects require initialization, which can impact performance.
     * Memory fragmentation can lead to slower performance.

</div>

</div>

<div>
    
<button type="button" class="collapsible">+ Delegate vs Action vs Func vs Predicate</button>
    
<div class="content" style="display: none;" markdown="1">

   * ### Delegate:
      * An older, generic form of Action and Func.
      * Nowadays, prefer Action and Func (less complex; easier to read)
      
```C#
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

   * ### Action&lt;T&gt;: 
      * Return type must be `void`
      
```C#
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
                    { Console.WriteLine("Result = " + (a + b)); };
                    
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

```C#
class Program
{
    static void Main(string[] args)
    {
        // note: Func<in, in, out>
        Func<int, int, int> calc = Add;
        // Prints out "Result = 9"
        Console.WriteLine("Result = " + calc(4, 5));    
 
        calc = Subtract;
        // Prints out "Result = -1"
        Console.WriteLine("Result = " + calc(4, 5));    
        
        Func<int, int, int> anonymousFunc = (a, b) => 
                { return a + b; };
                
        // Prints out "Result = 9"
        Console.WriteLine("Result = " + anonymousFunc.Invoke(4, 5));    
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

<div>
    
<button type="button" class="collapsible">+ Linq</button>
   
<div class="content" style="display: none;" markdown="1">

Further info: [https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable)

### Where
```C#
IEnumerable<TSource> result = 
    Where<TSource>(IEnumerable<TSource>, Func<TSource,Boolean>);

var result = source.Where(o => o.Prop == x);
```

### Select
```C#
IEnumerable<TSource> result = 
    Select<TSource,TResult>(IEnumerable<TSource>, Func<TSource,TResult>)

var result = source.Select(o => new 
                            { 
                                Prop1 = o.Prop1; 
                                Prop2 = o.Prop2 
                            }
                        );
```

### OrderBy
```C#
IEnumerable<TSource> result = 
    OrderBy<TSource,TKey>(IEnumerable<TSource>, Func<TSource,TKey>)

var result = source.OrderBy(o => o.Prop);
```

### OrderByDescending
```C#
IEnumerable<TSource> result = 
    OrderByDescending<TSource,TKey>(IEnumerable<TSource>, Func<TSource,TKey>)

var result = source.OrderByDescending(o => o.Prop);
```

### ThenByDescending
```C#
IEnumerable<TSource> result = 
    OrderBy[...].
    ThenByDescending(IEnumerable<TSource>, Func<TSource,TKey>);

var result = source.OrderBy(o => o.Prop1).
                    ThenByDescending(o => o.Prop2);
```

### Join
```C#
var result = source1.Join(source2, 
                     o1 => o1.Prop1, o2 => o2.Prop1, 
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
```C#
var result = source1.GroupBy(o => o.Prop).
                                 Select(grp => new
                                     {
                                         PropId = grp.Key,
                                         PropCount = grp.Count()
                                     });
```

### Take
```C#
// select top 3

var result = source.Where(
                     o => o.Prop == x).
                     Take(3);
```

### Skip
```C#
// uses a mixture of query syntax and lambda syntax

var result = (from o in source
                where o.Prop1 == x
                orderby o.Prop2
                select o).Skip(2).Take(3);
```

### Single
```C#
// throws an exception if no elements

var result = source.Single(o => o.Prop == x);
```

### SingleOrDefault
```C#
// returns null if no elements

var result = source.SingleOrDefault(o => o.Prop == x);
```

### DefaultIfEmpty
```C#
// returns a new OClass instance if no elements

var result = source.Where(o => o.Prop == x).
                        DefaultIfEmpty(new OClass()).Single();
```

### Last
```C#
// First, Last and ElementAt used in same way

var result = source.Where(o => o.Prop == x).
                        OrderBy(o => o.Prop).Last();
```

### SingleOrDefault
```C#
// returns 0 if no elements

var result = source.Where(o => o.Prop == x).
                      Select(o => o.Prop).SingleOrDefault();
```

### ToArray
```C#
// uses query syntax

string[] result = (from o in source
                select o.Prop).ToArray();
```

### ToDictionary
```C#
// uses lambda syntax

Dictionary<int, OClass> result = 
            source.ToDictionary(o => o.IntProp);

// uses a mixture of query syntax and lambda syntax

Dictionary<string, double> result = 
    (from og in
        (from o1 in source1
         join o2 in source2 on o1.Prop equals o2.Prop
         select new { o2.StrProp, o1.DblProp})
            group og by og.StrProp into g
            select g).
                ToDictionary(g => g.Key, 
                                g => g.Max(og => og.DblProp));
```

### ToList
```C#
// uses query syntax

List<OClass> result = (from o in source
                        where o.Prop > x
                        orderby o.Prop).ToList();
```

### ToLookup
```C#
ILookup<int, string> result = 
        source.toLookup(o => o.IntProp, o.StrProp);
```

</div>

</div>                  
                     
                     
<script type="text/javascript">

    var coll = document.getElementsByClassName("collapsible");
    var i;

    for (i = 0; i < coll.length; i++) {
      coll[i].addEventListener("click", function() {
        this.classList.toggle("active");
        var content = this.nextElementSibling;
        if (content.style.display === "block") {
          content.style.display = "none";
        } else {
          content.style.display = "block";
        }
      });
    }

</script> 
