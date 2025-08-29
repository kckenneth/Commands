## HEADER file ifndef (IF Not DEFined)

https://stackoverflow.com/questions/3246803/why-use-ifndef-class-h-and-define-class-h-in-h-file-but-not-in-cpp

```
#ifndef _MYFILE_H_
#define _MYFILE_H_
```

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

https://pdos.csail.mit.edu/6.828/2014/readings/pointers.pdf

This is a good chapter on the usage of pointer explanation. Whenever we use the equal `=`, there's `lvalue (left value)` and `rvalue (right value)`. 

When we declare a variable we set aside a spot in memory to hold the value of the appropriate type. Once that is done the name of the variable can be interpreted in one of two ways. When used on the left side of the assignment operator, the compiler interprets it as the memory location to which to move that value resulting from evaluation of the right side of the assignment operator. But, when used on the right side of the assignment operator, the name of a variable is interpreted to mean the contents stored at that memory address set aside to hold the value of that variable.

```
k = 5;
```
In this statement, there're something that I could understand based on what I have studied. 
1. There's a mapping on the `lvalue` on the variable table.
2. On that table, the right side is the memory address of the variable `k`.
3. After the mapping, the compiler will go and update the value of `5` in the memory address of `k`.

```
|  k  | 0x000134    |     # imaginary table on the variable k and its memory address on the right side.
```

In the memory address `0x000134`, the value of `5` will be updated. 

Now imagine, 
```
k = 5;   <--- line 1
j = 2;   <--- line 2
k = j;   <--- line 3
```
After line 1 and 2, the table will look like this. 
```
|  k  | 0x000134   |    --> has the value of `5` at the address
|  j  | 0x000542   |    --> has the value of `2` at the address
```
Each memory address will have `5` and `2` value respectively. 

In line 3, since the variable `k` is on the left side of the `=`, its memory address won't be touched. The variable `j` is on the right side of the `=`, the compiler will go and check its value in the memory address at `0x000542`. The compiler finds the value of `2` at the memory address at `0x000542`. The compiler will then update the value `2` at the memory address of `k` which is `0x000134`. The table after the line 3 will look the same. But the value at the memory address at `0x000134` will change to `2`. 

```
|  k  | 0x000134   |    --> has the value of `2` at the address
|  j  | 0x000542   |    --> has the value of `2` at the address
```

Now let's look at the pointer assignment. This time, we don't want to store the value at the memory address. We want to store another memory address at the current memory address. Like this. 

```
|  k  | 0x000134   |    --> has the value of `0x000542` at the address
|  j  | 0x000542   |    --> has the value of `2` at the address
```

In this situation, the variable `k` will have the value of `0x000542` which is a memory address. We know that the memory address is `j's`. But it can be any memory addresses. So we need to let the compiler know that the variable `k` will store the memory address. 

```
int *k;
```

To store the memory address, so what we need to do is,
```
int *k;
k = &j;
```
By adding a unary operator `&` in front of `j`, we're asking the compiler to look up the memory address of `j`, and assign the memory adderss which is `rvalue` right now, to the pointer `k`. 


More on pointer examples. 

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


## Vector

```
std::vector<float> x(10, 1);
```

This is prepopulating the vector size `10` with a value of `1`. 

```
[1,1,1,1,1,1,1,1,1,1]
```


--------------

## GDB debugging 

after you restarted the ydisc and it failed, it will generate the coredump file `core.xxxxx`. You can run the commands below to back trace where the runtime fails. 

```
gdb /home/y/bin64/ydisc core.10579
```

After the `gdb` runs and you're now in `gdb` shell, you can type `bt` to check on the backtrace. 

sample
```
gdb /home/y/bin/ydisc core.10579 
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
[New LWP 10603]
[New LWP 10604]
[New LWP 10607]
[New LWP 10614]
[New LWP 10609]
[New LWP 10605]
[New LWP 10606]
[New LWP 10616]
[New LWP 10612]
[New LWP 10667]
[New LWP 10632]
[New LWP 10651]
[New LWP 10675]
[New LWP 10678]
[New LWP 10613]
[New LWP 10611]
[New LWP 10610]
[New LWP 10623]
[New LWP 10619]
[New LWP 10649]
[New LWP 10654]
[New LWP 10615]
[New LWP 10677]
[New LWP 10683]
[New LWP 10608]
[New LWP 10592]
[New LWP 10691]
[New LWP 10599]
[New LWP 10681]
[New LWP 10595]
[New LWP 10679]
[New LWP 10687]
[New LWP 10692]
[New LWP 10618]
[New LWP 10585]
[New LWP 10600]
[New LWP 10653]
[New LWP 10674]
[New LWP 10597]
[New LWP 10617]
[New LWP 10697]
[New LWP 10657]
[New LWP 10655]
[New LWP 10689]
[New LWP 10682]
[New LWP 10694]
[New LWP 10685]
[New LWP 10695]
[New LWP 10688]
[New LWP 10696]
[New LWP 10673]
[New LWP 10665]
[New LWP 10579]
[New LWP 10622]
[New LWP 10690]
[New LWP 10594]
[New LWP 10601]
[New LWP 10668]
[New LWP 10680]
[New LWP 10686]
[New LWP 10666]
[New LWP 12303]
[New LWP 10676]
[New LWP 10598]
[New LWP 10671]
[New LWP 10664]
[New LWP 10624]
[New LWP 10662]
[New LWP 10602]
[New LWP 10593]
[New LWP 10663]
[New LWP 10661]
[New LWP 10693]
[New LWP 10620]
[New LWP 10660]
[New LWP 10659]
[New LWP 10684]
[New LWP 10596]
[New LWP 10670]
[New LWP 10638]
[New LWP 10658]
[New LWP 10672]
[New LWP 10656]
[New LWP 10621]
[New LWP 10625]
[New LWP 10669]
[New LWP 10635]
[New LWP 10650]
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib64/libthread_db.so.1".
Core was generated by `/home/y/bin64/ydisc /qis/ydisc/conf/Server.conf'.
Program terminated with signal 11, Segmentation fault.
#0  0x00007f0ed659b1a0 in ?? ()
Missing separate debuginfos, use: debuginfo-install apr-1.4.8-7.el7.x86_64 apr-util-1.5.2-6.el7_9.1.x86_64 avro-1.7.7-42079899.el7.x86_64 boost-filesystem-1.53.0-28.el7.x86_64 boost-iostreams-1.53.0-28.el7.x86_64 boost-program-options-1.53.0-28.el7.x86_64 boost-regex-1.53.0-28.el7.x86_64 boost-signals-1.53.0-28.el7.x86_64 boost-system-1.53.0-28.el7.x86_64 boost-thread-1.53.0-28.el7.x86_64 bzip2-libs-1.0.6-13.el7.x86_64 cyrus-sasl-lib-2.1.26-24.el7_9.x86_64 dh_rainbow_client_api_cpp-18.7-45446693.el7.x86_64 dh_rainbow_file_counter_cpp-14.1-45446524.el7.x86_64 dh_rainbow_libutils_cpp-80.2-45446205.el7.x86_64 elfutils-libelf-0.176-5.el7.x86_64 elfutils-libs-0.176-5.el7.x86_64 expat-2.1.0-15.el7_9.x86_64 glib2-2.56.1-9.el7_9.x86_64 glibc-2.17-326.el7_9.3.x86_64 keyutils-libs-1.5.8-3.el7.x86_64 krb5-libs-1.15.1-55.el7_9.x86_64 libattr-2.4.46-13.el7.x86_64 libcap-2.22-11.el7.x86_64 libcom_err-1.42.9-19.el7.x86_64 libconfig-1.4.9-5.el7.x86_64 libdb-5.3.21-25.el7.x86_64 libdb4-4.8.30-13.el7.x86_64 libevent-2.0.21-4.el7.x86_64 libgcc-4.8.5-44.el7.x86_64 libgcrypt-1.5.3-14.el7.x86_64 libgpg-error-1.12-3.el7.x86_64 libicu-50.2-4.el7_7.x86_64 libselinux-2.5-15.el7.x86_64 libstdc++-4.8.5-44.el7.x86_64 libuuid-2.23.2-65.el7_9.1.x86_64 libxml2-2.9.1-6.el7_9.6.x86_64 log4cxx-0.10.0-16.el7.x86_64 lz4-1.8.3-1.el7.x86_64 mdbm-4.12.4.146-1.el7.x86_64 nspr-4.35.0-1.el7_9.x86_64 nss-3.90.0-2.el7_9.x86_64 nss-softokn-freebl-3.90.0-6.el7_9.x86_64 nss-util-3.90.0-1.el7_9.x86_64 openldap-2.4.44-25.el7_9.x86_64 openssl-libs-1.0.2k-26.el7_9.x86_64 pcre-8.32-17.el7.x86_64 protobuf-c-1.1.1-30.el7.x86_64 systemd-libs-219-78.el7_9.9.x86_64 xz-libs-5.2.2-2.el7_9.x86_64 yaml-cpp-0.5.1-2.el7.x86_64 zlib-1.2.7-21.el7_9.x86_64
(gdb) bt
#0  0x00007f0ed659b1a0 in ?? ()
#1  0x00007f06654034a1 in qis::local::CICallback::operator() (this=0x7f10a8006ae0, source="main", tags=std::vector of length 3, capacity 4 = {...}, seq_prob=1, 
    seq_crfprob=1) at ContextualInterpreterModule.cc:226
#2  0x00007f105217ca3d in qis::Interpreter::convertQIGTEOutputJson (this=this@entry=0x7f0ff1c366f0, outputs=..., modification=<optimized out>, 
    tokens=std::vector of length 5, capacity 8 = {...}, ci_callback=..., explainer=...) at Interpreter.cpp:560
#3  0x00007f06653f000b in qis::ContextualInterpreterModule::requestCompletionCallback (this=0x4d87898, context=..., interface=..., response=...)
    at ContextualInterpreterModule.cc:791
#4  0x00007f06653f1503 in operator() (a3=..., a2=..., a1=..., p=<optimized out>, this=<optimized out>) at /usr/include/boost/bind/mem_fn_template.hpp:393
#5  operator()<boost::system::error_code, boost::_mfi::mf3<boost::system::error_code, qis::ContextualInterpreterModule, middleware::AsyncContext&, ContextualInterpreterInterface&, qis::HttpResponse&>, boost::_bi::list3<middleware::AsyncContext&, ContextualInterpreterInterface&, qis::HttpResponse&> > (a=<synthetic pointer>, f=..., 
    this=<optimized out>) at /usr/include/boost/bind/bind.hpp:447
#6  operator()<middleware::AsyncContext, ContextualInterpreterInterface, qis::HttpResponse> (a3=..., a2=..., a1=..., this=<optimized out>)
    at /usr/include/boost/bind/bind_template.hpp:116
#7  boost::detail::function::function_obj_invoker3<boost::_bi::bind_t<boost::system::error_code, boost::_mfi::mf3<boost::system::error_code, qis::ContextualInterpreterModule, middleware::AsyncContext&, ContextualInterpreterInterface&, qis::HttpResponse&>, boost::_bi::list4<boost::_bi::value<qis::ContextualInterpreterModule*>, boost::arg<1>, boost::arg<2>, boost::arg<3> > >, boost::system::error_code, middleware::AsyncContext&, ContextualInterpreterInterface&, qis::HttpResponse&>::invoke (function_obj_ptr=..., 
    a0=..., a1=..., a2=...) at /usr/include/boost/function/function_template.hpp:132
#8  0x00007f06653f63f5 in operator() (a2=..., a1=..., a0=..., this=0x7f10a8006ed0) at /usr/include/boost/function/function_template.hpp:767
#9  invoke (response=..., interface=..., ctx=..., this=0x7f10a8006ed0) at /home/y/include/ydisc/CallbackWrapperImpl.hh:81
#10 middleware::CallbackWrapperImpl<middleware::AsyncModuleAdapter<qis::ContextualInterpreterModule, ContextualInterpreterInterface>, qis::HttpResponse, true>::callback (
    this=0x7f10a8006e30) at /home/y/include/ydisc/CallbackWrapperImpl.hh:162
#11 0x00007f10e6582b95 in middleware::TaskImpl::callback (this=0x7f10a80078e0, callback=...) at impl/Task.cc:594
#12 0x00007f100f905b6e in responseComplete (this=<optimized out>) at /home/y/include/ydisc/TaskHolderImpl.hh:113
#13 responseComplete (this=<optimized out>) at /home/y/include/ydisc/TaskHolder.hh:99
---Type <return> to continue, or q <return> to quit---q
Quit
(gdb) quit

```

