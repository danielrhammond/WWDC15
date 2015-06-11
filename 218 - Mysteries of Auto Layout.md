# Mysteries of Auto Layout, Part 1 (218)

## UIStackView
- Built on top of auto layout, can incorporate custom constraints
- Horizontal or vertical
- Alignment control
- Distribution/fill control
- Is a UIView subclass so can be separately constrained itself with regular constraints
- `subviews` won’t be automatically arranged so can be used for decorators, `addArrangedSubview` and `arrangedSubviews`
- Performance improvement over using regular UIViews

## Changing Constraints
Don’t use addConstraint/addConstraints, use activate/deactivate instead. Benefit is that it finds its own optimized container to attach the constraints to, can better encapsulate without having to always have a reference to the views being constrained.

Keep a reference to constraints that you will need to mutate, don’t make assumptions on the contents of `-constraints` since you don’t own all of those constraints.

## View Sizing
- `intrinsicContentSize`, size derived from non-constraint internals (like text for labels or images for UIImageViews)
- override `intrinsicContentSize` if you’re doing custom drawing or a size that can’t be derived from constraints, if you override you are responsible for calling `invalidateIntrinsicContentSize` where appropriate
- Use manual constraints to do aspect ratio constraints with multipliers

## Self-sizing Table View Cells
- Width is already defined, your constraints need to result in a height given the specific width
- The requirement is that your constraints must adequately constrain the height of the contentView in the cell to get a result

## Priorities
Priorities range from 1-1000

```
	Required = 1000
	DefaultHigh = 750
	DefaultLow = 250
```

System Priorities - See NSLayoutConstraint header defines values for internal use, set around these values but not equal to

## Alignment
UITextView has a `firstBaseline` and `lastBaseline` (single line there will be equal). This is often preferable over using top and bottom when dealing with text.

Leading and Trailing helps solve for right-to-left localization. Best practice is to use leading and trailing over left/right

### Alignment Rects
Alignment rects should include the “critical content” only, isn’t effected by shadows or transformations. `alignmentRectInsets` helps override the calculation when you have a view that needs customization.





















