Whats New in Swift (106)

# Fundamentals
## enums
- print out debug values
- supports associated types
- recursive enum
## do
Introduces a explicit scope, helps with error. do/while -> repeat
## Option sets
- representing sets of booleans, can do bitwise operations
- can now be used as a set `[.Repeat, .CurveEaseIn]`
- Can create your own option set, create a struct implementing OptionSetType (implemented through default implementation in protocols!)
## Functions & Methods
Both work the same way in terms of argument labels/defaults, no change for functions imported from C. Argument labels are expected as part of pure swift api for functions now. Can customize argument label 
```
func save(name name : String, encrypt : Bool) // save(name: “foo”, encrypted: true)
func save(name : String, _ encrypt : Bool) // save(“foo”, true)
```
## Diagnostics
Better error messages around mutability safety. Other new warnings
# SDK Improvements
## Integration
Better integration of swift and objective-c. Adoption of best practices on obj-c code, nullability qualifiers, objective-c typed collections, NS_ENUM, NS_Options, etc…
## Testing + access control
Unit tests use @testable, public and internal symbols now available, same optimizations/collision prevention exist in release builds
## Rich Comments 
Documentation comments can include markup like syntax
# Pattern Matching
## guard
great for early exits, your else exits the current scope (return, break, abort, throw), ensures that after the fall through compiler can assume the inverse

guard let name = json[“name”] as? String {
    return nil
}
name.doSomething() // no optional
## Pattern Matching with if case
`if case .MyEnumCase(let value) = bar() where value != 42 {}`
## for … in filtering
`for value in mySequence where value != “” {}`
# API availability
- Compiler now warns on apis that you call not available on min deployment target
- `if #available(OSX 10.10.3, *) { // run if 10.10.3 }`
# Protocol extensions
Can add extensions to protocols, provide implementation for methods
Lots of global functions are becoming methods:
`filter(map(numbers) {$0 * 3}) { $0 >= 0}`
numbers.map({$0 * 3}).filter({$0 >= 0})
# Error handling
## Trivial Errors -> Optionals
## Logic Errors -> Should abort program
## Detailed recoverable errors (NSError in cocoa)
	`try`
	by default functions can’t throw, makes explicit what can with `throws` keyword in method
	`do`/`catch` pattern match against protocol ErrorType (NSError conforms)
		`catch let error` global catch and assign to error
		`catch NSURLError.somelongErrorType` catch one error type
	Impossible errors use `try!`, will abort execution if the code throws
### `defer { … }` will execute at end of scope regardless of how scope is ended (via throwing, returning, etc…)
### Swift error handling is more balanced performance wise, similar performance to “if”, can use error paths 
### Automatically incorporated into most cocoa APIs
