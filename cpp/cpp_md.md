
## constexpr

The expression may or may not be `const`.
Example, let's say we have a function:

```cpp
constexpr double square(double x)
```

Now you can call this function with and without `const` variables.
Basically means that the value of a function of object can be evaluated at compile time.

## copy constructor

Gets called whenever we are constructing a new object from an existing one: `Bus local(existing_bus);`
Which is the same as: `Bus local = existing_bus;`
See [Copy constructors](https://en.cppreference.com/w/cpp/language/copy_constructor)
Definition:
```cpp
// class_name ( const class_name & )
struct A
{
    int n;
    A(int n = 1) : n(n) { }
    A(const A& a) : n(a.n) { } // user-defined copy ctor
};
```

## copy assignment operator

Gets called when we are updating an existing object by assigning it an existing one:

```cpp
Bus local, another;
local = another; // copy assignment operator called
```

It has two main forms: `class_name & class_name :: operator= ( class_name )`, this is the typical declaration of a copy assignment operator when **copy-and-swap idiom** can be used. This idiom can be used when there is no need for **deep copy**. Meaning when no heap allocations are needed to be managed. Meaning when there are no pointers. Which you can see below in `Struct A`.
**Note:** That even though `Struct B` added `string s2` inherited copy constructor takes care of the swapping

The second form: `class_name & class_name :: operator= ( const class_name & )`, you can see in `Struct C`

See [Copy constructors](https://en.cppreference.com/w/cpp/language/copy_assignment) and [Assignment Operator](https://en.cppreference.com/w/cpp/language/operators#Assignment_operator)
Definition:
```cpp
struct A
{
    int n;
    std::string s1;
    // user-defined copy assignment, copy-and-swap form
    A& operator=(A other)
    {
        std::cout << "copy assignment of A\n";
        std::swap(n, other.n);
        std::swap(s1, other.s1);
        return *this;
    }
};

struct B : A
{
    std::string s2;
    // implicitly-defined copy assignment, calls copy assignment of A
};

struct C
{
    std::unique_ptr<int[]> data;
    std::size_t size;
    // non-copy-and-swap assignment
    C& operator=(const C& other)
    {
        // check for self-assignment
        if(&other == this)
            return *this;
        // reuse storage when possible
        if(size != other.size)
        {
            data.reset(new int[other.size]);
            size = other.size;
        }
        std::copy(&other.data[0], &other.data[0] + size, &data[0]);
        return *this;
    }
    // note: copy-and-swap would always cause a reallocation
};
```


## copy elision

Compiler optimization that prevents unnecessary copy.
See [Copy elision](https://en.cppreference.com/w/cpp/language/copy_elision)

## aggregate initialization

Preferred way to initialize values: `double d {2.3}`
Because the compiler will through an error when there is lots of information.
Example when converting from double to int. Or from int to char.

See [aggregate initialization](https://en.cppreference.com/w/cpp/language/aggregate_initialization)

## declaring pointer to a pointer

`char *p`, reads as pointer to.
In an expression: `*p = 'R'` or `char P = *p`, is read as contents of pointer.
`&` in an expression: `char *pp = &p` is read as address of

`**` notation means:
we have a pointer to a pointer.

Rarely used in C++ language

In the C language is normally used when you want to `realloc` a pointer, and you need a double pointer because the value of the intermediate pointer is going to change. Meaning, `&var` is going to be different. Example:

```cpp
int *ptr = var;

void func(int **var) { var = (int *) realloc(sizeof(int)); }
```

![Example](Screenshot_20191029-105329.jpg)

