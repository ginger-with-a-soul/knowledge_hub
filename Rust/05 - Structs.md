* An entire instance of a struct must be mutable if want to have any field mutable. In other words, you cannot have a mutable field and a non mutable instance of a struct - no shit Sherlock.
* You can instantiate a struct via function arguments in a shorthand format if the argument name corresponds to the key name that a struct expects to have:
![[Shorthand struct creation.png]]
* Creating a copy of an instance with certain changed fields can be done quickly as well:
*![[Struct update syntax.png]]

* However, be careful about creating a copy as if there is any field you're *copying* but it does not implement a **Copy** behaviour (like `Username` that is a String in this example), it will be used a **Move**, making our 'original' instance invalid as a field has moved to another instance. 
* A **tuple struct** is a special type of struct that should be used when we require our tuples to have a name but we do not care about the names of the individual fields, we only care about their data type. A tuple struct can be constructed as follows:
![[A tuple struct.png]]
* Structs can also store references to data owned by something else, but for that we'll need to specify **lifetimes**. 
* A struct does not know how to represents itself to the world when we call `println!("{}")` unless we implement a `Display` formatter for it. This formatter is implicitly called by using placeholder - `{}` as is meant for the end user to see. However, we can also try to use a `Debug` formatter by using `{:?}` instead of the `{}` placeholder. Before we can do that, we also need to specify an ***outer attribute*** to our struct that talks about debugging. For a prettier output (that also uses the Debug formatter), instead of `{:?}` we can use `{:#?}`. This is shown in the following:
![[Adding a debug attribute to a struct.png]]