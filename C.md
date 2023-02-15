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
 for (std::vector::iterator it = data.beging(); it != data.end(); ++it) { }
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
 
