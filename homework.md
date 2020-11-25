# **Difference between Chrome V8 vs Mozilla’s Spider Monkey**
The main difference between chrome’s V8 Engine and Mozilla’s SpiderMonkey lies in ECMAScript conformance Test262 
which is used to check how closely JavaScript implementation follows the ECMAScript 5th edition specification standards, 
created by ECMA International. This test consists of thousands of individual tests, which checks the requirement of the specification.
### Conformance test: ###
1. Chrome’s V8 Engine -> 98%
1. Mozilla’s SpiderMonkey -> 87%
The tracing JIT as implemented in SpiderMonkey can produce extremely specialized code compared to a whole-method JIT, 
since it has already executed the code and can speculate on the types of variables (such as treating the index variable
in a for loop as a native integer), where a whole-method JIT would have to treat the variable as an object because JavaScript
is untyped and the type could change (SpiderMonkey will simply "fall off" trace if the assumption fails, and return to interpreting
bytecode). However, SpiderMonkey's tracing JIT currently does not work efficiently on code with many branches, as the traces are optimized
for single paths of execution. In addition, there's some overhead involved in monitoring execution before deciding to compile a trace, and
then switching execution to that trace. Also, if the tracer makes an assumption that is later violated (such as a variable changing type), 
the cost of falling off trace and switching back to interpreting is likely to be higher than with a whole-method JIT.
V8 is the fastest, because it compiles all JS to machine code.
SpiderMonkey (what FF uses) is fast too, but compiles to an intermediate byte-code, 
not machine code. That's the major difference with V8. EDIT- Newer Firefox releases 
come with a newer variant of SpideMonkey; TraceMonkey. TraceMonkey does JIT compilation 
of critical parts, and maybe other smart optimizations.
[geeksforgeeks](https://www.geeksforgeeks.org/what-happens-inside-javascript-engine/)
[stackoverflow](https://stackoverflow.com/questions/2137320/javascript-engines-advantages#:~:text=V8%20is%20the%20fastest%2C%20because,the%20major%20difference%20with%20V8.&text=TraceMonkey%20does%20JIT%20compilation%20of,and%20maybe%20other%20smart%20optimizations.)
