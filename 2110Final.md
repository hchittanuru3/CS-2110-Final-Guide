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
	* **volatile:** This keyword tells the compiler not to optimize anything to do with the variable, and this would be used when you're interfacing with hardware
	   * For example, if you're using a variable that is mapped to RAM, you want to have a volatile qualifier in front of it, like ```volatile int mappedToMem; ```
	* **auto:** An auto variable is a variable that is allocated and deallocated automatically when the program flow enters the variable's scope. 
		* Not used since the default variable type in C is *auto*
	* **const:** This keyword tells the compiler that this variable is read only, and cannot be changed once it is initially set
		* If you try to change it, the code won't compile
	* **register:** Registers are faster than memory to access, and this keyword tells the compiler to put this data into a register
		* Typically this is not used, since the compiler can perform these optimizations by itself
	* **extern:** If you are declaring something that needs to be defined elsewhere
		* This is present implicitly when you declare variables/ functions without defining them
		* For code to compile, you need to define the variable somewhere else in the code
   
2. ***Macros:***
	* A macro is a code fragment that has been given a name
		* The C preprocessor goes through the code and replaces any instances of the name with the code that it defines
	* The format is ```#define ADD(a,b) ((a) + (b))``` or ```#define LIST_SIZE 1024```. 
		* **IMPORTANT: There are parentheses around the arguments in the function macro and no semicolon**
	
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
	* **Function Pointers:** Having a pointer that points to code rather than
	```c
	void fun(int a) {
		printf("This is the value %d", a);
	}
	```

	```c
	int main() {
		void (*fun_ptr)(int) = fun;
	}
	```
	    * Used for passing functions in as parameters into other functions
	 
4. ***Structures:***
	* A structure is a collection of variables grouped together under a single name, similar to a class. 
	```c
	struct rectangle {
	  int length;
	  int width;
	};
	```
	* **NOTE:** You want to pass in pointers to structures, rather than the structure itself into functions, because structures are large, and you don't want to put them on the stack for no reason.
	
5. ***Dynamic Memory Allocation:***

6. ***Common C Functions:***
	* **qsort**:
	* **sizeof**:
		* Always use sizeof(), compared to calculating sizes of data types by hand.

7. ***GBA:***
	* **Size of data types:**
		* *char:* 1
		* *short:* 2
		* *int:* 4
		* *pointer:* 8

8. ***Compiling:***
	* **File Formats:**
		* *.c and .h:* These are the source files.
		* *.i:* The file that results after the source files are preprocessed.
		* *.o:* These are the object files, after files are compiled (produced by the compiler) but not linked.
		* *.s:* These are the assembly files, between the assembler and linker.
		* *.exe:* This is the executable, after the files are all linked together.
		* *Order of Operations:* Source -> Pre-Processor -> Compiler -> Assembler -> Linker -> Executable
		
9. ***File I/O:***
