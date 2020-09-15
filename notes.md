Resources C++
- [geeksforgeeks](https://www.geeksforgeeks.org/c-plus-plus/)
- [tutorialspoint](https://www.tutorialspoint.com/cplusplus/cpp_overview.htm)
- [defenitive book guide](https://stackoverflow.com/questions/388242/the-definitive-c-book-guide-and-list)
- [stackoverflow faq](https://stackoverflow.com/questions/tagged/c%2B%2B-faq)
- [compiler explorer](https://godbolt.org/)
- [cpp reference](https://en.cppreference.com/w/)
- [iso cpp faq](https://isocpp.org/faq)
- [core guidelines](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)
- [yandex c++ course](https://www.coursera.org/specializations/c-plus-plus-modern-development)
- [google style guide](https://google.github.io/styleguide/cppguide.html)
- [stroustrup](https://www.stroustrup.com/)
- [meyers](https://scottmeyers.blogspot.com/)
- [sutter](https://herbsutter.com/)
- [c++ weekly](https://www.youtube.com/playlist?list=PLs3KjaCtOwSZ2tbuV1hx8Xz-rFZTan2J1)
- [hiring cpp](https://www.hackerearth.com/recruit/resources/e-books/hire-cpp-developer/)
- [interview quest](https://www.softwaretestinghelp.com/cpp-interview-questions/)
- [geeks quest1](https://www.geeksforgeeks.org/commonly-asked-c-interview-questions-set-1/)
- [geeks quest2](https://www.geeksforgeeks.org/commonly-asked-c-interview-questions-set-2/?ref=rp)
- [oop quest1](https://www.geeksforgeeks.org/commonly-asked-oop-interview-questions/?ref=rp)
- [top interview quest](https://encelo.github.io/notes.html)
- [cracking coding interview](https://1lib.eu/ireader/2724521)
- [learncpp](https://www.learncpp.com/)
- [cherno c++](https://www.youtube.com/watch?v=18c3MTX0PK0&list=PLlrATfBNZ98dudnM48yfGUldqGD0S4FFb)


Compile
```bash
$ g++ test.cpp -o test            " Compile
$ g++ test.cpp -Wall -std=c++0x   " Warnings, standard
$ echo $?                         " Output return value

> c1 /EHsc test.cpp    " Windows compile, exception handling
> echo %ERRORLEVEL%    " On Windows
```

List of c++ compilers:
- g++
- clang c++
- llvm
- apple c++
- microsoft visual c++
- intel c++
- ibm c++

Always flash buffer when debugging (endl) to avoid incorrect inferences where program crashed

Don't
```cpp
using namespace std;
```

Possible (not so good)
```cpp
using std::endl;
using std::cin;
```

EOF Windows: Ctrl+Z
EOF Unix: Ctrl+D

Use a style whatever you want, but be consistent
Styles:
- [Google C++](https://google.github.io/styleguide/cppguide.html)
- [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
- [Jason Turner's best practices](https://github.com/lefticus/cppbestpractices)

### Use file redirection
```bash
$ ./test <infile >outfile
```

[Built-in types](https://www.tutorialspoint.com/cplusplus/cpp_data_types.htm)
[Else](https://www.geeksforgeeks.org/c-data-types/)

In order to make *portable* apps you should avoid *implementation-defined behaviour* (e.g assuming int 32bit etc)

Don't mix signed and unsigned types (signed converts to unsigned)

Literals:
- printable ('a', "asd")
- non-printable (escape sequences:'\n', '\t' etc, can be like \xD3 or \115)

Specifying type of a literal:
- L'a'          wchar_t
- u8"hi!"       utf-8 string
- 42ULL         unsigned long long
- 3F            float
- 3.1415        long double
- u'a', U'A'    char16_t, char32_t
- true, false   boolean
- nullptr       null pointer

[Literals](https://www.geeksforgeeks.org/types-of-literals-in-c-c-with-examples/)

Initialization != assignment (replace current value)

Way to initialize
```cpp
int val = 0;
int val = {0};  //list initialization, doesn't allow to truncate
int val{0};     //doesn't allow to truncate
int val(0);
```
[difference](https://stackoverflow.com/questions/5350125/constructor-of-type-int)

By default variable are default initialized:
- undefined (local scopes)
- 0 if global

Separate compilation
```cpp
extern int a;               //declares but not defines
int b;                      //declares and defines
extern double pi = 3.1415;  //definition, overrides extern
```

It is error to use extern inside function
Variables must be defined 1 time but can be declared many

Naming conventions:
- INDEX for constants
- _NAME for reserved macros

Scopes:
- Global
- Block

It is a bad idead to name global and local variables same name

Compound types:
- References (lvalue, another name for existing object)
- Pointers

```cpp
int &a = i, &b = i;     //every should be preceded by &
int *a, int *b;
```
```cpp
int val = 10;
int *ptr = &val;      //& takes address, creates ref
int *ptr = ptr2;      //* dereferences ptrs, creates ptrs
```

Pointer value:
- Object
- Past the end of an object (e.g map.end() iterator)
- nullptr
- Invalid

We may dereference only valid pointer to an object

[How to read C declarations](http://unixwiz.net/techtips/reading-cdecl.html)

nullptr (new standard) ~ NULL (preprocessor macro for 0) ~ ptr to 0

void* pointer
void* can hold the address of any object
We can not use void* to operate on adresses (dont't know size of object)

Pointers' fun
```cpp
int p = 5;
int *pt = &p;
int **ptr = &pt;
```

Reference to pointer
```cpp
int val = 12;
int *p = &val;
int *&refp = p;
```

It can be easier to understand complicated ptr/ref when read right to left

Const refs/ptrs
```cpp
const int a = 5;
const int j = get_size();   //ok
const int k;                //error
```

By default const objects are local to a file
Usually compiler replaces variable with its corresponding value, so it has to see its initializer

When we split a program into multiple files, every file that uses the const must have access to its initializer
To share a const object among multiple files, you must define the variable as extern
[extern stackoverflow](https://stackoverflow.com/questions/10422034/when-to-use-extern-in-c)

Reference to const (abbreviate as const reference)
```cpp
int val = 1024;
const int &r1 = val;
```
```cpp
int i = 1;
const int &r1 = i;      //ok, const to nonconst
const int &r2 = 42;     //ok
const int &r3 = r1*2;   //ok
int &r4 = r*2;

const int i2 = 1231;
int &ref = i2;          //error: ref to nonconst int

double c = 3.1415;
int &ref = c;           //error
const int &ref = c;     //ok, creates temp int, ref binds to 3

int a = 12;
const int &ref = a;     //ok, const ref to nonconst
```

In some sense all refs are const: you can not bind it to another object
Reference to const may refer to a nonconst object
You can not change an object if it is ref to const


Pointers and const
```cpp
const double pi = 3.14;     //pi i const, its value may not be changed
double *ptr = &pi;          //error, ptr is a plain pointer
const double *cptr = &pi;   //ok
*cptr = 42;                 //error
```

refs:
- plain: to plain
- const: to plain, const

ptrs:
- plain: to plain, const
- const: to plain, const

top-level const = const ptr
low-level const = const int


Constexpr and constant expression
Constant expression: value can't be changed, evaluated at compile time
```cpp
const int a = b+1;          //const expression
int afd = 33;               //not a const expression
const int sz = get_size()   //not a const expression
```

Constexpr varibles
Use constexpr to ask compiler to verify if expression is const
```cpp
constexpr int mf = 20;          //20 is a constant expression
constexpr int limit = mf + 1;   //mf + 1 is a constant expression
constexpr int sz = size();      //ok only if size is a constexpr function
```
[constexpr geeks](https://www.geeksforgeeks.org/understanding-constexper-specifier-in-c/)
[constexpr vs template](https://www.modernescpp.com/index.php/c-core-guidelines-programming-at-compile-time-with-constexpr)


constexpr applies to pointer, not to type it points

```cpp
constexpr int* ptr = &val;          //ok
constexpr const int* ptr = &val;    //ok
```


Type aliases
```cpp
typedef vector<vector<double>> rmatrix;                 //typedef
using nmatirx = vector<vector<int>>;                    //alias declaration, c++11
auto start = std::chrono::high_resolution_clock::now(); //auto type specifier for type deduction
auto sz = 0, pi = 3.14;                                 //error
auto i = 0, *p = &i;                                    //ok


//auto usually ignores top-level consts, keeps lov-level consts
const int i =  12, &cr = ci;
auto b = ci;                    //b is int
auto c = cr;                    //c is int
auto d = &i;                    //d is int*
auto e = &ci;                   //e is const int*

const auto f = ci;              //say eplicitly for top-level const int

decltype(f() ) sum = x;         //sum has whatever type f returns, compiler doesn't call f, dosnt't drop top-level const
const int ci = 0;
decltype(ci) x = 0;             //has type const int

// decltype of an expression can be a reference type
int i = 42, *p = &i, &r = i;
decltype(r + 0) b; // ok: addition yields an int ; b is an (uninitialized) int
decltype(*p) c;
// error: c is int& and must be initialized

// decltype of a parenthesized variable is always a reference
decltype((i)) d;
// error: d is int& and must be initialized
decltype(i) e;
// ok: e is an (uninitialized) int
```


Structs and Classes
[member init list vs in-class init](https://stackoverflow.com/questions/27352021/c11-member-initializer-list-vs-in-class-initializer)

We can define a class inside function but it'll have limited functionality


Header files
When we update header, we have to recompile our program

Preprocessor
Preprocessor variables have 2 states(defined/not defined)
Header guards(relies on preprocessor vars):
- #define       defines a var to given name
- #ifdef        is true if var is defined
- #ifndef       is true if var is not defined
- #endif        close block

Preprocessor variable names do not respect C++ scoping rules
Preprocessor vars must be unique, typically we base it on the name of (a class in the header)header, write in UPPERCASE

Headers should have guards, even if they aren't (yet) included by another header
[guards stackover](https://stackoverflow.com/questions/4767068/header-guards-in-c-and-c)


String
Standard specifies not only operations but efficiency requirements

```cpp
string s1;
string s2 = s1;
string s3 = "asddsa";
string s4(10, 'c');

string s5 = "London";   //copy init
string s6("Kyiv");      //direct init
string s7(10, 'a');     //direct init
```
[direct init vs copy](https://stackoverflow.com/questions/1051379/is-there-a-difference-between-copy-initialization-and-direct-initialization)


Some string operations:
```cpp
os << s;
is >> s;
getline(is, s);
s.empty();
s.size();
s = s1 + s2;
s1 < s2;
s1 != s2;
```

size_t type is big enough to hold size ob biggest object

<cheader> vs <header.h>
c++ headers vs c headers

range based for
```cpp
for(auto& i : str){
    i = toupper(i);
}
```

Functions for string
```cpp
isalnum(c);
isupper(c);
//etc
```

Vector type is a class template, not type
Instantiation = compiler creates function/class from template
Type can be vector<int> etc
```cpp
vector<int> a;
vector<int> a(b);
vector<int> a = b;

vector<int> a = {1, 2, 3};
vector<int> a = (1, 2, 3);      //error

vector<int> a(10, -1);          //10 elements = -1
vector<string> b(12, "Hi!");    //12 strings = "Hi!"

vector<int> a(10);              //10 ints = 0
vector<string> b(3);            //3 empty strings

vector<int> a("Hi!");           //error
vector<int> b{"Hi!"};           //ok, 1 string
vector<int> c(10, "Hi!");       //10 strings
vector<int> d{10, "Hi!"};       //10 strings
```

Better use vector.push_back() instead of vector.resize() and assignments
Vectors grow effitiently
Exception = all elements need same value

Best way to iterate, also are possible iterators or subscripts
```cpp
for(auto &i : vec){
    i *= 20;                //change
}

for(const auto &i : vec){
    cout << i << endl;      //read
}
```
If want to use size_t, you have to specify type
```cpp
vector<int>::size_type;        //ok
vector::size_type;             //error
```

Vector supports >, <, !=, == etc operations

Best way to check if empty
```cpp
if(vector.empty()){
    //good
}

if(vector.size()!=0){
    //bad
}
```

Iterators
```cpp
auto it = vec.begin();      //ordinary
auto e = vec.end();         //e.g vector<int>::iterator it

auto cit = vec.cbegin();    //const
auto ce = vec.cend();       //e.g vector<int>::const_iterator
cit


//end iterator points to one past lat element
//we can change const_iterator, but not the content it points to


auto b = *it;               //dereferences
b = iter->mem;              //dereferences iter and fetches memory
                            //equal to (*iter).mem;

auto itmid = vi.begin() + v.size() / 2;

if(it < itmid){
    process_befmid();
}else{
    process_after();
}

//also support !=, ==, ++, --
//there is an iterator arithmetic iter +- n, iter1 - iter2 etc
//string iter support >, >=, <, <=
//most don't support <, >
```

If container is empty then vec.begin() == vec.end()


Arrays
Use vector if you don't know how many elements you need

```cpp
//n has to be constant expression
//can not use auto for arrays
//initialise with undefined
int arr[n];


//char arrays must have enough size to hold '\0'
char a4[2] = "Hi";  //error

//we can use range based for
for(auto &i : a4){
    cout << i << ' ';
}
```

Buffer overflow - program fails to check a subscript and mistakenly uses memory outside the range


You can not directly pass arrays by value
```cpp
int arr1[10];
int *arr2 = arr1;   //not &arr1, because arr1 is a ptr

//Pointer arithmetic
//*(arr1)     == arr1[0]
//*(arr1 + 1) == arr1[1]
//*(arr1 + 2) == arr1[2]
//*(arr1 + 3) == arr1[3]


//Derederence pointers
//*arr1 + 1 == arr1[0] + 1



arr1 == &arr1[0]  //pointer to array points to adress of I element

//BUT

int *ptr = &arr[0]; //arr[i] returns i not ptr


//begin(), end() retutn pointers to fist/last elements
int *b = begin(arr2);


arr[-1] == *(arr-1);    //undefined behaviour
```

Instead of C style string use string
```cpp
strlen(p);          //returns len of p, not counting '\0'
strcmp(p1, p2);     //compares p1 and p2 for equality, returns 0 if p1==p2, >0 if p1>p2, <0 if p1<p2
strcat(p1, p2);     //appends p2 into p1, returns p1
strcpy(p1, p2);     //copies p2 into p1, returns p1


string str = "das";
const char *strc = str.c_str();     //init from <string>
```

Multi dimensional arrays
```cpp
int a[10][20][30];
```



  Operators
  |       |
unary   binary


Operand are generally promoted to a larger type
sign -> unsign



Rvalues and lvalues
Order of evaluation
```cpp
int i = f1() * f2();    //don't know order(f1, f2), it is unspecified
```

There are 4 operators that guarantee order of eval:
- AND (&&) left-hand operand is evaluated first, right-hand is evaluated only if left-hand is true
- OR  (||)
- Conditional (? :)
- Comma (,)



Better don't use true and false in comparison
```cpp
if(a == true){
    //true only if a == 1
}

//use instead

if(a){
    //true if nonzero
}

if(!a){
    //true if zero
}

```


Better use prefix increment (especially for complex types)


Better nest no more than 2 or 3 conditionals


Bitwise:
- NOT (~)
- AND (&)
- OR  (|)
- XOR (^)
- >>  (right shift) (for unsign inserts 0; for sign implementation defined)
- <<  (left shift)  (same; 0 for signed)

It is better to use unsigned types with bitwise (there are no guarantees how sign bit is handled)


Sizeof returns size of variable in bytes (it doens't evaluate its operand)

Always sizeof(char) == 1

Sizeof(arr) is size of entire array
```cpp
int size = sizeof(arr)/sizeof(*arr);    //define number of elements

int x[10];
int *p = x;
cout << sizeof(x)/sizeof(*x) << endl;   //10
cout << sizeof(p)/sizeof(*p) << endl;   //2
```

Sizeof(vector/string) is size of fixed part



Type conversions:
- implicit
- explicit

Implicit:
smaller size -> bigger (e.g int -> long)
integral -> floating point (e.g int -> float)
signed -> unsigned (int -> uint)

int ia[10] -> int *ip = ia;     //only in functions
0, nullptr -> any pointer type
pointer to any nonconst -> void*
pointer to any -> const void*
there are some conversions defined by classes (string)


Cast are dangerous constructs
Explicit:
- static_cast       //can cast arithmetics, void*
- dynamic_cast      //runtime cast, useful for inheritance
- const_cast        //cast away low-level const
- reinterpret_cast  //machine dependent, low-level reinterpretation of bit pattern

Old-style:
- type (expr)       //function-style
- (type) expr       //c-style

Every time you write a cast you should think if you can achieve same result different way


Null statement
for(;;);
    //or
for(;;)
    ;


Switch
```cpp
switch(ch):
    case 'a':
        ++acnt;
        break;
    case 'o':
        ++ocnt;
        break;
    default:
        ++notoacnt;
        break;

//do not forgive break
switch(ch):
    case 'a': case'o':
        ++aocount;
        break;
    default:
        ++notaocount;
        break;
```


Exceptions:
- throw     //raises an excepton
- try       //deal with exception
- catch     //exceptions handlers

Set of exceptions classes are used to pass info what happend beetwen try and catch



Static object exists during program execution
Static vs global: global(with extern) is for external linkage when static is for internal


Pass objects to functions:
- Value
- Pointer
- Reference


We can use command line args in main (char argv*[])
argv[0] contains program name




Functions with varying parameters:
- initializer_list<T>
- elipsis parameters (should be used with built-in types, not classes)



It is normal return a pointer/reference to function arguments, but you should NEVER return pointer/reference to a local object!


vector<T> functions can return an initializer list


Main returns a value that indicates programs's status
To make return values machine independent <cstdlib> contains 2 preprocessor values:
- EXIT_FAILURE
- EXIT_SUCCESS


Trailing return type
```cpp
auto func(int i) -> int(*)[10];
```

decltype
```cpp
int odd[] = {1,3,5,7,9};
int even[] = {0,2,4,6,8};
// returns a pointer to an array of five int elements
decltype(odd) *arrPtr(int i)
{
    return (i % 2) ? &odd : &even; // returns a pointer to the array
}
```


Overloaded functions
Sometimes parameter might look different(aliases) but be same

Parameter with top-level const is indistinguishable from parameter without it

Low-level const allows to overload functions
```cpp
// functions taking const and non const references or pointers have different parameters
// declarations for four independent, overloaded functions
Record lookup(Account&);    // function that takes a reference to Account
Record lookup(const Account&); // new function that takes a const reference
Record lookup(Account*);    // new function, takes a pointer to Account
Record lookup(const Account*); // new function, takes a pointer to const
```

Compiler prefer top-level const functions when overloadinf, specifying same low-level const function will result in error


Function matching (overload resolution): compiler determines which function to call comparing functions' arguments

There can be 3 outcomes:
- Best match
- No match
- Ambiguous call


Default function arguments
```cpp
typedef string::size_type sz;
string screen(sz ht = 24, sz wid = 80, char backgrnd = ' ');


window = screen();   // equivalent to screen(24,80,’ ’)
window = screen(66); // equivalent to screen(66,80,’ ’)
window = screen(66, 256);      // screen(66,256,’ ’)
window = screen(66, 256, ’#’); // screen(66,256,’#’)
```

If a parameter has a default argument, all the parameters that follow it must also have default arguments.

Part of the work of designing a function with default arguments is ordering the parameters so that those least likely to use a default value appear first and those most likely to use a default appear last


Default arguments ordinarily should be specified with the function declaration in an appropriate header.
But we can specify it in our scope with a function declaration (only add defaults to non specified, not changing specified)



Inline and constexpr
On most machines function call is more expensive than appropriate operator usage (registers are saved before call and restored after return, arguments may be copied etc)


Inline functions avoid function call overhead
Function declared so (usually) is expanded "in line" at each call

The inline specification is only a request to the compiler. The compiler may choose to ignore this request


Constexpr
Similar to other function but:
- return type must be a literal
- type of each parameter must be a literal
- function body must contain only 1 return

Compiler replaces such functions with their resulting values
Constexpr functions are implicitly inline


If we give non constant expression args compiler will produce error

Constexpr function will only yield a constant expression if only its arguments are constants expressions



Aids for debugging
Programmers include some code for debugging
Preprocessor faciities:
- assert(expr)  (preprocessor macro <cassert>, no std::, no using directive are needed; many headers include <cassert>, so likely iw would be included)
- NDEBUG        (preprocessor variable, if defined assert does nothing)

#define NDEBUG before assert inclusion or
g++ -DNDEBUG main.cpp
CC -D NDEBUG main.c

If NDEBUG is defined we avoid run-time overhead

We can also write conditional debugging code
```cpp
void print(const int ia[], size_t size){
    #ifndef NDEBUG
    //__func__ is a local static defined by compiler that holds function's name
    cerr << __func__ >> ": array size is " << size << endl;
    #endif
}
// here we print function's name we are debugging
```

In addition to __func__ which compiler defines, preprocessor defines:
- __FILE__ string literal containing file name
- __LINE__ integer literal containing line number
- __TIME__ string literal containing time file was compiled
- __DATE__ string literal containing the date file was compiled


We can use it to report additional error message:
```cpp
if (word.size() < threshold)
cerr << "Error: " << _ _FILE_ _
     << " : in function " << _ _func_ _
     << " at line " << _ _LINE_ _ << endl
     << "Compiled on " << _ _DATE_ _
     << " at " << _ _TIME_ _ << endl
     << " Word read was \"" << word
     << "\": Length too short" << endl;
```


Function matching
```cpp
//#define NDEBUG
void process(const vector<int>&arr){
    for(int i=0; i<1000; ++i){
        #ifndef NDEBUG
        assert(arr.empty());
        cerr << __func__ << '\n'
             << __DATE__ << '\n'
             << __TIME__ << '\n'
             << "at line "
             << __LINE__ << '\n';
        #endif
    }
}
```

Candidate funcs(overloaded) -> viable funcs(args match)


Casts should not be needed to call overloaded function
Otherwise func's parameter sets are designed poorly



Argument type conversion:
1. Exact match:
• Argument == parameter
• Array/function type -> corresponding ptr
• Top-level const is added/discarded
2. Const conversion
3. Promotion
4. Arithmetic/pointer conversion
5. Class-type convertion



Pointers to functions
Pointer to function denotes function rather than object
A function's type is determined by its return type and types of its parameters

To declare a pointer that can point at it, we declare a pointer in place of function's name

```cpp
bool lengthCompare(const string &, const string &);
bool (*pf)(const string &, const string &);

pf = lengthCompare; // pf now points to the function named lengthCompare
pf = &lengthCompare; // equivalent assignment: address-of operator is optional

bool b1 = pf("hello", "goodbye");
// calls lengthCompare
bool b2 = (*pf)("hello", "goodbye"); // equivalent call
bool b3 = lengthCompare("hello", "goodbye"); // equivalent call

string::size_type sumLength(const string&, const string&);
bool cstringCompare(const char*, const char*);

pf = 0;                 //ok, points to no function
pf = sumLength;         //error: return type differs
pf = cstringCompare;    //error: params type differs
pf = lengthCompare;     //ok
```

Parentheses around *pf are necessary
There is no conversion between pointers to one function type and pointers to another function type. However, as usual, we can assign nullpеr or a zero-valued integer constant



When we use overloaded function, the context must make it clear which version is being used
```cpp
void (*pf1)(unsigned int) = ff;     // pf1 points to ff(unsigned)
```


Function pointer parameters
```cpp
// third parameter is a function type and is automatically treated as a pointer to function
void useBigger(const string &s1, const string &s2,
                bool pf(const string &, const string &));

// equivalent declaration: explicitly define the parameter as a pointer to function
void useBigger(const string &s1, const string &s2,
                bool (*pf)(const string &, const string &));
```


When we pass a function as an argument, we can do so directly. It will be automatically converted to a pointer:
```cpp
// automatically converts the function lengthCompare to a pointer to function
useBigger(s1, s2, lengthCompare);
```


As we’ve just seen in the declaration of useBigger, writing function pointer types quickly gets tedious
Type aliases, along with decltype, let us simplify code that uses function pointers:
```cpp
// Func and Func2 have function type
typedef bool Func(const string&, const string&);
typedef decltype(lengthCompare) Func2; // equivalent type

// FuncP and FuncP2 have pointer to function type
typedef bool(*FuncP)(const string&, const string&);
typedef decltype(lengthCompare) *FuncP2; // equivalent type

// equivalent declarations of useBigger using type aliases
void useBigger(const string&, const string&, Func);
void useBigger(const string&, const string&, FuncP2);
```


Returning a pointer to function
As with arrays(can return ptr), we can't return a function type, but can retun ptr to function
The easiest way is to use type aliases:
```cpp
using F = int(int*, int);
// F is a function type, not a pointer
using PF = int(*)(int*, int); // PF is a pointer type
```


We have to explicitly specify return type
Unlike parameter type return type is not auto converted
```cpp
using F = int(int*, int);     // F is a function type, not a pointer
using PF = int(*)(int*, int); // PF is a pointer type


PF f1(int);      //ok: PF is a ptr to function
F f1(int);       //error: F is a function type, can't return a function
F *f1(int);      //ok: explicitly specify that the return type is a pointer to function


int (*f1(int))(int*, int);  //declare f1 directly


auto f1(int) -> int (*)(int*, int);   //simplify using trailing return
```

When use decltype, you should use * sign



```cpp
#include <iostream>
#include <random>
#include <vector>
using namespace std;

int add(int a, int b){
    return a + b;
}

int main()
{
    vector<int(*)(int a, int b)> foo_ar(10, add);
    cout<<"Hello World";
    for(const auto &i : foo_ar){
        cout << i(rand() % 100, rand() % 10) << endl;
    }
    return 0;
}
```

```cpp
#include <iostream>
#include <vector>
#include <random>
using namespace std;

int add(int a, int b){
    cout << "Addition: " << a << '+' << b << '\n';
    return a + b;
}

int sub(int a, int b){
    cout << "Substraction: " << a << '-' << b << '\n';
    return a - b;
}

int mul(int a, int b){
    cout << "Multiplication: " << a << '*' << b << '\n';
    return a * b;
}

int divv(int a, int b){
    cout << "Division: " << a << '/' << b << '\n';
    return a / b;
}

int main()
{
    vector<int(*)(int a, int b)> foo_ar{add, add, sub, sub, mul, mul, divv, divv};
    for(const auto &i : foo_ar){
        cout << i(rand() % 100, rand() % 10 + 1) << endl;
    }
    return 0;
}
```



OOP:
- Abstraction   (Interface/Implementation)
- Encapsulation
- Polymorphism
- Inheritance


Class that use abstraction and encapsulation is an abstract data type

Class can have member functions

Functions defined in the class are implicitly inline (!only suggestion for compiler!)



This
```cpp
total.isbn();       //fetches method and call to it
```

When isbn() refers to members of Sales_data, it is referring implicitly to the members of the object on which function was called (e.g total.bookNo)

Member function access the object through an extra, implicit parameter named this

[is this implicitly taken](https://stackoverflow.com/questions/41667653/does-every-c-member-function-take-this-as-an-input-implicitly)

When we call a function this is initialized with adress of the object on which function was invoked


This is a const pointer to nonconst instance by default(we cannot change adress it holds)



It is illegal to define a parameter/variable/member function this
It is legal to use this->bookNo; but is unnecessary(in most cases)



Const member functions (const after parameter list)
The purpose of that const is to modify the type of this ptr
By def, it is  const class *this
Normally we cannot bind this to a const object
This means we can not call an ordinary member function on a const object

Those functions are "read-only", don't change data


!CONST objects (ref/ptr to const) may only call CONST member functions



Class by itself is a scope
Regardless where member data is init(can be after member function), members can use it



Defining a member function outside the class
```cpp
double Sales_data::avg_price() const {
    if (units_sold)
        return revenue/units_sold;
    else
        return 0;
}
```



Defining a function to return this object
```cpp
const B* get_adress() const{
        return this;            //return adress
}

Sales_data& Sales_data::combine(const Sales_data &rhs)
{
    units_sold += rhs.units_sold; // add the members of rhs into
    revenue += rhs.revenue;
                                  // the members of ‘‘this’’ object
    return *this;                 // return the object on which the function was called
}

// By
// return *this; we return an object on which the function was called
```

```cpp
const B* get_adress() const{
    return this;
}

const B& get_instance() const{
    return *this;
}
```


Defining nonmember class related functions
!!Ordinarily, nonmember functions that are part of the interface of a class should be declared in the same header as the class itself

```cpp
// input transactions contain ISBN, number of copies sold, and sales price
istream &read(istream &is, Sales_data &item)
{
    double price = 0;
    is >> item.bookNo >> item.units_sold >> price;
    item.revenue = price * item.units_sold;
    return is;
}

ostream &print(ostream &os, const Sales_data &item)
{
    os << item.isbn() << " " << item.units_sold << " "
    << item.revenue << " " << item.avg_price();
    return os;
}
```

The IO classes can not be copied, so we pass them by reference
Moreover, read/writ-ing change the stream so reference must be nonconst
Ordinarily, thise functions do minimal formatting



Defining sum function
```cpp
Sales_data add(const Sales_data &lhs, const Sales_data &rhs)
{
    Sales_data sum = lhs; // copy data members from lhs into sum
    sum.combine(rhs);
    // add data members from rhs into sum
    return sum;
}



Constructors
Constructor is a special member function of class, its job is to initialize data members
Constructor have same type class has, have no return type

Constructors can write to const objects during their construction


Default constructor(no args):
Will be implicitly defined by compiler if we do not provide explicit default constructor

Compiler provided constructor is called synthesized default constructor:
- Initialize the member if there is an in-class initialier
- Otherwise default-initialize the member

E.g string will be initialized to empty strings
Int would have "garbage"


Most classes could not rely on default constructor
(could rely only if all members have in-class initializers)
Sometimes compiler can not init members (class without constructor)



What =default means
```cpp
Sales_data() = default; //constructor
```
We are defining this constructor because want to provide other as well


Constructor initializer list
Best way
```cpp
B(): count(), numberIsbn() { }      //0, empty string
B(int n, string isbn): count(n), numberIsbn(isbn) { }
```

Constructor should not override default value, only if different



We can define constructors outside class body
```cpp
Sales_data::Sales_data(std::istream &is)
{
    read(is, *this); // read will read a transaction from is into this object
}
```


[return this vs this*](https://stackoverflow.com/questions/2750316/this-vs-this-in-c)


Copy, assignment and destruction
Compiler provides synthesid versions
Although they might not always work(especially when allocating memory)
But they might work with <string> and <vector>

Objects are copied:
- Initialise a variable
- Pass/return object by value

Assigned:
- Use assignment operator

Destroyed:
- Cease to exist (exit from block of code)
- Vector of object destroyed



Access control and encapsulation
Specifiers:
- public (accessible to all parts of program)
- private (accesible to member functions)


Class vs struct
[c struct vs c++](https://stackoverflow.com/questions/2242696/c-structure-and-c-structure)

C++ struct == public class

If we want to have all member public, we define a struct
Struct can have constructor, be derived etc



Friends
Class can allow another class/funcrion to access its nonpublic member, by making function/class friend



!!It is a good idea to group friends declaration together



Mutable data member is never const, even when it is a member of a const object
So we can change it in any member including const functions


Vector of class objects
```cpp
std::vector<Screen> screens{Screen(24, 80, ’ ’)};   //1 Screen
std::vector<B> bees(100, B());                      //100 B's
```




Class is a user-defined type
Even if 2 classes have same members they are different types

We can declare class by 2 ways:
```cpp
class B b;
B b;

//same for structs
struct B b;
B b;
```

```cpp
//we can declare class
class B;
//and define it somewhere(like functions)
class B{
    //members
};
```


Frendship between classes
We can make a class/function friend
We can specify a function from class to make it a friend
If it is overloaded you must specify what to make a friend

We have to declare inside and define outside the friend function



Compiler process declarations firstly and then goes to defenitions


Compiler looks for a declaration of type in class, if didn't find - goes out of scopes


Redefining global typedefs will result in error
We should place typedef at the beginning of the class


Scope name lookup: function -> class -> global scope

Good practice is not to use same name for members functions' params and class members



Constructors
Initializer list>direct init constructor
Some members MUST be initialized not assigned(e.g const, references), so we HAVE TO use initializer list


Order of member initialization
Members are initialized in the way they are specified in class defenition, not in initializer list



!!It is a good idea to write constructor initializars int the same order members are declared
Moreover, when possible, avoid using members to initialize other members


We can define a constructor with default params
If all default params are provided, it defines a default constructor as well



Delegating constructors
```cpp
Sales_data(): Sales_data("", 0, 0) {}
```


In order to nest class A in class B, A should have a constructor
```cpp
struct A{
    NODEFAULT constructor;
};
struct B{
    A a;        //error, if there is no def cons; would work with int, double etc
};


vector<B>arr (10, B());     //B should have def constructor
```

If B contains A and A doesn't have default constructor, it is error to create a vector of B, but can create instance of B


!In practice it is always good to provide default constructor


Implicit class-type conversion
A constructor that can be called with a single argument defines an implicit conversion from the constructor’s parameter type to the class type

```cpp
// ok: explicit conversion to string , implicit conversion to Sales_data item.combine(string("9-999-99999-9"));

// ok: implicit conversion to string , explicit conversion to Sales_data item.combine(Sales_data("9-999-99999-9"));
```

!!In order to be able to convert type T to our class C we should provide a constructor that takes 1 arg of type T



Supressing implicit conversions
We could prevent that behaviour by declaring constructor explicit
Constructors that take 2+ args are not used in conversions, thus there is no need to declare them explicit

Explicit keyword only used on declaration inside class

We can not use =(can lead to implicit conversions) with explicit constructor, only direct form of initialization



We can use explicit constructors for conversions
```cpp
// ok: the argument is an explicitly constructed Sales_data object
item.combine(Sales_data(null_book));

// ok: static_cast can use an explicit constructor
item.combine(static_cast<Sales_data>(cin));
```



Aggregate class:
- All data members are puvlic
- Does not define any constructors
- Has no in-class initializers
- Has no base classes or virtual functions

We can init it with a braced list {}




Literal classes
Aggregate class is literal
- Data members are literal
- Class must have >=1 constexpr constructor
- If is in-class initializer must be a const exprssion
- Class must use default defenition for ita destructor




Constexpr constructor
Constructor can't be const, but constexpr (body is empty)



Static class members
Static members can be private/public.., const, reference, ptretc

The static data members exists outside any object
Similarly static member functions are not bound; they do not have this ptr
Static member functions may not be declared as const
We may not refer to this in their body

It is true both for explicit/implicit this call
(We can not call class nonstatic members from static function)

```cpp
auto var = B::static_func();

//even though the're not an object of a class, we can call by
object(reference) or a pointer
B obj;
B *ptr = &obj;
var = obj.static_func();
var = ptr->static_func();
```

Member functions can use static directly

Static members can not be initialized in constructors
We can define static outside class
Static variable exists during program lifetime
Static data member may access private members of its class

!!Best way to ensure object is defined exactly once is to put defenition of static to class member functions


We can initialize const staic in a class and must initialize constexpr in a class

!!Even if a const static data member is initialized in the class body, that member ordinarily should be defined outside the class defenition




Static members can be used in ways ordinary members can't
- Nonstatic data member is restricted to being declared as ptr/ref to an object of its class etc




C++ library
The IO classes:
- <iostream> (types used to read and write streams)
- <fstream> (... read and write files)
- <sstream> (... read and write in-memory strings)


To support languages that use wide characters, the library defines a set of types and objects that manipulate wchar_t data
The names of wide-character version begin with a w
wcin, wcout, wcerr -> (correspond to) cin, cout, cerr

Wide-char types are are defined in same header (ifstream->wifstream)



Relationships among the IO types
The library lets us ignore the differences among different kinds of streams by using inheritance
istream -> ifstream, istringstream
We can use those objects similarly to cout and cin




No copy or assign for IO objects
We can not copy or assign objects of IO types
```cpp
ofstream out1, out2;
out1 = out2;                //error
ofstream print(ofstream);   //error
out2 = print(out2);         //error
```

Because of it we can not have a parameter or return type that is one of the stream types
Functions that do IO typically pass/return the stream through references
Reading/writing an IO object changes its state, so the reference must not be const



Condition states
Doing IO errors can occur
Some errors are recoverable, other are not

IO classes define functions and flags that let us access and manipulate the condition state of a stream
Example
```cpp
int ival;
cin >> ival;    //if we enter "Boo" //similarly for eof input
```


Once error has occured, subsequent IO operations on stream will fail
We can read or write to a stream only when it is in a non-error state
The easiest way to check it is to put in a condition
```cpp
while (cin >> word);
```



Interrogating the state of a stream
Using a stream as a condition tells only if stream is valid
It does not tell us what happened
IO library defines type named iostate
IO classes define four constexpr of type iostate that represent particular bit patterns
They can be used with bitwise operators

The badbit indicates a system level failure (unrecoverable read or write error)
It is usually not possible to use it once badbit has been set
The failbit is set after recoverable error, such as a reading a character when numeric data was expected

Reaching end-of-file sets both eofbit and failbit
The goodbit, which is guaranteed to have value 0, indicates no failure on the stream
If any of badbit, failbit or eofbit are set, then a condition that evaluates that stream will fail

The library also defines functions to interrogate the state of these flags
Good() returns true if none of the error bits is set
The bad(), fail() and eof() operations return true when corresponding bit is set

The right way to determine the overall state of stream is to use either good() or fail()
Using stream as condition == caling !(stream.fail())

Eof and bad reveal only when those specific errors occured



Managing the condition state
The rdstate member returns an iostate value that corresponds to the current state of the stream
The setstate tyrns on the given state
Clear member is overloaded:
- no args: turns off all failure bits
- iostate: takes 1 arg and set to it

We can use rdstate
Turns off failbit and badbit, other-unchanged
```cpp
cin.clear(cin.rdstate() & ~cin.failbit & ~cin.badbit);
```



Managing the output buffer
Each output stream manages a buffer, which it uses to hold data the program reads and writes
```cpp
os << "please enter a value: ";
```

The literal may be printed immediately, or the os may store it in a buffer to print it later
It can combine several output in order to provide perfomance boost (writing to a device can be time-consuming)

Conditions that cause buffer to flush:
- Program completes normally. All buffers are flushed
- If buffer becomes full, it will be flushed before next write
- We can flush explicitly using endl
- We can use unitbuf to set its internal state to empty the buffer after each output operation. By default, it is set for cerr
- An output stream may be tied to another stream. In this case, the output stream is flushed whenever the stream to which it is tied is read or written. By default, cin and cerr are both tied to cout



Flushing the output buffer
Manipulators:
- endl (writes + newline and flushes)
- flush (writes and flushes)
- ends (writes + null and flushes)


Unitbuf(to flush every output)
```cpp
cout << unitbuf;

cout << nounitbuf;
```

Buffers are not flushed if the program crashes
So for debugging you should flush it



Tying input and output streams
Interactive systems usually should tie their streams, in order to output prompts appear before read thr input




File input and output
```cpp
fstream fstrm;
fstream fstrm(path);
fstream fstrm(path, mode);

fstrm.open(path);
fstrm.open(path, mode);
fstrm.close();
fstrm.is_open();    //returns bool
```



Using file stream objects
We can pass inhereted type in place of original type
E.g ostream -> ofsream, istream -> ifstream

The open and close members
```cpp
ifstram in(file);   //if open fails failbit will be set
ofstream out;
out.open(ifile + ".copy");

if(out){
    //it is a good idea to use check
    //if out
}
```


Automatic construction and destruction
When an fstream object is destroyed, close is called automatically



File modes:
- in (open for input)
- out (open for output)
- app (seek to the end before every write)
- ate (seek to the end immediately after the open)
- trunc (truncate the file)
- binary (do IO operations in binary mode)

By default, when we open an ofstream the contents of the file are discrarded
The only way to preserve the existing data in a file opened by an ofstream is to specify app or in mode explicitly


We can change files and file modes
```cpp
ofstream out;   // no file mode is set

out.open("scratchpad"); // mode implicitly out and trunc
out.close();

// close out so we can use it for a different file
out.open("precious", ofstream::app);
out.close();
```

Any time open is called, the file mode is set, either explicitly or implicitly



String streams
```cpp
sstream strm;       //strm is an anbound stringstream
sstream strm(s);    //holds copy of s

strm.str()          //returns a copy of the string
strm.str(s);        //copies string into strm
```


Using an istringstream
Using ostringstreams




Sequential containers
