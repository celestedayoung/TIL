# Is JavaScript an interpreted language?

`#Interpreted_Language` `#Compiled_Language` `#Just_In_Time` `#V8`

## ✓ Trigger

While studying JavaScript, upon encountering the statement "JavaScript engines evaluate literals at runtime, when the code is executed, to generate values," I began to think, 'JavaScript must be an interpreted language, right?'. So, I searched for more information, and I came across articles suggesting that JavaScript could also be seen as a compiled language. This prompted me to delve deeper into the topic, sparking my curiosity and prompting further investigation.

## ✓ Overview

> **_JavaScript is an interpreted language_**, not a compiled language. A program such as C++ or Java needs to be compiled before it is run. - web.stanford.edu

The source code undergoes a process called compilation, where it is translated into bytecode that the machine can execute. However, JavaScript operates differently. Instead of a compilation step, it relies on an interpreter within the browser to read through the code, interpret each line, and execute it. Modern browsers often utilize Just-In-Time (JIT) compilation, which compiles JavaScript into executable bytecode just before it is executed.

## ✓ After V8...

> V8 increases **_performance by compiling JavaScript_** to native machine code before executing it, versus executing bytecode or interpreting it. -V8, Chrome

JavaScript is not a statically typed language but rather a dynamically typed language, which means there are many unknown values before the source code is executed, making optimization difficult. Therefore, it adopts an interpretation approach where each line of code is interpreted as it is executed, rather than a compilation approach where all the source is interpreted at once. This is done with the following three benefits in mind:

1. Reduced memory usage: Compiling JavaScript code into bytecode is more convenient than compiling it into machine code.
2. Decreased parsing overhead: Bytecode is concise, making it easier to parse again.
3. Simplified compilation pipeline: Bytecode is advantageous even during optimizing or deoptimizing processes through TurboFan.

### V8 architecture

### Before V8 5.9 version

<img width="898" alt="past" src="https://github.com/celestedayoung/TIL/assets/144453750/83a39cde-af22-4801-ab70-7377c3ef4179">

In V8 engines prior to version 5.9, there were two compilers: `Full-codegen` and `Crankshaft`.

Full-codegen was a compiler used alongside `Ignition` to convert JavaScript code into bytecode for faster execution. `Crankshaft`, like `TurboFan`, compiled bytecode into optimized code.

However, the original intention of the V8 engine was to utilize only `Ignition` and `TurboFan`. In the early stages, the performance of these two was significantly lower, so both `Full-codegen` and `Crankshaft` were used together out of necessity. As a result, the structure was much more complex than it is today.

### Now

<img width="898" alt="now" src="https://github.com/celestedayoung/TIL/assets/144453750/322732b8-8924-4990-ac24-b3976cf72712">

As the V8 engine continued to evolve, the performance of Ignition and TurboFan improved significantly. Conversely, `Full-codegen` and `Crankshaft` were unable to keep up with the performance enhancements. Therefore, starting from version 5.9, these two components were removed from the engine.

### Interpreter-`Ignition`

Ignition is an interpreter that converts JavaScript code into bytecode. It translates the original source code into bytecode, which is easier for the computer to interpret. By minimizing the need for parsing the code frequently and reducing the amount of code, it efficiently manages memory space.

### Compiler-`TurboFan`

TurboFan is the optimization compiler that completely replaced the Crankshaft compiler used before V8 version 5.9. It is responsible for optimizing JavaScript code. TurboFan is employed to minimize the frequent conversion of code into bytecode.

During runtime, V8 instructs its buddy, `Profiler`, to gather data such as the frequency of function or variable calls. Utilizing this collected data, TurboFan optimizes the code according to its criteria.

## ✓ Then, can JavaScript be considered a compiled language?

- While JavaScript undergoes JIT compilation before execution, it differs from traditional compiled languages in the sense that compilation occurs in real-time during program execution.
- Typically, compiled languages compile the entire source code into machine code at once. JavaScript, on the other hand, undergoes compilation even during execution. This is why JavaScript is often classified as an "interpreted language," but due to JIT compilation producing machine code, it can also be considered a compiled language.
- Ultimately, this means that JavaScript doesn't strictly belong to either category of traditional compiled or interpreted languages.

---

### references

https://developer.mozilla.org/ko/docs/Web/JavaScript
https://v8.dev/blog/ignition-interpreter
https://web.stanford.edu/class/cs98si/slides/overview.html
https://docs.google.com/presentation/d/1OqjVqRhtwlKeKfvMdX6HaCIu9wpZsrzqpIVIwQSuiXQ/edit#slide=id.g1453eb7f19_5_51
https://en.wikipedia.org/wiki/Just-in-time_compilation
https://velog.io/@seungchan__y/자바스크립트는-Compiler-Interpreter-언어다
