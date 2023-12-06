## Need to know basis

### Common questions
**Q. Which types are not allowed within an *enum* variant's body?**
A. *Zero-sized types* i.e **Structs, Trait objects, Floating-point numbers**

**Q. How can we avoid memory allocations when writing to a file in rust?**
A. 
- Use the equivalent Rust code with no locks or allocations
- Explicitly **deref** the reference to reassign
- Take an existing custom allocator, like **wee_alloc**, fork it, and modify it to never allocate to the area of memory you want to preserve.

**Notes**
- It’s  `format!`  that allocates. It evaluates to a **String**, and **String** is heap-backed.
If you want to avoid allocation, use write!  instead.

**Q. Are closures types in Rust?**
A. Rust closure type is a type of **anonymous function** that can capture values from the scope in which it’s defined.

**Q. Can closures in rust be returned directly from a function?**
A. 
- There is **no way to return** from a function within a closure in Rust
- Closures **don't have a concrete** type that's **returnable**, so it's not possible to use the function pointer **fn** as a return type
- However, as of **Rust 1.26**, you can use **impl** trait to return an unboxed closure
- You *cannot* capture a **potentially uninitialized** value in a closure, but you can fix this by using **Option**

**Q. Which type cast preserves mathematical value in all cases?**
A. i32 as i64

**Q. Is an emoji a string literal?**
A. **You can include  **emojis**** in **a  **liter**al** String **or  **Chara**cter** expression by setting it off with double quotes. The type inferrer will default the expression to a S**tring  **li**teral**, unl**ess the  **Ch**aracter** type is specified

**Q. What cannot be destructured in rust?**
A. In Rust, almost everything can be destructured using pattern matching and the destructuring syntax. However, there are a few types of structures or patterns that do not support destructuring. Here are some examples:

1.  **Structs without Named Fields:** If a struct does not have named fields, you cannot destructure its values by name. For example:
    
    rustCopy code
    
    `// This struct can be destructured
    struct Point {
        x: i32,
        y: i32,
    }
    
    let point = Point { x: 10, y: 20 };
    let Point { x, y } = point;
    
    // This tuple struct cannot be destructured by name
    struct TuplePoint(i32, i32);
    
    let tuple_point = TuplePoint(10, 20);
    // This will result in an error
    // let TuplePoint { 0: x, 1: y } = tuple_point;` 
    
2.  **Tuples with Different Types:** If a tuple contains elements of different types, you cannot destructure it directly. Tuples are homogeneous collections of elements.
    
    ```rust
    // This tuple can be destructured
    let tuple = (10, 20);
    let (x, y) = tuple;
    
    // This tuple with different types cannot be destructured
    let mixed_tuple = (10, "hello");
    // This will result in an error
    // let (a, b) = mixed_tuple;
    ```
    
3.  **Arrays with Dynamic Size:** Arrays in Rust have a fixed size determined at compile time. If you try to destructure an array into a different size, it will result in a compile-time error.
    
 ```rust
   // This array can be destructured
    let array = [1, 2, 3];
    let [a, b, c] = array;
    
    // This will result in a compile-time error
    // let [x, y] = array;
   ```
   
It's important to note that Rust's compiler is designed to catch these errors at compile time, providing safety and preventing runtime errors related to restructuring.

**Q. What does the ? operator do in rust?**
A. It is a convenience offered by Rust, that eliminates boilerplate code and makes function's implementation simpler.

**Notes**
- Not to be confused with actual `.unwrap()` which panics in the case of an error.
- It is used for `propagating errors`. Sometimes we write code that might fail but we do not want to catch and handle error immediately. Your code will not be readable if you have too much code to handle the error in every place. Instead, if an error occurs, we might want to let our caller deal with it. We want errors to propagate up the call stack.
```rust
```rust
 // file type is Result if "?" is not used
 // file:Result<File,Error>
 let mut file = File::create("foo.txt");

 // file type is File if "?" is used
 // file:File
 let mut file = File::create("foo.txt")?;
 // if an error occurs, code after this line will not be executed
 // function will return the error
```

**Q. What are the benefits of Generics?**
A. 
- A generic function is a function that can accept one or more generic type parameters.
- Generic functions are useful because they make code more flexible and prevent code duplication.
- Generic types can be used in collections, structures, enums, and traits. Generic types are specified in the signature of the function where the datatype of parameters and return type are declared.

**Q. What is the use of the pub keyword?**
A. To tell Rust to **make** a **function** public, we add the **pub** keyword to the start of the declaration. 

**Q. What is X-Ray tracing on the function(s) in your application?**
A. AWS X-Ray tracing is a user-friendly and detailed service that allows users to trace their **lambda functions** and generate statistics such as response time, annotations, and response codes.
