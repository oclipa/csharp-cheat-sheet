## Stack vs Heap

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
