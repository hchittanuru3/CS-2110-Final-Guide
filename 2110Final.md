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
		* http://www.geeksforgeeks.org/const-qualifier-in-c/
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
	* **Function Pointers:** Having a pointer that points to code, usually used for dynamically being able to call a function
		```c
		void fun(int a) {
			printf("This is the value %d", a);
		}
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

5. ***Typedef:*** Use this keyword to makes aliases for data types, or structs
	```c
	typedef struct rectangle {
		int length;
		int width;
	} alias_name;
	```
	```c
	typedef some_alias_name int;
	```

6. ***Dynamic Memory Allocation:***
	* **malloc:** Allocates a block of memory
		```c
		void *malloc(size_t size);
		```

	* **free:** Deallocates the memory pointed to at the adddress
		```c
		void free(void* pointer);
		```

	* **realloc:** Resizes the memory block pointed to by a pointer that was allocated with malloc or calloc.
		```c
		void *realloc(void* ptr, size_t size);
		```
		* To implement realloc, you have to deal with four cases, a combination of null and non-null pointers, and 0 and non zero size.
		```c
		void *realloc(void *ptr, size_t size) {
			if (ptr == NULL) {
				malloc(size);
			}
			if (size == 0) {
				free(ptr);
				return NULL;
			}
			void *pointer = malloc(size);
			if (pointer == NULL) {
				return pointer;
			}
			memcpy(pointer, ptr, size); // if ptr's size is less, use that
			free(ptr);
			return pointer;
		}
		```
	* **calloc:** Calloc acts like malloc, but it sets the memory to zero.
		```c
		void *calloc(size_t nmemb, size_t size) {
			void *ptr = malloc(size * nmemb);
			if (ptr == NULL) {
				return NULL;
			}
			memset(ptr, 0, nmemb * size);
			return ptr;
		}
		```
	* **IMPORTANT:** Always remember to free any memory that you allocate once you're done using it.

7. ***Common C Functions:***
	* **qsort:**
	```c
	qsort(void* arr, size_t numelems, size_t sizeofelem, (int) (*compare) (const void*, const void*));
	```
	* **sizeof:** Gives the size of the data type in the given
		* Always use sizeof(), compared to hardcoding these values, as different systems might have different implementations
		```c
		int size_of_int = sizeof(int);
		```
		* This avoids complications, as size of the datatype pointers can differ on different machines, even though datatype sizes remain the same due to C's standard library.
	* **memcpy:**
	* **memset:**

8. ***GBA:***
	* **Size of data types:**
		* *char:* 1 byte
		* *short:* 2 bytes
		* *int:* 4 bytes
		* *pointer:* 4 bytes

9. ***Compiling:***
	* **File Formats:**
		* *.c* Source files with code
		* *.h:* Header files with prototypes, structs and macros
		* *.i:* The file that results after the source files are preprocessed.
		* *.o:* These are the object files, after files are compiled (produced by the compiler) but not linked.
		* *.s:* These are the assembly files, between the assembler and linker.
		* *.exe:* This is the executable, after the files are all linked together.
		* *Order of Operations:* Source -> Pre-Processor -> Compiler -> Assembler -> Linker -> Executable

10. ***Basic I/O:***
	* **getchar()**: ```getchar()``` returns the next input character each time it's called, or EOF when it reaches the end of the file. It returns an ```int```.
	* **putchar()**: ```putchar(c)``` puts the character c , or EOF if there's an error, on the standard output (usually the screen).
	* **Basic printf() conversions:**
		* d, i: decimal number (```int```)
		* c: single character (```int```)
		* s: a string (```char*```)
		* f: a double (```double```)
		* p: pointer (```void*```)

11. ***File I/O:***
	* When dealing with a file, you have to create a file pointer ```FILE *fp;``` that holds information about the file.
	* First step: opening the file. ```fp = fopen(name, mode)``` Mode can either be r, w or a.
	* Always have to close the file: ```fclose(fp)```
	* ```fread(void* ptr, size_t size, size_t no_of_elem, FILE *file)``` reads no_of_elem elements from ```file``` and puts it in ```ptr```.

12. ***Bitwise Operations:***
	* **Packing:**
		* Function:
		```c
		unsigned long long pack (int a, int b) {
			return (a << 32) | b;
		}
		```
		* Macro:
		```c
		#define pack(a, b) (((a) << 32)) | (b))
		```
	* **Unpacking:**
		```c
		void unpack (unsigned long long src, int *ptr_a, int *ptr_b) {
			*ptr_b = (int) (src & 0xFFFFFFFF);
			*ptr_a = (int) ((src << 32) & 0xFFFFFFFF);
		}
		```

13. ***Swapping:***
	* **Swapping Primitives:**
		```c
		void swap (int *x, int*y) {
			int z = *y;
			*y = *x;
			*x = *z;
		}
		```
	* **Swapping Structures:**
		```c
		void swap_struct (void *a, void *b, int size) {
			char *aa = (char*)a;
			char *bb = (char*)b;
			for (int i = 0; i < size; i++) {
				char temp = aa[i];
				aa[i] = bb[i];
				bb[i] = temp;
			}
		}
		```
		* The size in this function would be the size of the structure.

	* **Using memcpy to swap:**
		```c
		void mem_swap(void *a, void *b, size_t size) {
			void *temp = malloc(size);
			memcpy(temp, a, size);
			memcpy(a, b, size);
			memcpy(b, temp, size);
			free(temp);
		}
		```

14. ***qsort Answer:***
	```c
	#include <stdio.h>
	#include <string.h>
	//compare method
	int compare(const void *a, const void *b) {
    	return *(const int*)a - *(const int*)b;
	}
	//qsort method
	void myqsort(void *arr, size_t nmemb, size_t size, int (*compare) (const void *, const void *)) {
    		int i = 0;
    		while (i < (nmemb * size) - size) {
        		void *a = arr + i;
        		void *b = arr + i + size;
        		if (compare(a, b) > 0) {
            			void *temp = malloc(size);
            			memcpy(temp, a, size);
            			memcpy(a, b, size);
            			memcpy(b, temp, size);
            			free(temp);
        		}
        		i +=size;
    		}
	}
	// main method
	int main() {
    		int arr[5] = {3, 3, 4, 1, 8};
    		qsort(arr, 5, sizeof(int), compare);
    		for (int i = 0; i < 5; i++) {
        		printf("%d\n", arr[i]);
    		}
    	}
	```
