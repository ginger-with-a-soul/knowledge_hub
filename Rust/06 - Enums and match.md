# Enums:
* In Rust, enum can also hold data similarly like struct does. The power of enums in Rust lies in the fact that individual fields of your enum can hold different data types, and even other enums, custom data types and structs. Because of this, enum can initialize that value by calling an initialization function which is quite strange compared to other languages:
![[Enum with a struct type.png]]
* Enums also support methods, defined like we did with structs:
![[Enum method.png]]
* In Rust, signifying that [[An encyclopedia of Computer Science references#Meaning of null values | a value might be missing]] is implement using an Enum so important that is already included into prelude (already imported into every source file). This is the `Option<T>` enum that looks like this:
```rust
enum Option<T> {
	None,
	Some(T),
}
```
* Looking at this, you could again argue that you could still be using this enum that stores your value in type `T` erroneously - thinking it for sure contains your value. However, Rust compiler will not let you use `Option<T>` with anything unless you've made sure you have your `T` inside. And only after that could you perform operations defined for your data type `T`. Getting your `T` outside of the `Option<T>` can be done using a variety of methods defined on this enum type. Overall guidance is that wherever you have an `Option<T>` type, you need to have 2 branching decisions being made depending on the contents of your `Option` instance - is it a `None` or is it a `Some<T>`.
# Match:
* A way of branching the `Option` is by using a `match` control flow construct. This is a very powerful construct in Rust. It can be compared with `switch` from C and `match` that was introduced into 3.10 Python. In Rust, `match` needs to be **exhaustive**. For example, if you pass an enum to it, it has to have implemented actions for every possible value that that enum defined. Otherwise the compiler will throw a compile time error. One of the ways you can achieve this requirement w/out implementing an action for every possible value (for example an action is shared for multiple different enum values) is by specifying the **catch-all pattern** which is placed as a last match 'arm'. This option binds any value, that went through the sieve above, to the specified variable and in the action for that match arm you can use this variable. If for any reason you do not care about the catch-all arm, instead of specifying a variable that an action HAS to use, your variable name can be just `_` which is also called a **placeholder**. Doing so, you will not get a warning from compiler about an unused variable. This placeholder can go along a ***unit value*** which is an empty tuple, which we specify in the actions part of the arm to signify we do not want to execute any code as an action for that arm:
![[Match with placeholder and unit value.png]]