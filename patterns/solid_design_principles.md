# Udemy C++ Design Patterns
# SOLID Design Principles

Q:what are design patterns
A:common architectural approaches used to solve problems
<!-- 1552225320815 -->

Q:what is the Single Responsibility Principle
A:a class should only have a single responsibility
a class should only have a single reason to change
<!-- 1552225320817 -->

Q:Open Close Principle
A:your system should be open to extension through inheritance
but close for modification
Think about how the action you are doing
create a base class that can be extended through inheritance
use templates
avoid modification of code you have already written
prefer making your code extensible

Q:Enterprise pattern (Specification pattern)
pending

Q:Liskov Substitution Principle
A:If you have a function that takes in a base class
You should be able to use that function with its inherited
class without any problem.
basically `process(Square)` should also work for `process(Rectangle)`
who inherits from Square
