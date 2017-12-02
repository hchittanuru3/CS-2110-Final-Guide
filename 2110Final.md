# CS 2110 Final Guide
1. **Keywords in C**
   * Static: Static can be used in two cases:
       * Global variables (or) functions: Using static restricts the scope of the variable/function to the file it is in.
       * In-function variables: The variable is stored in statically allocated memory, so the value of it won't be reset everytime the function is invocated.
       ```c
       void func() {
           int a = 10;
           static int b = 10;
           a++;
           b++;
       }
       // This code will always ensure that a is 11, but with every invocation of func(), b increases one.
       ```
   * Volatile: This keyword tells the compiler not to optimize anything to do with the variable, and this would be used when you're interfacing with hardware.
       * For example, if you're using a variable that is mapped to RAM, you want to have a volatile qualifier in front of it, like ```volatile int mappedToMem; ```.
   * Auto: An auto variable is a variable that is allocated and deallocated automatically when the program flow enters the variable's scope. We don't need to use the keyword auto because the compiler automatically interprets a variable as auto.
   
2. Macros:
    * For a macro: the format is ```#define```
