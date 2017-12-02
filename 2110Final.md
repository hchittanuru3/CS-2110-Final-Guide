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
       