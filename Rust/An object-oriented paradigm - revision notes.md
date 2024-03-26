# Composition vs Inheritance
These two OOP concepts serve the same purpose of bringing additional functionality to a class and adding to code reusability. However, they way of achieving the result is not the same and choosing the right one for the situation can be important.
Inheritance is a design approach that tells the story: **is a relationship** between two objects. For example, a `Cat` is an `Animal`.
Composition is a design approach that tells the story: **has a relationship** between two objects. For example, a `Tire` belongs to a `Wheel`.
It's often more preferable using composition as that relationship is more common than finding an ancestry tree for classes. Usually the biggest benefit of composition compared to inheritance comes from higher flexibility - reduced coupling. 