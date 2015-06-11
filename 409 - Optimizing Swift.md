Optimizing Swift Performance (409)

# Compiler optimizations
Array bounds checks optimizations, lots of other stuff

# Use struct/value type over reference types
Since value types do not require ARC, performance benefits exist when looping/storing in arrays, passing, etc…

When a struct contains a reference, you lose this benefit

Use a Wrapper type to encapsulate multiple references in one within a struct to minimize overhead (Friday 2:30 building better apps with Value Types)

# Generics
*example* `min<T: Comparable>(x: T, y: T) -> T {}`

Compiler must copy/release all x/y’s in case they are reference types, and perform indirection via function table to be safe. 

The compiler can replace functions with generics with specific versions to avoid this overhead, but only in the case where the compiler has access to the generic definition when compiling (in same file or with Whole Module Optimization is on)

# Dynamic dispatch
Compiler can only call methods directly if it can prove that there are no overrides in any subclasses. Use final on any APIs where it does not make sense to override.

Also ensure that private methods are private not just for encapsulation but also to avoid dynamic dispatch cost associated with calling private methods.

# Instruments
New heaviest trace detail on time profiler is nice (in assistant). TURN ON WHOLE MODULE OPTIMIZATION ON RELEASES


