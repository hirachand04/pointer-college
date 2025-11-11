Pointer
A pointer is a variable that stores the memory address of another variable.
Instead of holding a direct value, it holds the address where the value is stored in memory. It is the backbone of low-level memory manipulation in C.
A pointer is declared by specifying its data type and name, with an asterisk (*) before the name. Syntax: data_type *pointer_name;
The data type indicates the type of variable the pointer can point to. For example, "int *ptr;" declares a pointer to an integer.
Accessing the pointer directly will just give us the address that is stored in the pointer. To get the value at the address stored in a pointer variable, we use * operator which is call dereferencing operator in C
Note that we use * for two different purposes in pointers. One is to declare a pointer variable and the other is in an operator to get the value stored at address stored in pointer.

#include <stdio.h>

int main()
{

   					 		// Normal Variable
    int var = 10;

  						  // Pointer Variable ptr that stores address of var
    int *ptr = &var;

   						 // Directly accessing ptr will give us an address
    printf("%d", ptr);

    return 0;
}

Initialize the Pointer
A pointer is initialized by assigning it the address of a variable using the address operator (&).
Syntax: pointer_name = &variable;
Initializing a pointer ensures it points to a valid memory location before use.
You can also initialize a pointer to NULL if it doesn’t point to any variable yet: int *ptr = NULL;




Dereference a Pointer
We have to first dereference the pointer to access the value present at the memory address. This is done with the help of dereferencing operator(*) (same operator used in declaration).
#include <stdio.h>
int main()
 {
    int var = 10;
    
   				 // Store address of var variable
    int* ptr = &var;
    
    				// Dereferencing ptr to access the value
    printf("%d", *ptr);
    
    return 0;
}

Out Put 10

Size of Pointers
The size of a pointer in C depends on the architecture (bit system) of the machine, not the data type it points to.
On a 32-bit system, all pointers typically occupy 4 bytes.
On a 64-bit system, all pointers typically occupy 8 bytes.
#include <stdio.h>
int main()
 {
    int *ptr1;
    char *ptr2;
    
 				   // Finding size using sizeof()
    printf("%zu\n", sizeof(ptr1));
    printf("%zu", sizeof(ptr2));
    
    return 0;
}

Out Put 8
               8

Special Types of Pointers
There are 4 special types of pointers that used or referred to in different contexts:

NULL Pointer
The NULL Pointers are those pointers that do not point to any memory location.
They can be created by assigning NULL value to the pointer. A pointer of any type can be assigned the NULL value.
This allows us to check whether the pointer is pointing to any valid memory location by checking if it is equal to NULL.
#include <stdio.h>
int main() 
{
   			 // Null pointer
    int *ptr = NULL;
    
    return 0;
}

Void Pointer
The void pointers in C are the pointers of type void.
It means that they do not have any associated data type.
They are also called generic pointers as they can point to any type and can be typecasted to any type.
#include <stdio.h>
int main()
 {
    			// Void pointer
    void *ptr;
    
    return 0;
}

Wild Pointers
The wild pointers are pointers that have not been initialized with something yet. These types of C-pointers can cause problems in our programs and can eventually cause them to crash. If values are updated using wild pointers, they could cause data abort or data corruption.
#include <stdio.h>
int main() 
{
    // Wild Pointer
    int *ptr;
    
    return 0;
}



Dangling Pointer
A pointer pointing to a memory location that has been deleted (or freed) is called a dangling pointer.
Such a situation can lead to unexpected behavior in the program and also serve as a source of bugs in C programs.


#include <stdio.h>
#include <stdlib.h>

int main()
 {
    int* ptr = (int*)malloc(sizeof(int));

    // After below free call, ptr becomes a dangling pointer
    free(ptr);
    printf("Memory freed\n");

    // removing Dangling Pointer
    ptr = NULL;

    return 0;
}

Output
Memory freed


Pointer to Array
#include <stdio.h>

int main()
 {
    int arr[5] = {10, 20, 30, 40, 50};
    int *p = arr; 		 // p points to first element

    printf("Array elements using pointer:\n");
    for (int i = 0; i < 5; i++) 
{
        printf("*(p + %d) = %d\n", i, *(p + i));
    }

    return 0;
}
Output:
*(p + 0) = 10
*(p + 1) = 20
*(p + 2) = 30
*(p + 3) = 40
*(p + 4) = 50

Sum of Array Elements Using Pointer
#include <stdio.h>

int main()
 {
    int arr[5] = {5, 10, 15, 20, 25};
    int *p = arr;
    int sum = 0;

    for (int i = 0; i < 5; i++)
 {
        sum += *(p + i);
    }

    printf("Sum = %d\n", sum);
    return 0;
}
Output:
Sum = 75

Reverse an Array Using Pointers
#include <stdio.h>

int main() 
{
    int arr[5] = {1, 2, 3, 4, 5};
    int *p1 = arr;          // start pointer
    int *p2 = arr + 4;      // end pointer
    int temp;

    while (p1 < p2)
 {
        temp = *p1;
        *p1 = *p2;
        *p2 = temp;

        p1++;
        p2--;
    }

    printf("Reversed Array: ");
    for (int i = 0; i < 5; i++)
        printf("%d ", arr[i]);

    return 0;
}

Output:
Reversed Array: 5 4 3 2 1

Find Maximum Element Using Pointer
#include <stdio.h>

int main() 
{
    int arr[6] = {12, 45, 23, 51, 19, 8};
    int *p = arr;
    int max = *p;

    for (int i = 1; i < 6; i++) 
{
        if (*(p + i) > max)
            max = *(p + i);
    }

    printf("Maximum Element = %d\n", max);
    return 0;
}
Output:
Maximum Element = 51











Pointer to Array (2D Array Example)
#include <stdio.h>

int main()
 {
    int arr[2][3] = {{1, 2, 3}, {4, 5, 6}};
    int (*p)[3] = arr;  // pointer to an array of 3 integers

    for (int i = 0; i < 2; i++) 
{
        for (int j = 0; j < 3; j++) 
{
            printf("%d ", *(*(p + i) + j));
        }
        printf("\n");
    }

    return 0;
}

Output:
1 2 3
4 5 6


Function Pointer with Parameters
#include <stdio.h>

void add(int a, int b)
 {
    printf("Sum = %d\n", a + b);
}

int main() 
{
    void (*ptr)(int, int);  // pointer to function with two int parameters

    ptr = add;  // assign address
    ptr(5, 10); // call function using pointer

    return 0;
}
Output:
Sum = 15
Array of Function Pointers (Menu-Driven Example)
#include <stdio.h>

int add(int a, int b) { return a + b; }
int sub(int a, int b) { return a - b; }
int mul(int a, int b) { return a * b; }

int main()
 {
    int choice, x, y;
    int (*op[3])(int, int) = {add, sub, mul}; // array of function pointers

    printf("Enter two numbers: ");
    scanf("%d%d", &x, &y);

    printf("Choose operation:\n1. Add\n2. Subtract\n3. Multiply\n");
    scanf("%d", &choice);

    if (choice >= 1 && choice <= 3)
        printf("Result = %d\n", op[choice - 1](x, y));
    else
        printf("Invalid choice!\n");

    return 0;
}

Output:
Enter two numbers: 5 3
Choose operation:
1. Add
2. Subtract
3. Multiply
2
Result = 2

