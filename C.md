## HEADER file ifndef (IF Not DEFined)

https://stackoverflow.com/questions/3246803/why-use-ifndef-class-h-and-define-class-h-in-h-file-but-not-in-cpp

During compilation of your project, each .cpp file (usually) is compiled. In simple terms, this means the compiler will take your .cpp file, open any files #included by it, concatenate them all into one massive text file, and then perform syntax analysis and finally it will convert it to some intermediate code, optimize/perform other tasks, and finally generate the assembly output for the target architecture. Because of this, if a file is #included multiple times under one .cpp file, the compiler will append its file contents twice, so if there are definitions within that file, you will get a compiler error telling you that you redefined a variable. 

## Name convention 

https://cplusplus.com/forum/beginner/89834/ 

- typedef are followed by `_t` 

```
size_t, time_t
```

## Callback Function

If you have a function, y, as an argument to use in a function x, the function y is called "callback function".

```
void handleCache(int nsegments){
    ...
    ...
}

void print_function(char *arg){
    fprintf(stdout, arg);
}

int calculate(int sum){
    ...
    ...
    char str = "SUCCESS";
    print_function(str);                //This is not a callback function per se
    
    setupopt(gfs, port, handleCache);   //handleCache is a callback function
 
    return 0;
 }
 ```

## call methods in other class, by `this` 

https://stackoverflow.com/questions/983310/calling-a-method-from-another-method-in-the-same-class-in-c 

Sometimes you have methods in other class that you want to use in a new class. eg

```
void A::a(){
   do stuff;
}

void B::b(){
   a();
   do stuff;
}
```
In this case, you expect the method `a()` in the function `B` will call the method from the function `A`. It is not. It's like you're creating a new method `a()` inside the function `void B`. So to call the other function as a method in the function `B`, you'd use `this->` 

```
void B::b(){
   this->a();
   do stuff;
}
```


 
 ## `.` dot and `->` arrow operator 
 
 https://www.tutorialspoint.com/What-is-the-difference-between-the-dot-operator-and-in-Cplusplus  
 https://cpp.sh 
 
 `.` dot operator = use when the object is a direct object  
 `->` arrow operator = use when the object is derived from the pointer reference  
 
 ## iterator
 
 https://stackoverflow.com/questions/9963401/why-are-standard-iterator-ranges-begin-end-instead-of-begin-end
 
 When iterating the vector, it's used as !=xxx.end(), it's because of the pointer references. 
 
 ```
 for (std::vector<int>::iterator it = data.begin(); it != data.end(); ++it) { }
 ```
 
 ```
   +---+---+---+---+
   | A | B | C | D |
   +---+---+---+---+
   ^               ^
   |               |
 begin            end
 ```
 
 When the iterator begins, it begins at the left side of the object A. Object A can be any size, could be 1KB, 5KB, so it occupies the space. The iterator, usually `i` is pointing to the starting index of the first object A. So it's on the left side. It will keep going until the end, which is the right side of the object D. If there's an object E, the end position would be the left side of the object E. 
 
 When the iterator reaches the end, it tries to read the right side of its position, which is beyond the vector `[A,B,C,D]`. Therefore, in for loop, it usually indicates that the iterator shouldn't end at the actual end point. 
 
## address variable, address of, content of address 
## int *ptr, &ref, *ptr

https://stackoverflow.com/questions/36962658/what-exactly-is-the-purpose-of-the-asterisk-in-pointers  
https://dev.to/sandordargo/how-to-use-ampersands-in-c-3kga  
https://www.w3schools.com/cpp/cpp_pointers_modify.asp  

```
int x = 5;
int *pointer = &x;
cout<<pointer        # hexadecimal value 
cout<<*pointer       # content of the address 
```

Mnemonic, whenever you see the type `int`, `string`, etc followed by the asterisk `*`, that means the variable is the memory address. 

So the variable `pointer` is the memory address. What is its value? Its value is the address of the variable `x`. So address is an ampersand `&`. So the variable `pointer` has the memory address value of the another variable `x`. 

So when printing the variable `pointer`, it's printing the memory address in hexademical value. 
But if we add `*` in front of the variable `pointer`, it's now printing the content of the memory address. It might be confusing what the asterisk `*` represents whether it represents the address variable or the content of address. Whenever you see the type `int`, `string` in front of the `*`, it means the variable is the memory address. All other are using the content of that memory address. 

### Address of &ref 

for address of `&ref`, although if you print the `&ref`, it will print out the memory address, but when you want the actual content value, you just use the ref and no need to use the asterisk. 

```
#include <iostream>
#include <string>
using namespace std;

int main() {
  string food = "Pizza";
  string &meal = food;
  string *ptr = &meal;

  cout << food << "\n";         # Pizza
  cout << meal << "\n";         # Pizza
  cout << &meal << "\n";        # 0x7ffe31618600
  cout << ptr << "\n";          # 0x7ffe31618600
  cout << *ptr << "\n";         # Pizza
  cout << &ptr << "\n";         # 0x7ffe316185f8
  return 0;
}
```

### Note 

```
using namespace std;
int main()
{
    vector<int> ar = { 1, 2, 3, 4, 5 };
      
    // Declaring iterator to a vector
    vector<int>::iterator ptr;
      
    // Displaying vector elements using begin() and end()
    cout << "The vector elements are : ";
    for (ptr = ar.begin(); ptr < ar.end(); ptr++)
        cout << *ptr << " ";
      
    return 0;  
```

The other pointer that also points to the memmory address is `vector<int>::iterator ptr`

In this case, the variable `ptr` points to the memory address of an array. When we want to call the value from that memory address, we use `*ptr`.

-----------
https://programsquared.com/cpp/difference-between-ampersand-and-asterisk-operator-c++/

```
include <iostream>

void modifyObject(int& obj){
    obj = 3; //Modifies the object directly
}

int main(){
    int obj = 41;
    modifyObject(obj);
    std::cout << obj << std::endl; //Returns 3

    return 0;
}
```
In this example, the `&` is close to the type `int` and we're directly modifying the variable `obj` content. 

## struct Vs class

as far as I understand, `struct` is an object which can have its attributes, which are usually static. `class` is an object that can have statics as well as function inside the class. Imagine a cassette player, the cassette is a `struct` which doesn't have any functions. It has its attributes such as 1. rectangular in size, 2. two holes, 3. magnetic tape, etc. 

A cassette player `class` has its attributes such as square, rectangular in size, but it also has the function that can play another object, eg a cassette. 

```
struct Cassette {
  int width, height;
} cassette;

class Player {
  int width, height;
  int area {return width * height};
} player;
```

## scope operator :: 

https://cplusplus.com/doc/tutorial/classes/ 

If the class has a function, we can use `::` scope operator to set the value. 

```
void Player player::area(int x, int y) {
    width = x;
    height = y;
}
```

## class inheritance 

https://stackoverflow.com/questions/19898920/use-of-colon-after-class-name-in-c

```
class ApplicationUI : public QObject
```

```
It means that ApplicationUI inherits all methods and member variables from the class QObject. The use of public means that the public methods and members of QObject are also public in ApplicationUI.
```

## Check the core.xxxx 

```
gdb -c core.21359 /home/y/bin/ydisc

GNU gdb (GDB) Red Hat Enterprise Linux 7.6.1-120.el7
Copyright (C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-redhat-linux-gnu".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from /home/y/bin64/ydisc...done.
[New LWP 21383]
[New LWP 21387]
```

## string::npos 

https://cplusplus.com/reference/string/string/find/ 
https://stackoverflow.com/questions/3827926/what-does-stringnpos-mean-in-this-code

It's the `not found position` for mnemonic, usually used in finding the index position of the string. 

```
std::string s1 = 'apple';
std::string s2 = 'app';

string::size_type found = s1.find(s2);
if (found != string:npos){
    cout << "s2 string found in s1 at the start position of" << found << endl;
}

## probable result since I didn't compile the code
s2 string found in s1 at the start position of 0.
```

In this code snippet, the s2 value `app` is searched in s1. If it's found, the result `found` will have an index value. If it's not, it'd be `-1` or some maximum number possible. Since the s2 `app` was found in s1 `apple`, and its index is `0`, the variable `found` = `0`. So `string::npos` is `-1` or some maximum number possible, we were saying if the index position is not equal to `-1`, which means there's an index position found, then we'd generate the output.  

## tempate <typename foo>

In C++, `template` can take any of `typename`. Eg

```
template <typename t>
void myfunc(t x, t y){
  return x+y
}

void main()
{
  std::cout << myfunc(int 1, int 2) << std::endl;       # will get 3
  std::cout << myfunc(char a, char b) << std::endl;     # will get ab
}
```

So intead of defining `myfunc` function twice with `int` and `char`, we can use `typename` which can be `int` or `char` depending on what you define when you call the `myfunc` function.



