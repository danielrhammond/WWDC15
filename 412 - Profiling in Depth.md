# Profiling in Depth (412)

## Creating Instruments 7
- Look and feel
- New graphing styles
- Faster rendering

## Process
1. Prototype rewrite of critical component (ex: graph rendering) in isolated app
2. Set performance budget/requirements (100k data points, 60fps on iPad Mini 1st gen)

## Backtrace Example

*insert some assembly code*

Time Profiler samples CPU activity at 1k hertz and then traces back the frame pointers from current stack to build up a stack/backtrace.

## Tail Call Elimination

*Excellent but very visual explanation in the talk*

### Disabling
`CFLAGS=“-fno-optimize-sibling-calls”` this disables the TCE which might help with creating more accurate backtraces when profiling (but at performance cost)

### How to tell if a ARM32-bit
- TCE will be Branch and Link instruction (bl)
	- sets “lr” to next address and jumps
- Regular calls use simple branches (b)

## Evaluating Multithreaded Performance
By zooming in a lot you can see when CPUs are on/off (rather than average usage, and can answer the question of “Is this work successfully being parallelized?”

## objc_msgSend
There’s no compile time optimization on classes/objects because implementations can be swapped. Cacheing the function pointer helps, but you still have to marshal arguments, push stack, etc…

What you really want when you are trying to get rid of objc_msgSend is to inline the given function. 

Swift helps in this case because its only dynamic when it needs to be.

## Record waiting threads
By default time profiler doesn’t record idle threads so if you have issues with lock contention etc… it might be helpful to use the record waiting threads option

## Invert Call Tree
Start from lower call tree functions, helpful when there are multiple entry points to your hottest code paths