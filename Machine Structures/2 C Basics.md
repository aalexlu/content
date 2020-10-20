#  C Basics

## C

- function-oriented
- pass-by-value

| op      | performs                                        |
| ------- | ----------------------------------------------- |
| **!**   | returns 0 if value is non-zero, 1 if value is 0 |
| **~**   | bitwise not                                     |
| **&**   | and (turn bits OFF)                             |
| **\|**  | or (turn bits ON)                               |
| **^**   | bitwise xor (flipping bits)                     |
| >>      | shift right                                     |
| **<<**  | shift left                                      |
| *****   | evaluate                                        |
| **? :** | compact if else                                 |
| **&=**  | can do this                                     |

## Programs

Swap value of two ints

``````
void swap(int* x, int* y) {
	int temp = *x;
	*x = *y;
	*y = temp;
}
``````

Return the number of bytes in a string

``````
int mystrlen(char* str) {
	int counter = 0;
	while (*str) {
		str++;
		counter++;
	}
	return counter;
}
``````

Arrays - make sure to pass in size

``````
int sum(int* summands, size_t n) {
	int sum = 0;
	for (int i = 0; i < n; i++) {
		sum += *(summands + i);		//program knows to add 4 when indexing
	}
	return sum;
}
``````

``````
void increment(char* string, int n) {
	while (string[i] != 0) {
		(*(string + i))++;		//or string[i]++
	}
}
``````

## Memory Management

| Stack                             | Heap             | Static                           | Code                 |
| --------------------------------- | ---------------- | -------------------------------- | -------------------- |
| local variables                   | result of malloc | static variables                 | machine instructions |
| string literals (char[7] s = "a") |                  | global variables                 |                      |
|                                   |                  | constants                        |                      |
|                                   |                  | string literals (char * s = "a") |                      |

Heap Allocation

- **array arr of k integers:**

  - ``````
    int* arr = (int*) malloc(k * sizeof(int));
    ``````

- **string str of p characters (+1 for null terminator):**

  - ``````
    char* str = (char*) malloc((p+1) * sizeof(char));
    ``````

- **n x m matrix mat of integers initialized to 0:**

  - ``````
    int* mat0 = (int*) calloc(n * m, sizeof(int));		//1D
    ``````

  - ``````
    int** mat1 = (int**) calloc(n, sizeof(int*));		//2D
    for (int i = 0; i < n; i++) {
    	*(mat1 + i) = (int*) calloc(m, sizeof(int));
    }
    ``````

Linked List Example

``````
struct ll_node {
	int first;
	struct ll_node* rest;
}

void prepend(struct ll_node** lst, int value) {
	struct ll_node* item = (struct ll_node*) malloc(sizeof(struct ll_node));
	item->first = value;
	item->rest = *lst;
	*lst = item;
}

void free_ll(struct ll_node** lst) {
	if (*lst) {
		free_ll(&((*lst)->rest));
		free(*lst);
	}
	*lst = NULL;		//so writes to **lst fail instead of writing to unusable memory
}
``````

*view lab01, lab02*

