# Udemy C++ Design Patterns

# SOLID Design Principles

Q:what are design patterns
A:common architectural approaches used to solve problems

Q:what is the Single Responsibility Principle
A:a class should only have a single responsibility
a class should only have a single reason to change
separation of concerns
different classes handling different/independent problems/tasks

Q:Open Close Principle
A:your system should be open to extension through inheritance
but close for modification
Think about how the action you are doing
create a base class that can be extended through inheritance
use templates
avoid modification of code you have already written
prefer making your code extensible

Q:Enterprise pattern (Specification pattern)
A:pending

Q:Liskov Substitution Principle
A:If you have a function that takes in a base class
You should be able to use that function with its inherited
class without any problem.
basically `process(Square)` should also work for `process(Rectangle)` who inherits from Square
you should always be to substitute a derived class for a base class and viceversa

Q:Interface Segregation Principle
A:Its always better to split functionality
Example: Interface IMachine that can Print, Fax, Scan
Well this is a mistake, its better to have an IPrinter, IFaxer, IScanner interfaces
The lesson is to always segregate, split, modularize
Dont overload interfaces

Q:Dependency Inversion Principle (1 of 2)
A:High Level Modules should not depend on low level modules
Both should depend on abstractions
Abstractions should not depend on details
Details should depend on abstractions

Q:Dependency Inversion Principle (2 of 2)
A:Like for example have a class that depends on a low level struct
High level uses abstraction.
Low level inherits and implement abstraction
