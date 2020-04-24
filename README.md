<script type="text/javascript">

    function loadCSS(filename){ 

       var file = document.createElement("link");
       file.setAttribute("rel", "stylesheet");
       file.setAttribute("type", "text/css");
       file.setAttribute("href", filename);
       document.head.appendChild(file);
    }
    
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

## Stack vs Heap

<div>
    
<button type="button" class="collapsible">Open Collapsible</button>
    
<div class="content">

Stack:
  * Contiguous memory.
  * A stack consists of frames; each frame corresponds to a method/function call.  A pointer references the current frame.
  * When a method is called, all of its value-types (and pointers) are stored as a frame which is pushed onto the top of the stack.
  * When the method returns, the frame for that method is popped off the stack (releasing the memory) and the pointer moves down to the next frame (i.e. the calling method).

Heap:
   * Dynamic memory which can be allocated at will.
   * Can be fragmented since no guarantee which memory will be available at time objects are written.
   * Creating a reference-type object reserves memory for the object, plus overhead for the pointer, plus overhead for memory management.
   * When a reference-type object is no longer referenced from the stack (or another object), it is available to be garbage collected (which happens on occasion).

</div>

</div>

## Structs vs Classes

Structs:
```
public struct MyStruct
{
    public float number;
    public byte flags;
    public byte index;
}
```
  * Value-type (entire object stored in a single memory location).
  * Allocated on the stack (if local to a function) or on the heap (if a class member).
  * Cannot be null (unless wrapped in a Nullable<> class)
  * Memory overhead is: (total size of fields) + (memory alignment padding)
  * Unless using the `ref` keyword, structs are always copied when passed into functions.
     * When using `ref` the stack address of the value type is passed, rather than a copy of the value type.
  * Once out of scope, memory location is immediately available to be overwritten.
  * Memory is contiguous, so may improve memory access patterns and CPU caching.
  
  * Cons: 
     * Cannot usually have multiple objects reference the same struct; each requires its own copy of the struct.
     * Large structs can be slow to copy, which can impact performance.
     * Boxing a struct (i.e. converting it in an object) can impact performance

Classes:
```
public class MyStruct
{
    public float number;
    public byte flags;
    public byte index;
}
```
   * Reference-type (object is referenced by a pointer).
   * Allocated on the heap.
   * Can be null (if pointer is not assigned to a memory location)
   * Memory overhead is: (total size of fields) + (8 byte pointer) + (16 byte memory management).
   * References to a class are passed between methods (rather than the class itself).
   * Once out of scope, the memory location is available to be garbage collected (which may not happen immediately).
   * Memory can be fragmented.

  * Cons: 
     * Extra memory overhead (which may not be immediately removed when the object is no longer referenced)
     * Objects require initialization, which can impact performance.
     * Memory fragmentation can lead to slower performance.

## Delegate vs Action vs Func vs Predicate

   * Delegate:
      * An older, generic form of Action and Func.
      * Nowadays, prefer Action and Func (less complex; easier to read)
```
class Program
{
    public delegate int CalculateIt(int x, in y);
    
    static void Main(string[] args)
    {
        CalculateIt calc = Add;
        Console.WriteLine("Result = " + calc(4, 5));    // Prints out "Result = 9"
        
        calc = Subtract;
        Console.WriteLine("Result = " + calc(1, 2));    // Prints out "Result = -1"
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

   * Action&lt;T&gt;: 
      * Return type must be `void`
```
class Program
{
    static void Main(string[] args)
    {
        Action<int, int> calc = Add;
        calc(4, 5);           // Prints out "Result = 9"
 
        calc = Subtract;
        calc(4, 5);           // Prints out "Result = -1"
        
        Action<int, int> anonymousAction = (a, b) =>  { Console.WriteLine("Result = " + (a + b)); };
        anonymousAction.Invoke(4, 5);  // Prints out "Result = 9"
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
   * Func&lt;T&gt;: 
      * Must return a value
```
class Program
{
    static void Main(string[] args)
    {
        Func<int, int, int> calc = Add;                 // note: Func<in, in, out>
        Console.WriteLine("Result = " + calc(4, 5));    // Prints out "Result = 9"
 
        calc = Subtract;
        Console.WriteLine("Result = " + calc(4, 5));    // Prints out "Result = -1"
        
        Func<int, int, int> anonymousFunc = (a, b) => { return a + b; };
        Console.WriteLine("Result = " + anonymousFunc.Invoke(4, 5));    // Prints out "Result = 9"
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

   * Predicate&lt;T&gt;: 
      * Basically, a special case of Func, which returns a bool.


## Linq

Further info: [https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable)

```
IEnumerable<TSource> result = Where<TSource>(IEnumerable<TSource>, Func<TSource,Boolean>);

var result = source.Where(obj => obj.Property == x);
```
```
IEnumerable<TSource> result = Select<TSource,TResult>(IEnumerable<TSource>, Func<TSource,TResult>)

var result = source.Select(obj => new 
                    { 
                        Property1 = obj.Property1; 
                        Property2 = obj.Property2 
                    }
                );
```
```
IEnumerable<TSource> result = OrderBy<TSource,TKey>(IEnumerable<TSource>, Func<TSource,TKey>)

var result = source.OrderBy(obj => obj.Property);
```
```
IEnumerable<TSource> result = OrderByDescending<TSource,TKey>(IEnumerable<TSource>, Func<TSource,TKey>)

var result = source.OrderByDescending(obj => obj.Property1);
```
```
IEnumerable<TSource> result = OrderBy[...].ThenByDescending(IEnumerable<TSource>, Func<TSource,TKey>);

var result = source.OrderBy(obj => obj.Property1).
                    ThenByDescending(obj => obj.Property2);
```
```
var result = source1.Join(source2, 
                     obj1 => obj1.Property1, obj2 => obj2.Property1, 
                     (obj1, obj2) => new 
                         {
                             obj1.Property1,
                             obj1.Property2,
                             obj2.Property3,
                             obj2.Property4
                         }
                     );
```
```
var result = source1.GroupBy(
                     obj => obj.Property).
                     Select(grp => new
                     {
                         PropertyId = grp.Key,
                         PropertyCount = grp.Count()
                     });
```
                     
                     
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
