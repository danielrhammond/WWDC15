# Swift in Practice (411)

## Availability Checking

Compiler in swift 2 will check at compile time to ensure that the apis used are available on the deployment target. The fixit for this error will add a guard for the correct `#availability` version

### Why check based on version

- Features and users are tied to OS versions
- Checking runtime availability doesn’t actually guarantee expected behavior (ex: internal APIs)

### guard makes this nice (less nesting)

```
guard #available(ios 9.0, *) else { return }
let stack = UIStackView()
```

### annotation

functions can be annotated with `@available(iOS 8.0, *)` you ensure the same safety for your internal code and can factor out code paths that can only be called on certain versions without duplicate checks

## Enforcing Application Constraints

### Asset Catalog Identifiers

`let fooImage = UIImage(named: “foo”)!`

You have to force unwrap because your identifiers are “stringly” typed. Solution is to codify the type as an application specific enum:

```
extension UIImage {
	enum AssetIdentifier: String {
		case Isabella = “Isabella”
		case Foo = “Foo”
	}

convenience init!(identifier: AssetIdentifier) {
	return UIImage…
}
```

#### Benefit
- Centrally located constants
- Doesn’t pollute global namespace
- Must use one of the enum cases and results in a non-failable initializer

### Constrained protocol extension

```
extension SegueHandlerType where Self: UIViewController {
    // can add methods only where the implementer of SegueHandlerType is a UIViewController
}
```
