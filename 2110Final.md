# CS 2110 Final Guide
1. ***Keywords in C***
   * **static:** Static can be used in two cases:
       * *Global variables (or) functions:* Using static restricts the scope of the variable/function to the file it is in.
       * *In-function variables:* The variable is stored in statically allocated memory, so the value of it won't be reset everytime the function is invocated.
       ```c
       void func() {
           int a = 10;
           static int b = 10;
           a++;
           b++;
       }
       // This code will always ensure that a is 11, but with every invocation of func(), b increases one.
       ```
   * **volatile:** This keyword tells the compiler not to optimize anything to do with the variable, and this would be used when you're interfacing with hardware.
       * For example, if you're using a variable that is mapped to RAM, you want to have a volatile qualifier in front of it, like ```volatile int mappedToMem; ```.
   * **auto:** An auto variable is a variable that is allocated and deallocated automatically when the program flow enters the variable's scope. We don't need to use the keyword auto because the compiler automatically interprets a local variable as auto, as it is on every local variable.
   * **const:**
   * **register:**
   * **extern:**
   
2. ***Macros:***
    * For a macro: the format is ```#define ADD(a,b) ((a) + (b))``` or ```#define LIST_SIZE 1024```. The parentheses around the arguments in the function macro and no semicolon are important features.
    
3. ***Pointers:***
    * A pointer is a variable that contains the address of another variable. The following example illustrates how to use a pointer and assign it:
    ```c
    int x = 0;
    int *ptr;
    ptr = &x;
     ```
     * Dereferencing pointers is the action of accessing what the pointer is pointing to. The operator ```*``` is used to dereference a pointer. Looking at the previous example, we can say that ```x == *ptr``` is true. 
     * **NOTE:** You cannot dereference a void pointer, because C's compiler doesn't know the size of the object it's pointing to. To work around this, we can do the following:
     ```c
     void *ptr;
     int x = 20;
     ptr = &x;
     return *(int*) ptr;
     ```
     * Arrays in C use pointers. We can use a pointer to point to the first element in the array, and everytime you want to access the next element you can increment the pointer and dereference it.
     
4. ***Structures:***
    * A structure is a collection of variables grouped together under a single name, similar to a class. 
    ```c
    struct rectangle {
      int length;
      int width;
    };
    ```
5. ***Dynamic Memory Allocation:***

6. ***Common C Functions:***
    * **qsort**:
    * **sizeof**:
        * Always use sizeof(), compared to calculating sizes of data types by hand.

7. ***GBA:***

8. ***Compiling:***
    * **File Formats:**
        * *.c and .h:* These are the source files.
        * *.i:* The file that results after the source files are preprocessed.
        * *.o:* These are the object files, after files are compiled (produced by the compiler) but not linked.
        * *.exe:* This is the executable, after the files are all linked together.
        
