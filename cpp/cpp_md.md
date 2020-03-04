
## constexpr

The expression may or may not be `const`.
Example, let's say we have a function:

```cpp
constexpr double square(double x)
```

Now you can call this function with and without `const` variables.
Basically means that the value of a function of object can be evaluated at compile time.

## copy constructor

Gets called whenever we are constructing a new object from an existing one:
Bus local(existing_bus);

which is the same as:
Bus local = existing_bus;
