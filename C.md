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
 
 
 
