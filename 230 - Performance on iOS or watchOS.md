# Performance on iOS and watchOS (230)

## Why performance

Users like responsive apps, be a good neighbor on multitasking on iPad (hah), efficient apps save battery power.

## Choosing technologies

Know the technologies and then pick the best one. (was that really necessary?)

## Profiling

Use Instruments.app, code-level instrumentation 

## App Memory

Xcode debugger, Instruments (Allocations, Leaks)

## Code instrumentation

Use `CFAbsoluteTimeGetCurrent()` and subtract end from start. 

## Animations

60fps son

## Responsiveness

How you react to user input. 100ms is the threshold for user perception), make sure you test on the oldest supported hardware (fuck the A5)

## Don’t guess

Don’t tweak performance related code without measuring

## Perform experiments

1. Reproduce
2. Profile
3. Measure
4. Make code change based on hypothesis

## Don’t block

When you have a blocking call replace it with non-blocking or use GCD

## Memory

Reclaiming memory takes time, sudden high-memory demand impacts responsiveness. The more efficient you are in the background the less aggressively your process will be killed.

## watchOS Performance Strategies

- send appropriately sized and formatted responses
- send resized images
- Use app context to update bi-directional shared state
- When impossible to resize on the server, use the iPhone to resize/process content etc… (Use `WCSession`)

## Summary

- Performance is a feature
- Efficient apps are nice
- Learn about everything then make right choices (/s)
- Optimize downloads
