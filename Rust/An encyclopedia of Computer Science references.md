# Dangling pointer problem
 In traditional languages, a Dangling pointer problem occurs when you do not invalidate a pointer to a memory after you've freed that memory.
 In C++ this can be illustrated with the following:
 ![[Pasted image 20240324214316.png]]
 Calling `ptr` would result in undefined behaviour but would be triggered only during the runtime. 
 However, the same can be seen in Rust as well but this would cause a compile time termination which is much better:
 ![[Pasted image 20240324214528.png]]