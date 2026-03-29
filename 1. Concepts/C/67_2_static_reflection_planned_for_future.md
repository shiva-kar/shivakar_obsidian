### 67.2 Static Reflection (planned for future)

- Compile-time introspection of class structure.
   **Static reflection** is a programming feature that allows a program to inspect its own code and structure at **compile time** rather than runtime. Unlike dynamic reflection which occurs while the program is running, static reflection uses information collected during the compilation process to generate optimized code or perform compile-time checks. This leads to higher performance and zero-overhead abstractions, and is especially useful in statically-typed languages like C++. 

Key characteristics

- **Compile-time process:** All reflection and code generation happens during the compilation phase, before the program is executed.
- **Compiler-based:** The compiler is responsible for collecting type and code information and using it to transform the code.
- **High performance:** Because it runs at compile time, it can lead to highly optimized code without the performance overhead associated with runtime reflection.
- **Compile-time safety:** The use of compile-time checks can catch errors early in the development process.
- **Limited by compiler knowledge:** It can only be used on code that the compiler knows about, as it relies on information available during compilation. 

Example scenarios

- **Code generation:** Automatically generating code for tasks like serialization, data validation, or creating boilerplate code based on a class's structure.
- **Compile-time validation:** Performing type-checking or other checks at compile time to ensure the generated code is correct and meets specific requirements.
- **Metaprogramming:** Creating complex compile-time algorithms or abstractions, such as creating a  a make_integer_sequence for a specific type.