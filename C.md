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

https://stackoverflow.com/questions/36962658/what-exactly-is-the-purpose-of-the-asterisk-in-pointers 
https://dev.to/sandordargo/how-to-use-ampersands-in-c-3kga

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

