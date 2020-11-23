---
title:	    Cpp KnowledgeCenter
subtitle:   Document Description
author:		Reinaldo Molina
email:      rmolin88 at gmail dot com
revision:	0.0.0
date: \today{}
date-created:       Thu Nov 09 2017 11:24
toc: true
---

\pagebreak

# Threads

- Wed Aug 22 2018 15:18
- Keyword: schedule, scheduler, cpp, thread, parallel, parallelism, worker, pattern, task
- [Good Article](https://www.codeproject.com/Articles/10777/Make-Tasks-in-Thread-Pool-to-Collaborate)

# Reading the book

## 2.2 The Basics
- C++ is compiled language.
	- What this means is that you must compile your program in order for it to run.
	- Source files are compiled into object files.
	- Object files are then `linked` together to form the executable.
- C++ is statically typed language.
	- This means that the type of every variable defined must be known ahead of time.

### 2.2.1 Hello World.
- A string literal is sequence of characters surrounded by double quotes:
	- `"Hello World!\n"`

### 2.2.2 Types, Variables and Arithmetic
- A declaration is a statement that introduces a name into the program.
- Every time you declare a variable some amount of memory is reserved to store that
variable in memory.
- The amount of memory depends on the hardware implementation.
- However, you can obtain its size making use of the `sizeof()`.
- The basic unit block is the `sizeof(char) = 1`. Or 8bits normally.
- Then all the others are based of that. Example `sizeof(int) = 4`. Meaning
`4*sizeof(char)`.
- There is a new **curly-braced-delimeted initializer lists**. 
	- Example: `double d2 {2.3}`
	- When you use it the `=` is optional.
	- Meaning the above is the same as `double d3 = {4.8}`
- A constant cannot be left uninitialized.
	- **Suggestion:** Dont introduce variables until you need them.
	- **Suggestion:** This way you can initialize them properly.
- **Auto:**
	- With `auto` you have to use `=`, no `{}` initializer.
	- Example uses of `auto`:

```cpp
//good : auto increases readability here
for(auto it = std::begin(v); it != std::end(v); ++it)//v could be array as well
{
//..
}

//bad : auto decreases readability here
auto obj = ProcessData(someVariables);

//without auto. Not that good, looks cumbersome
SomeType<OtherType>::SomeOtherType * obj1 = new SomeType<OtherType>::SomeOtherType();
std::shared_ptr<XyzType> obj2 = std::make_shared<XyzType>(args...);
std::unique_ptr<XyzType> obj2 = std::make_unique<XyzType>(args...);

//With auto. good : auto increases readability here
auto obj1 = new SomeType<OtherType>::SomeOtherType();
auto obj2 = std::make_shared<XyzType>(args...);
auto obj3 = std::make_unique<XyzType>(args...);
```

### 2.2.3 Constants
- **Definition:** Immutability: Something that doesnt change. Antonym: Mutability- Is
supposed to change.
- `const`: I promise not to ever change this value. Enforced by compiler.
- `constexpr`: Means - To be evaluated at compile time.
	- Basically means, I can or cannot be a constant. It depends on the evaluation at compile time.
	- Simple example:
```cpp
constexpr double square(double x) { return x*x; }
```
	- `constexpr` functions should be simple.
	- The idea is to reuse a function's definition for both `const` and non `const`
	variables.
	- Before you would have had to define this function twice in order to use it with
	`const` variables.

### 2.2.4 Pointers, Arrays, and Loops
- In a declaration `[]` means **array of**.
	- Example: `char v[6];` is read as: v is array of char of size 6.
	- All arrays starts at 0. Therefore, we have elements from v[0] to v[5].
- Also in a declaration `*` means **pointer to**.
	- Example: `char *p;`
- In an expression, prefix unary `*` means **contents of** and unary `&` means **address of**.
	- Example:

```cpp
char v[6];
char *p = &v[3]; // p points to v's fourth element
char x = *p; // *p is the object that p points to
```

- **For range loops:**
```cpp
int v[] {1,2,3,4,5,6,7,8,9};

// Careful with this implementation. Here you are copying values. Not optimal
for (auto x : v)
	cout << x << '\n';

// Use this way if you just want to refer to the value
for (auto &x : {11,22,33,44,55,66,77})
	cout << x << '\n';

```

## 2.3 User-Defined Types
- The types that are built from the fundamental types.

### 2.3.1 Structures
- The **new** operator allocates memory from an area called `the free store`, also known as `dynamic memory` and/or `heap`.

### 2.3.2 Classes
- A class object can be seen as a pointer to the elements of the class.

### 2.3.3 Enums

```cpp
// They are ints unless you say otherwise.
enum class Color {red, green, yellow};
enum class Traffic_Light {yellow, green, red};

Color c = Color::red;
Traffic_Light t = Traffic_Light::red;
```

- You can also define operators and functions for an `enum class`:

```cpp
Traffic_Light& operator++(Traffic_Light& t)
{
	switch(t)
	{
		case Traffic_Light::green: return t = Traffic_Light::yellow;
		case Traffic_Light::red: return t = Traffic_Light::green;
		case Traffic_Light::yellow: return t = Traffic_Light::red;
	}
}

// Now you can:
Traffic_Light next = ++light; // Assuming light = yellow it will go red
```

## 2.4 Modularity
- A function **declaration**, is just the name: `double sqrt(double)`.
- A function **definition**, is where you specify what it does.

### 2.4.1 Separate Compilation
- This makes emphasis to the issue of separating a class implementation to its own `.cpp` file.
- For example you should have the following: class declarations in `Vector.h`, class
definitions in `Vector.cpp`, usage of the class in `main.cpp` or `X.cpp`, etc.

### 2.4.2 Namespaces
- Its use for expressing that some declarations belong together and their namespaces
shouldn't clash with that of others.
- For example this allows you to have your own `string` implementation, as opposed
to that of `std::string`.
- They are mainly used in libraries.

### 2.4.3 Error Handling
- There is some talk about exceptions here.
- The main take is that exceptions are used to `Handle` an error. If your function
is messed up after the exception. Meaning you can't recover. Then just re-throw
(`throw`) the exception back.

## 3.2 Classes
- A class represents a `concept` in the code of a program.

### 3.2.1 Concrete Types
- A `concrete` type of class is suppose to behave `just like built-in types` but are
of course a bit more complex.
- Examples are `vector`, `string`, etc. They just build on top of `built-in` types.
- They are subdivided into different types.

#### 3.2.1.1 An arithmetic type
- Like `complex`, from complex numbers.
- Where you can do things like add, subtract, etc.
- **Note:** Functions defined in a class are inlined by default.
- Unlined functions are faster because there is no function call overhead.
- **Note:** Defining a `default constructor`, the `<class name>()` you eliminate the
possibility of uninitialized class variables!.
- **Note:** The `const` specifier means that the function is not allowed to change
the object for which they are called. Meaning the value of the variables of that
object.
- **NOTE:** This section is a good example on defining custom `operators`. Like
`+-()*/=`, also good example of `operator==` and `operator!=`.

#### 3.2.1.2 A container type
- Like `vector`.
- A `destructor` is a mechanism to ensure that the memory allocated by the
constructor is deallocated. Of course this is done manually. Meaning you need to do
it!
- **Note:** `new` allocates memory on the free store, also called `heap` or `dynamic store`.
- The counterpart to `new` is `delete`. Is what you suppose to call on the pointer
allocated with `new`.
- **Note:** If you use `new` with an array: `double *elem = new double[100];` you must use `delete[]`: `delete[] elem;`.
- **NOTE:** This technique is very awesome. Meaning the action of allocating
resources in the destructor and deallocating them in destructor.
	- The technique is called Resource Acquisition Is Initialization **(RAII)**.
	- It allows to eliminate _naked new operators_ that you then must remember to
	`delete`.

# C++ QUICK REFERENCE

## Singleton
- Tue Sep 11 2018 09:51

```cpp
class S
{
	public:
		static S& getInstance()
		{
			static S    instance; // Guaranteed to be destroyed.
			// Instantiated on first use.
			return instance;
		}
	private:
		S() {}                    // Constructor? (the {} brackets) are needed here.

		// C++ 03
		// ========
		// Don't forget to declare these two. You want to make sure they
		// are unacceptable otherwise you may accidentally get copies of
		// your singleton appearing.
		S(S const&);              // Don't Implement
		void operator=(S const&); // Don't implement

		// C++ 11
		// =======
		// We can use the better technique of deleting the methods
		// we don't want.
	public:
		S(S const&)               = delete;
		void operator=(S const&)  = delete;

		// Note: Scott Meyers mentions in his Effective Modern
		//       C++ book, that deleted functions should generally
		//       be public as it results in better error messages
		//       due to the compilers behavior to check accessibility
		//       before deleted status
};
```

## USING

```cpp
using size_t = unsigned int;
template<typename Value>
using String_map = Map<string, Value>
String_map<int> m; // m is a Map<string,int>
// You can also do:
using std::string; // use "string" to mean std::string
string sCust;
```

## MACROS

```cpp
__FILE__
__LINE__
__cplusplus
```

## PREPROCESSOR

```cpp
// Comment to end of line
/* Multi-line comment */
#include <stdio.h> // Insert standard header file
#include "myfile.h" // Insert file in current directory
#define X some text // Replace X with some text
#define F(a,b) a+b // Replace F(1,2) with 1+2
#define X \ some text // Line continuation
#undef X // Remove definition
#if defined(X) // Condional compilation (#ifdef X)
#else // Optional (#ifndef X or #if !defined(X))
#endif // Required after #if, #ifdef
```

## BINARY

```cpp
iBits &= ~SomeBit; // Clear a bit
1byte = 8bits = 0x00 = 2 nibbles = 0b0000 0000 = 1/2 word
1hex =  4bits = 1 nibble = 0x0 = 0b0000
```

## LITERALS

```cpp
255, 0377, 0xff // Integers (decimal, octal, hex)
2147483647L, 0x7fffffffl // Long (32-bit) integers
123.0, 1.23e2 // double (real) numbers
'a', '\141', '\x61' // Character (literal, octal, hex)
'\n', '\\', '\'', '\"' // Newline, backslash, single quote, double quote
"string\n" // Array of characters ending with newline and \0
"hello" "world" // Concatenated strings
true, false // bool constants 1 and 0
```

## DECLARATIONS

```cpp
int x; // Declare x to be an integer (value undefined)
int x=255; // Declare and initialize x to 255
short s; long l; // Usually 16 or 32 bit integer (int may be either)
char c='a'; // Usually 8 bit character
unsigned char u=255; signed char s=-1; // char might be either
unsigned long x=0xffffffffL; // short, int, long are signed
float f; double d; // Single or double precision real (never unsigned)
bool b=true; // true or false, may also use int (1 or 0)
int a, b, c; // Multiple declarations
int a[10]; // Array of 10 ints (a[0] through a[9])
int a[]={0,1,2}; // Initialized array (or a[3]={0,1,2}; )
int a[2][3]={{1,2,3},{4,5,6}}; // Array of array of ints
char s[]="hello"; // String (6 elements including '\0')
int* p; // p is a pointer to (address of) int
char* s="hello"; // s points to unnamed array containing "hello"
void* p=NULL; // Address of untyped memory (NULL is 0)
*ptr // value pointed by pointer
&ptr // address of pointer
int& r=x; // r is a reference to (alias of) int x
enum weekend {SAT,SUN}; // weekend is a type with values SAT and SUN
enum weekend day; // day is a variable of type weekend
enum weekend {SAT=0,SUN=1}; // Explicit representation as int
enum {SAT,SUN} day; // Anonymous enum
enum class Color { red, green = 20, blue };
enum struct|class name : type { enumerator = constexpr , enumerator = constexpr , ... }
Color r = Color::blue;
switch(r)
{
	case Color::red  : std::cout << "red\n";   break;
	case Color::green: std::cout << "green\n"; break;
	case Color::blue : std::cout << "blue\n";  break;
}
// int n = r; // error: no scoped enum to int conversion
int n = static_cast<int>(r); // OK, n = 21
typedef String char*; // String s; means char* s;
const int c=3; // Constants must be initialized, cannot assign to
const int* p=a; // Contents of p (elements of a) are constant
int* const p=a; // p (but not contents) are constant
const int* const p=a; // Both p and its contents are constant
const int& cr=x; // cr cannot be assigned to change x
```

## STORAGE CLASSES

```cpp
int x; // Auto (memory exists only while in scope)
// More on static at cpp-static.md
static int x; // Global lifetime even if local scope
extern int x = 10; // Declaration of extern
extern int x; // Information only, declared elsewhere
```

## STATEMENTS

```cpp
x=y; // Every expression is a statement
int x; // Declarations are statements
; // Empty statement
{ // A block is a single statement
	int x; // Scope of x is from declaration to end of
	block
		a; // In C, declarations must precede statements
}
if (x) a; // If x is true (not 0), evaluate a
else if (y) b; // If not x and y (optional, may be repeated)
else c; // If not x and not y (optional)
while (x) a; // Repeat 0 or more times while x is true
for (x; y; z) a; // Equivalent to: x; while(y) {a; z;}
do a; while (x); // Equivalent to: a; while(x) a;
switch (x) { // x must be int
	case X1: a; // If x == X1 (must be a const), jump here
	case X2: b; // Else if x == X2, jump here
	default: c; // Else jump here (optional)
}
break; // Jump out of while, do, or for loop, or switch
continue; // Jump to bottom of while, do, or for loop
return x; // Return x from function to caller
try { a; }
catch (T t) { b; } // If a throws a T, then jump here
catch (...) { c; } // If a throws something else, jump here
```

## FUNCTIONS

```cpp
int f(int x, int); // f is a function taking 2 ints and returning int
void f(const Large& arg){} // Optimized for speed when Large is a big object that cannot be changed
void f(Large& arg){} // Optimized for speed when Large is a big object that can be changed
void f(); // f is a procedure taking no arguments
void f(int a=0); // f() is equivalent to f(0)
f(); // Default return type is int
inline f(); // Optimize for speed
f() { statements; } // Function definition (must be global)
T operator+(T x, T y); // a+b (if type T) calls operator+(a, b)
T operator-(T x); // -a calls function operator-(a)
T operator++(int); // postfix ++ or -- (parameter ignored)
extern "C" {void f();} // f() was compiled in C
//Function parameters and return values may be of any type. A function must either be declared or defined before
//it is used. It may be declared first and defined later. Every program consists of a set of a set of global variable
//declarations and a set of function definitions (possibly in separate files), one of which must be:
// ----------Class with Function Pointers---------------------
class A {
	int var;
	int var2;
	public:
	void setVar(int v);
	int getVar();
	void setVar2(int v);
	int getVar2();
	typedef int (A::*_fVar)();
	_fVar fvar;
	void setFvar(_fVar afvar) { fvar = afvar; }
	void insideCall() { (this->*fvar)(); }
};

void A::setVar(int v)
{
	var = v;
}

int A::getVar()
{
	std::cout << "A::getVar() is called. var = " << var << std::endl;
	return var;
}

void A::setVar2(int v2)
{
	var2 = v2;
}

int A::getVar2()
{
	std::cout << "A::getVar2() is called. var2 = " << var2 << std::endl;
	return var2;
}

int main()
{
	A a;
	a.setVar(3);
	a.setVar2(5);

	//    a.fvar = &A::getVar;
	a.setFvar(&A::getVar);
	(a.*a.fvar)();

	a.setFvar(&A::getVar2);
	(a.*a.fvar)();

	a.setFvar(&A::getVar);
	a.insideCall();

	a.setFvar(&A::getVar2);
	a.insideCall();

	return 0;
}
//----------------------------------------------
int main() { statements... } or
int main(int argc, char* argv[]) { statements... }
// argv[0] is always the name of the program. Therefore argc is always at least 1.
// argv is an array of argc strings from the command line. By convention, main returns status 0 if successful, 1 or
// higher for errors.
// Functions with different parameters may have the same name (overloading). Operators except :: . .* ?: may be
// overloaded. Precedence order is not affected. New operators may not be created.
```

## EXPRESSIONS

```cpp
// Operators are grouped by precedence, highest first. Unary operators and assignment evaluate right to left. All
// others are left to right. Precedence does not affect order of evaluation, which is undefined. There are no run time
// checks for arrays out of bounds, invalid pointers, etc.
T::X // Name X defined in class T
N::X // Name X defined in namespace N
::X // Global name X
t.x // Member x of struct or class t
p->x // Member x of struct or class pointed to by p
a[i] // i'th element of array a
f(x,y) // Call to function f with arguments x and y
T(x,y) // Object of class T initialized with x and y
x++ // Add 1 to x, evaluates to original x (postfix)
x-- // Subtract 1 from x, evaluates to original x
typeid(x) // Type of x
typeid(T) // Equals typeid(x) if x is a T
dynamic_cast<T>(x) // Converts x to a T, checked at run time
static_cast<T>(x) // Converts x to a T, not checked
reinterpret_cast<T>(x) // Interpret bits of x as a T
const_cast<T>(x) // Converts x to same type T but not const
sizeof x // Number of bytes used to represent object x
sizeof(T) // Number of bytes to represent type T
++x // Add 1 to x, evaluates to new value (prefix)
--x // Subtract 1 from x, evaluates to new value
~x // Bitwise complement of x
!x // true if x is 0, else false (1 or 0 in C)
-x // Unary minus
+x // Unary plus (default)
&x // Address of x
*p // Contents of address p (*&x equals x)
new T // Address of newly allocated T object
new T(x, y) // Address of a T initialized with x, y
new T[x] // Address of allocated n-element array of T
delete p // Destroy and free object at address p
delete[] p // Destroy and free array of objects at p
(T) x // Convert x to T (obsolete, use .._cast<T>(x))
x * y // Multiply
x / y // Divide (integers round toward 0)
x % y // Modulo (result has sign of x)
x + y // Add, or &x[y]
x - y // Subtract, or number of elements from *x to *y
x << y // x shifted y bits to left (x * pow(2, y))
x >> y // x shifted y bits to right (x / pow(2, y))
x < y // Less than
x <= y // Less than or equal to
x > y // Greater than
x >= y // Greater than or equal to
x == y // Equals
x != y // Not equals
x & y // Bitwise and (3 & 6 is 2)
x ^ y // Bitwise exclusive or (3 ^ 6 is 5)
x | y // Bitwise or (3 | 6 is 7)
x && y // x and then y (evaluates y only if x (not 0))
x || y // x or else y (evaluates y only if x is false (0))
x = y // Assign y to x, returns new value of x
x += y // x = x + y, also -= *= /= <<= >>= &= |= ^=
x ? y : z // y if x is true (nonzero), else z
throw x // Throw exception, aborts if not caught
x , y // evaluates x and y, returns y (seldom used)
```

## CLASSES

```cpp
// Info about classes ctors here: http://en.cppreference.com/w/cpp/language/default_constructor
// Why initialize class members in order declared:
// The reason for this ordering is because there is only one destructor, and it has to
// pick a "reverse order" to destroy the class member. In this case, the simplest solution
// was to use the order of declaration within the class to make sure that attributes were
// always destroyed in the correct reverse order.  class T
{ // A new type
	private: // Section accessible only to T's member functions
	protected: // Also accessable to classes derived from T
	public: // Accessable to all
		const static int r = 88; // the only way to initialize a value
		int x; // Member data
		void f(); // Member function
		void g() {return;} // Inline member function
		void h() const; // Does not modify any data members
		int operator+(int y); // t+y means t.operator+(y)
		int operator-(); // -t means t.operator-()
		T(): x(1) {} // Constructor with initialization list
		T(const T& t): x(t.x) {} // Copy constructor
		T(const T& t)= delete // No copy operations
		T(T&& t) {x = t.x; t.x = 0;}; // Move constructor
		T& operator=(T&& t): x(t.x) {t.x = 0;}; // Move operator
		T& operator=(const T& t) {x=t.x; return *this; } // Assignment operator
		T& operator=(const T& t)= delete; // No assignment operator. C++11 feature
		~T(); // Destructor (automatic cleanup routine)
		explicit T(int a); // Allow t=T(3) but not t=3
		explicit T(int x_): x(x_) {} // The explicit specifier specifies that a constructor or conversion function (since C++11) 
		// doesn't allow implicit conversions or copy-initialization. It may only appear within 
		// the decl-specifier-seq of the declaration of such a function within its class definition.
		operator int() const {return x;} // Allows int(t)
		friend void i(); // Global function i() has private access
		friend class U; // Members of class U have private access
		static int y; // Data shared by all T objects
		static void l(); // Shared code. May access y but not x
		static int getY(){return y;} // This is how you access static members after their initialization
		class Z {}; // Nested class T::Z. Also know as: "has a Z" relationship
		typedef int V; // T::V means int 
};

// Thu Nov 16 2017 11:59: calling a base class constructor 
class Foo : public BaseClass 
{
	public:
	Foo() : BaseClass("asdf") {}
};
void T::f() 
{ // Code for member function f of class T
	this->x = x;
} // this is address of self (means x=x;)
int T::y = 2; // Initialization of static member (required)
T::l(); // Call to static member
struct T 
{ // Equivalent to: class T { public:
	virtual void f(); // May be overridden at run time by derived class
	virtual void g()=0;  // Must be overridden (pure virtual)
};
class U: public T {}; // Derived class U inherits all members of base T. Also known as: "is a T" relationship
class V: private T {}; // Inherited members of T become private
class W: public T, public U {}; // Multiple inheritance
class X: public virtual T {}; // Classes derived from X have base T directly
// All classes have a default copy constructor, assignment operator, and destructor, which perform the
// corresponding operations on each data member and each base class as shown above. There is also a default noargument
// constructor (required to create arrays) if the class has no constructors. Constructors, assignment, and
// destructors do not inherit.
```

## TEMPLATES

```cpp
template <class T> T f(T t); // Overload f for all types
template <class T> class X { // Class with type parameter T
X(T t); }; // A constructor
template <class T> X<T>::X(T t) {} // Definition of constructor
X<int> x(3); // An object of type "X of int"
template <class T, class U=T, int n=0> // Template with default parameters
```

## NAMESPACES

- C++11 book page 390

```cpp
namespace N {class T {};} // Hide name T
N::T t; // Use name T in namespace N
using namespace N; // Make T visible without N::
```

## C/C++ STANDARD LIBRARY
Only the most commonly used functions are listed. Header files without .h are in namespace std. File names are
actually lower case.

### STDIO.H, CSTDIO (Input/output)

```cpp
FILE* f=fopen("filename", "r"); // Open for reading, NULL (0) if error
// Mode may also be "w" (write) "a" append, "a+" update, "rb" binary
fclose(f); // Close file f
fprintf(f, "x=%d", 3); // Print "x=3" Other conversions:
"%5d %u %-8ld" // int width 5, unsigned int, long left just.
"%o %x %X %lx" // octal, hex, HEX, long hex
"%f %5.1f" // float or double: 123.000000, 123.0
"%e %g" // 1.23e2, use either f or g
"%c %s" // char, char*
"%%" // %
sprintf(s, "x=%d", 3); // Print to array of char s
printf("x=%d", 3); // Print to stdout (screen unless redirected)
fprintf(stderr, ... // Print to standard error (not redirected)
getc(f); // Read one char (as an int) or EOF from f
ungetc(c, f); // Put back one c to f
getchar(); // getc(stdin);
putc(c, f) // fprintf(f, "%c", c);
putchar(c); // putc(c, stdout);
fgets(s, n, f); // Read line into char s[n] from f. NULL if EOF
gets(s) // fgets(s, INT_MAX, f); no bounds check
fread(s, n, 1, f); // Read n bytes from f to s, return number read
fwrite(s, n, 1, f); // Write n bytes of s to f, return number
written
fflush(f); // Force buffered writes to f
fseek(f, n, SEEK_SET); // Position binary file f at n
ftell(f); // Position in f, -1L if error
rewind(f); // fseek(f, 0L, SEEK_SET); clearerr(f);
feof(f); // Is f at end of file?
ferror(f); // Error in f?
perror(s); // Print char* s and error message
clearerr(f); // Clear error code for f
remove("filename"); // Delete file, return 0 if OK
rename("old", "new"); // Rename file, return 0 if OK
f = tmpfile(); // Create temporary file in mode "wb+"
tmpnam(s); // Put a unique file name in char s[L_tmpnam]
```

### STDLIB.H, CSTDLIB (Misc. functions)

```cpp
std::stoi(); std::stol(); std::stof();
atof(s); atol(s); atoi(s);// Convert char* s to float, long, int
strtoul(); strtof(); strtod(); strtold();
stroimax(); // Usefult because disregards whitespaces
rand(), srand(seed); // Random int 0 to RAND_MAX, reset rand()
void* p = malloc(n); // Allocate n bytes. Obsolete: use new
free(p); // Free memory. Obsolete: use delete
exit(n); // Kill program, return status n
system(s); // Execute OS command s (system dependent)
getenv("PATH"); // Environment variable or 0 (system dependent)
abs(n); labs(ln); // Absolute value as int, long
```

### STRING.H, CSTRING (Character array handling functions)

```cpp
// Strings are type char[] with a '\0' in the last element used.
strcpy(dst, src); // Copy string. Not bounds checked
strcat(dst, src); // Concatenate to dst. Not bounds checked
strcmp(s1, s2); // Compare, <0 if s1<s2, 0 if s1==s2, >0 if
s1>s2
strncpy(dst, src, n); // Copy up to n chars, also strncat(), strncmp()
strlen(s); // Length of s not counting \0
strchr(s,c); strrchr(s,c);// Address of first/last char c in s or 0
strstr(s, sub); // Address of first substring in s or 0
// mem... functions are for any pointer types (void*), length n bytes
memmove(dst, src, n); // Copy n bytes from src to dst
memcmp(s1, s2, n); // Compare n bytes as in strcmp
memchr(s, c, n); // Find first byte c in s, return address or 0
memset(s, c, n); // Set n bytes of s to c
```

### CTYPE.H, CCTYPE (Character types)

```cpp
isalnum(c); // Is c a letter or digit?
isalpha(c); isdigit(c); // Is c a letter? Digit?
islower(c); isupper(c); // Is c lower case? Upper case?
tolower(c); toupper(c); // Convert c to lower/upper case
MATH.H, CMATH (Floating point math)
sin(x); cos(x); tan(x); // Trig functions, x (double) is in radians
asin(x); acos(x); atan(x);// Inverses
atan2(y, x); // atan(y/x)
sinh(x); cosh(x); tanh(x);// Hyperbolic
exp(x); log(x); log10(x); // e to the x, log base e, log base 10
pow(x, y); sqrt(x); // x to the y, square root
ceil(x); floor(x); // Round up or down (as a double)
fabs(x); fmod(x, y); // Absolute value, x mod y
```

### TIME.H, CTIME (Clock)

```cpp
clock()/CLOCKS_PER_SEC; // Time in seconds since program started
time_t t=time(0); // Absolute time in seconds or -1 if unknown
tm* p=gmtime(&t); // 0 if UCT unavailable, else p->tm_X where X is:
sec, min, hour, mday, mon (0-11), year (-1900), wday, yday, isdst
asctime(p); // "Day Mon dd hh:mm:ss yyyy\n"
asctime(localtime(&t)); // Same format, local time
```

### ASSERT.H, CASSERT (Debugging aid)

```cpp
assert(e); // If e is false, print message and abort
#define NDEBUG // (before #include <assert.h>), turn off assert
```
### NEW.H, NEW (Out of memory handler)

```cpp
set_new_handler(handler); // Change behavior when out of memory
void handler(void) {throw bad_alloc();} // Default
IOSTREAM.H, IOSTREAM (Replaces stdio.h)
cin >> x >> y; // Read words x and y (any type) from stdin
cout << "x=" << 3 << endl; // Write line to stdout
cerr << x << y << flush; // Write to stderr and flush
c = cin.get(); // c = getchar();
cin.get(c); // Read char
cin.getline(s, n, ','); // Read line into char s[n] to '\n' (default)
// When getline finds the delimiter character it is extracted from input, but is not appended to str.
if (cin) // Good state (not EOF)?
// To read/write any type T:
istream& operator>>(istream& i, T& x) {i >> ...; x=...; return i;}
ostream& operator<<(ostream& o, const T& x) {return o << ...;}
```

### FSTREAM.H, FSTREAM (File I/O works like cin, cout as above)

```cpp
ifstream f1("filename"); // Open text file for reading
if (f1) // Test if open and input available
f1 >> x; // Read object from file
f1.get(s); // Read char or line
f1.getline(s, n); // Read line into string s[n]
ofstream f2("filename"); // Open file for writing
if (f2) f2 << x; // Write to file
```

####Copy a file in a sane way:

```cpp
int main()
{
std::ifstream  src("from.ogv", std::ios::binary);
std::ofstream  dst("to.ogv",   std::ios::binary);

dst << src.rdbuf();
}
```

### IOMANIP.H, IOMANIP (Output formatting)

```cpp
cout << setw(6) << setprecision(2) << setfill('0') << 3.1; // print "003.10"
// Input/Output manipulators
#include <iostream>
#include <sstream>
int main()
{
std::cout << "The number 42 in octal:   " << std::oct << 42 << '\n'
<< "The number 42 in decimal: " << std::dec << 42 << '\n'
<< "The number 42 in hex:     " << std::hex << 42 << '\n';
int n;
std::istringstream("2A") >> std::hex >> n; // Using a stream a as a temporary.Expensive operation
std::cout << std::dec << "Parsing \"2A\" as hex gives " << n << '\n';
// To clear a stream:
std::stringstream ss;
ss << "Some testing string\n";
// Once done:
ss.str(std::string());
ss.clear();
}
```

### STRING (Variable sized character array)

```cpp
string s1, s2="hello"; // Create strings
s1.size(), s2.size(); // Number of characters: 0, 5
// Note: For performance purposes is good to resize string as soon as they are created.
// Anticipating the size of the chars they are going to hold:
std::string str; str.reserve(1024);
// Resize is the desired function to use over reserve
// Reasons: 
// - reserve can shrink the capacity of an array
// - constructs and destructs elements to fit the new capacity
// - extremely slow
// The preferred way is resize.
// Look in the C++11 book page 384. 
// There are potential implementations of resize and reserve
// String compare example
s1.compare(0,3,"som");
// return 0 when comparison is true
// compare(from index, for x many characters, agains y);
// Carefull here. You should always make sure that index, count do not exceed size of str
// However, 
s1.compare("xxx"); // Will never throw
s1.capacity(); // returns the number of characters that can be held in currently allocated storage 
// Capacity can be increased using reserve. Only works if you are reserving more than current capacity
s1.size(); // returns the number of characters currently stored
// For this you can use resize. **Carefull** with resize
// It constructs new elements to fill the new size specified or destructs elements to shrink to that size
// In order to free memory what should be used is shrink_to_fit
s1 += s2 + ' ' + "world"; // Concatenation
s1 == "hello world" // Comparison, also <, >, !=, etc.
s1[0]; // 'h'
s1.substr(m, n); // Substring of size n starting at s1[m]
s1.c_str(); // Convert to const char*
getline(cin, s); // Read line ending in '\n'
// String pointers:
std::string str("Blah");
std::string *pStr = &str;
(*pStr)[0] = '8'; // Now str = "8lah"
```

### STD::ARRAY vs STD::VECTOR

std::array is just a class version of the classic C array. That means its size is fixed at compile time and it will be
allocated as a single chunk (e.g. taking space on the stack). The advantage it has is slightly better performance
because there is no indirection between the object and the arrayed data.

std::vector is a small class containing pointers into the heap. (So when you allocate a std::vector, it always calls
new.) They are slightly slower to access because those pointers have to be chased to get to the arrayed data... But in
exchange for that, they can be resized and they only take a trivial amount of stack space no matter how large they
are.

[edit]

As for when to use one over the other, honestly std::vector is almost always what you want. Creating large objects on
the stack is generally frowned upon, and the extra level of indirection is usually irrelevant. (For example, if you
iterate through all of the elements, the extra memory access only happens once at the start of the loop.)

The vector's elements are guaranteed to be contiguous, so you can pass &vec[0] to any function expecting a pointer
to an array; e.g., C library routines. (As an aside, std::vector<char> buf(8192); is a great way to allocate a local
buffer for calls to read/write or similar without directly invoking new.)

**NOTE:**
That said, the lack of that extra level of indirection, plus the compile-time constant size, can make std::array
significantly faster for a very small array that gets created/destroyed/accessed a lot.

**TL;DR:**
So my advice would be: Use std::vector unless (a) your profiler tells you that you have a problem and (b) the
array is tiny.

### VECTOR (Variable sized array/stack with built in memory allocation)

```cpp
// Tips:
// #1 Avoid unnecessary reallocate and copy cycles by reserving the size of vector ahead of time.
// #2 Use shrink_to_fit() to release memory consumed by the vector – clear() or erase() does not release memory.
// #3 When filling up or copying into a vector, prefer assignment over insert() or push_back().
// #4 While iterating through elements in a std::vector, avoid the std::vector::at() function.
// #5 Try to avoid inserting an element in front of the vector.
// #6 Prefer emplace_back() instead of push_back() while inserting into a vector.
// #7 Beware of push_back() it makes a copy of of your template class:
//  - Example: std::vector<ComplexClass> foo_complex; ComplexClass cc; foo_complex.push_back(cc);
//  - The above could be an expensive or very wrong copy constructor provided by compiler

vector<int> a(10); // a[0]..a[9] are int (default value is 0)
// Size of a = 10. Really bad. Called ctor of int 10 times. Imagine for a custom object
// This before is not the preferred since all 10 elements are initialized
// However with this method it is defined to do:
a[5] = 88;
// Preferred way:
vector<std::string> a; a.reserve(10);
for (int k=0; k<10; k++)
a.push_back(0); // Set all elements of a to 0
// With this method doing a[k] is not defined
// Since no element has being constructed
// Also if you can is better to use emplace_back instead of push_back
// Capacity refers to how many elements are allocated at the vector to be filled.
// Size refers to how many actually are there.
a.size(); // Number of elements (10)
a.push_back(3); // Increase size to 11, a[10]=3
a.back()=4; // a[10]=4;
a.pop_back(); // Decrease size by 1
a.front(); // a[0];
a[20]=1; // Crash: not bounds checked. Faster
a.at(20)=1; // Like a[20] but throws out_of_range(). Slower
for (vector<int>::iterator p=a.begin(); p!=a.end(); ++p)
*p=0; // Set all elements of a to 0
vector<int> b(a.begin(), a.end()); // b is copy of a
vector<T> c(n, x); // c[0]..c[n-1] init to x
T d[10]; vector<T> e(d, d+10); // e is initialized from d
```

### DEQUE (array/stack/queue)

```cpp
deque<T> is like vector<T>, but also supports:
a.push_front(x); // Puts x at a[0], shifts elements toward back
a.pop_front(); // Removes a[0], shifts toward front
```
### UTILITY (Pair)
```cpp
pair<string, int> a("hello", 3); // A 2-element struct
a.first; // "hello"
a.second; // 3
```

### MAP (associative array)

- **Note:** map sorts out its elements. Meaning the order in which you put them. Its not
the order they are stored in.
- The previously mentioned behavior is not possible with map. You can have
`std::unordered_map`, however the order of things stored in memory is again not
guaranteed. It's just random.

```cpp
map<string, int> a; // Map from string to int
a["hello"]=3; // Add or replace element a["hello"]
typedef std::map<std::string, int>::iterator MapIt; // MapIterator
for (map<string, int>::iterator p=a.begin(); p!=a.end(); ++p)
cout << (*p).first << (*p).second; // Prints hello, 3
a.size(); // 1
typedef std::map<STDELEMENT *, int> MsgElementIntMap;
typedef std::map<STDELEMENT *, int>::iterator MsgElementIntMapIt;

//--------------------------
struct Point { double x, y; };
struct PointCmp {
	bool operator()(const Point& lhs, const Point& rhs) const { 
		return lhs.x < rhs.x; // NB. intentionally ignores y
	}
};
 
// Custom Key class option 1:
// Use a comparison struct
std::map<Point, double, PointCmp> mag = {
	{ {5, -12}, 13 },
	{ {3, 4},   5 },
	{ {-8, -15}, 17 }
};

for(auto p : mag)
	std::cout << "The magnitude of (" << p.first.x
		<< ", " << p.first.y << ") is "
		<< p.second << '\n';
//--------------------------

std::map<int,char> example = {{1,'a'},{2,'b'}};

auto search = example.find(2);
if(search != example.end()) {
	std::cout << "Found " << search->first << " " << search->second << '\n';
}
else {
	std::cout << "Not found\n";
}
//--------------------------
```

### ALGORITHM (A collection of 60 algorithms on sequences with iterators)

```cpp
min(x, y); max(x, y); // Smaller/larger of x, y (any type defining <)
swap(x, y); // Exchange values of variables x and y
sort(a, a+n); // Sort array a[0]..a[n-1] by <
sort(a.begin(), a.end()); // Sort vector or deque
```

### ENDIANNESS

- This is very tricky.
- **Note:** Endiannes swaps bytes inside of each word.
- **Definition**:
- Big-endian and little-endian are terms that describe the order in which a sequence of bytes are
stored in computer memory. Big-endian is an order in which the "big end" (most significant value
in the sequence) is stored first (at the lowest storage address). Little-endian is an order in
which the "little end" (least significant value in the sequence) is stored first. For example, in
a big-endian computer, the two bytes required for the hexadecimal number 4F52 would be stored as
4F52 in storage (if 4F is stored at storage address 1000, for example, 52 will be at address
1001). In a little-endian system, it would be stored as 524F (52 at address 1000, 4F at 1001).

```cpp
// In order to see actual data without little endian
// See ((char *)&value)[0], ((char *)&value)[1], ...
// Better: (int)((unsigned char *)&value)[0] 
// Example:
unsigned long data = 0x3448 18f8;
// If you do this:
char *pch = &data;
printf("0x%c%c%c%c", *pch++,*pch++,*pch++,*pch)
// You'll get:
// 0x4834F818
// However, if you just do this:
printf("0x%X", data);
// You'll get:
// 0x3448 18f8;
// Bottom line is when you read int, long, all but char * data is swapped for you.
```

- This becomes tricky when you read and write to a **BINARY** file. Pretty much if you do it in the same
manner is suppose to be fine. And here is example:
```cpp
// Writing to a file
for (k = 0; (k<k1) && (ofsFile.good()); k++)  // Write binary data
	ofsFile.write((char*) (&CurrData.ulData[k]), UL_SZ);

// Reading from a file
if (ifsCalReadFile.read((char*) (&ulbuff), UL_SZ))
	pData[k] = ulbuff;
```
- The reason why the read above works is because you are writing to the address of `ulbuff` not to the
value of `ulbuff` so then when you read it automatically gets swapped.

- **NOTE:** not all architectures are little endian. Some are big endian

### Byte Swapping

```cpp
// Swapping words
ulbuff1 = ((ulbuff >> 16) & 0x0000FFFF) | ((ulbuff << 16) & 0xFFFF0000);

// Swapping bytes 2<->1 and 4<->3
ulbuff1 = ((ulbuff & 0xff) << 8) | ((ulbuff & 0xff00) >> 8) | ((ulbuff & 0xff0000) << 8) | ((ulbuff & 0xff000000) >> 8);
```

### Casting to float

- You always needs to do this

```cpp
f = *(float *) &ulbuff;
```

### For loop Code

```cpp
for ( declaration-or-expression(optional) aka init_statement ; 
declaration-or-expression(optional) aka condition; 
expression(optional) iteration_expression)
{
statement;
}

// Is the same as:

{
init_statement
while ( condition ) 
{
statement
iteration_expression ;
} 
} 

// Check if for loop finished:
if (k == condition - 1) // Use this when k < condition
if (k == condition) // Use this when k <= condition
```

### RValue Reference (&&)

- [Excellent 
Reference](https://stackoverflow.com/questions/5481539/what-does-t-double-ampersand-mean-in-c11#5481588)
