Swift and Objective-C Interoperability (401)
Jordan Rose

# Exposing methods from swift to objective-c
- Non-private, non swift features (enum, tuple) subclasses of NSObject
- Will warn now for swift methods that can’t conform to delegate (without @objc annotation)
- @IBOutlet, @IBAction, @NSManaged will all expose to obj-c
- `dynamic` will also expose as it gets replaced with KVC at runtime (?)
- `@objc` is most broad, try to use more explicit
- Note can use `@objc(selectorName:)` gives a method an arbitrary selector name, *new* @nonobjc explicitly declares a method as not accessible in obj-c
# Function pointers
`@convention(c)` creates a c function pointer from a closure and allows you to capture values from scope
# Error handling
## Objective-C > Swift
- Objective-C nullable results (where null also vends an NSError) will be turned to optional response and a throwable
- Objective-C boolean resutlt + NSErrorPointer then it gets turned to void + throw
- Other NSError’s get left alone
## Swift > Objective-C
Will automatically add the `error:` argument label/NSError pointer to methods that `throw`
## Handling Cocoa Errors
Most common error types in SDK are exposed as swift enums, “should just work”
# Nullability for Objective-C
Indicate whether objective-c/c pointer to determine whether it can be nil
## nullable
Maps to swift optional (ex: `UIView?`)
## nonnull
No change to compiler output, but communicates that (ex: `UIView`)
## null_unspecified
neither of the other specifiers applies, remains as a implicitly  unwrapped optional (ex: `UIView!`) 
## Audited region
`NS_ASSUME_NONNULL_BEGIN`/`NS_ASSUME_NONNULL_END`
single-level pointsers assumed to be nonnull
NSError** parameters assumed to be nullable for both levels (? is this just NSError or any double pointer ?)
# Nullability for C
prefix all qualifiers with `__` but follows the pointer
# Collection types in Objective-C
`NSArray<UIView *> *subviews` will warn against using less specific 
## Defining lightweight generics
```
@interface NSDictionary<KeyType, ObjectType> (TypedLookups)
- (ObjectType)objectForKey:(KeyType)…
@end
```
Type erasure model provides binary compatibility, which means no changes to the objective-c runtime, and no code generation changes (but obviously provides no real safety)
# Kindof
Many `id`-vending APIs actually mean “some subclass of ____”
with `__kindof` it describes a type as some sort of subclass
ex: `extern __kindof NSApplication *NSApp`
Implicitly converts to superclasses and subclasses
# Don’t use id
Can almost always use more specific type annotation:
- instancetype
- typed collections for most collections
- `__kindof X *`
- `id <SomeProtocol>`