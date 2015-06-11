# What’s New in Xcode (104)

# watchOS support
# swift 2
- error handling
- availability
- testability
- protocol extensions
- includes migration tool for swift 2

# objective-c
- generics for collections
- nullability annotations
- adopted across most of the SDKs

# playgrounds

## supporting sources
Breaks up playground into the interactive part and precompiled support code

## rich comments with markup

## pages 
For teaching content that is linked but is broken into pages

# App thinning

## Bitcode
App gets compiled to intermediate representation (LLVM ir?), uploaded to apple which lets them re-optimize with compiler updates in the future

## Slicing
Only includes the artwork required for the density the device requires

## On Demand Resources
Only download the resources as needed

# Address Sanitizer
Compiles objective-c and c code with special attention to memory management issues.

# Crash log management
Has a crash log viewer, similar featureset to hockeyapp/crashlytics but part of xcode.

# Testing

## UI Testing
KIF like integration tests, adds ability to record UI tests and have them automatically written. Runs in the simulator.

## Code Coverage
Measure amount of code coverage per methods called