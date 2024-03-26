# Dangling pointer problem
 In traditional languages, a Dangling pointer problem occurs when you do not invalidate a pointer to a memory after you've freed that memory.
 In C++ this can be illustrated with the following:
 ![[Pasted image 20240324214316.png]]
 Calling `ptr` would result in undefined behaviour but would be triggered only during the runtime. 
 However, the same can be seen in Rust as well but this would cause a compile time termination which is much better:
 ![[Pasted image 20240324214528.png]]
# Meaning of null value
Null value represents the absence of value. At every step of the program, a variable could be in two different states: null of not-null. This knowledge that data is missing is very valuable and used all the time. However, the problem with null values lies in the fact that in most programming languages, you could be dealing with a variable in state of null but not knowing in. This is the essence of the null problem: assuming that something is not null when in fact it ise. 

