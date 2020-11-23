## static keyword:
- A variable declared static within the body of a function maintains its value between invocations of the function.
- A variable declared static within a module (but outside the body of a function) is accessible by all functions
	within that module. However, it is not accessible by functions from other modules.
- static members exist as members of the class rather than as an instance in each object of the class. There is only a
	single instance of each static data member for the entire class.
- Non-static member functions can access all data members of the class: static and non-static. 
- Static member functions can only operate on the static data members.
- C functions declared static within a module may only be called by other functions within that module (file scope).
