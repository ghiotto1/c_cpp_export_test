# Purpose
This C source code file implements a linked list data structure specifically designed to manage a list of moves, likely for a chess application, as suggested by the inclusion of "chesslib/movelist.h". The primary functionality provided by this code is the creation, manipulation, and management of a move list, which includes operations such as adding moves, retrieving moves by index, undoing the last move, and converting the list of moves into a UCI (Universal Chess Interface) string format. The code defines several key functions: [`moveListCreate`](#moveListCreate) initializes a new move list, [`moveListNodeCreate`](#moveListNodeCreate) creates a new node for a move, [`moveListAdd`](#moveListAdd) appends a move to the list, [`moveListGet`](#moveListGet) retrieves a move at a specified index, [`moveListUndo`](#moveListUndo) removes the last move, [`moveListGetUciString`](#moveListGetUciString) generates a UCI string representation of the move list, and [`moveListFree`](#moveListFree) deallocates the memory used by the move list.

The code is structured to be part of a larger chess library, as indicated by the inclusion of a header file from "chesslib". It does not define a main function, suggesting that it is intended to be compiled as part of a library rather than an executable. The move list is implemented as a singly linked list, with each node containing a move and a pointer to the next node. The code handles memory allocation and deallocation explicitly, which is crucial in C to prevent memory leaks. The [`moveListGetUciString`](#moveListGetUciString) function is particularly noteworthy as it converts the list of moves into a format that can be used by chess engines and interfaces that support the UCI protocol, highlighting the code's role in facilitating communication between different components of a chess application.
# Imports and Dependencies

---
- `stdlib.h`
- `string.h`
- `chesslib/movelist.h`


# Functions

---
### moveListCreate<!-- {{#callable:moveListCreate}} -->
The `moveListCreate` function allocates and initializes a new `moveList` structure with default values.
- **Inputs**: None
- **Control Flow**:
    - Allocate memory for a new `moveList` structure using `malloc`.
    - Initialize the `head` pointer of the list to `NULL`, indicating an empty list.
    - Initialize the `tail` pointer of the list to `NULL`, indicating an empty list.
    - Set the `size` of the list to `0`, indicating that the list is empty.
    - Return the pointer to the newly created `moveList` structure.
- **Output**: A pointer to a newly allocated and initialized `moveList` structure.


---
### moveListNodeCreate<!-- {{#callable:moveListNodeCreate}} -->
The function `moveListNodeCreate` allocates memory for a new `moveListNode`, initializes it with a given move, and sets its next pointer to NULL.
- **Inputs**:
    - `move`: A `move` structure that contains the data to be stored in the new node.
- **Control Flow**:
    - Allocate memory for a new `moveListNode` structure.
    - Assign the provided `move` to the `move` field of the newly created node.
    - Set the `next` pointer of the node to `NULL`, indicating it is the last node in the list.
    - Return the pointer to the newly created node.
- **Output**: A pointer to the newly created `moveListNode` structure.


---
### moveListAdd<!-- {{#callable:moveListAdd}} -->
The `moveListAdd` function appends a new move to the end of a move list, updating the list's head, tail, and size accordingly.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure where the new move will be added.
    - `move`: A `move` structure representing the move to be added to the list.
- **Control Flow**:
    - Create a new `moveListNode` using the provided `move` by calling [`moveListNodeCreate`](#moveListNodeCreate).
    - Check if the `head` of the list is `NULL`, indicating the list is empty.
    - If the list is empty, set both the `head` and `tail` of the list to the newly created node.
    - If the list is not empty, set the `next` pointer of the current `tail` to the new node and update the `tail` to this new node.
    - Increment the `size` of the list by one.
- **Output**: The function does not return a value; it modifies the `moveList` structure in place.
- **Functions called**:
    - [`moveListNodeCreate`](#moveListNodeCreate)


---
### moveListGet<!-- {{#callable:moveListGet}} -->
The `moveListGet` function retrieves a move from a linked list of moves at a specified index.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure, which is a linked list of moves.
    - `index`: An unsigned integer representing the position in the list from which to retrieve the move.
- **Control Flow**:
    - Initialize `currNode` to the head of the list.
    - Iterate through the list, moving to the next node and decrementing `index` until `index` is zero.
    - Return the move stored in the current node.
- **Output**: The function returns a `move` from the specified index in the `moveList`.


---
### moveListUndo<!-- {{#callable:moveListUndo}} -->
The `moveListUndo` function removes the last move from a singly linked list of moves, effectively undoing the most recent move.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure, which represents a singly linked list of moves.
- **Control Flow**:
    - Check if the list is NULL or if the list's head is NULL; if so, return immediately as there is nothing to undo.
    - Check if the list contains only one node (i.e., `list->head->next` is NULL); if true, free the head node and set both the head and tail pointers to NULL.
    - If the list contains more than one node, iterate through the list to find the last node and its predecessor.
    - Free the last node, set the predecessor's `next` pointer to NULL, and update the list's tail pointer to the predecessor node.
    - Decrement the size of the list by one.
- **Output**: The function does not return a value; it modifies the `moveList` structure in place by removing the last node and updating the list's size.


---
### moveListGetUciString<!-- {{#callable:moveListGetUciString}} -->
The function `moveListGetUciString` generates a UCI (Universal Chess Interface) formatted string from a list of chess moves.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure, which contains a linked list of chess moves.
- **Control Flow**:
    - Check if the move list is empty; if so, allocate a single character for the string, set it to null, and return it.
    - If the move list contains only one move, convert that move to a UCI string and return it.
    - Calculate the required size for the UCI string, accounting for each move's characters, spaces, and any promotion characters.
    - Allocate memory for the UCI string based on the calculated size.
    - Iterate over each move in the list, convert it to a UCI string, append it to the result string, and add a space after each move.
    - Replace the last space with a null terminator to properly end the string.
    - Return the constructed UCI string.
- **Output**: A dynamically allocated string containing the UCI representation of the moves in the list, which must be freed by the caller.
- **Functions called**:
    - [`moveGetUci`](move.c.driver.md#moveGetUci)


---
### moveListFree<!-- {{#callable:moveListFree}} -->
The `moveListFree` function deallocates all memory associated with a `moveList` and its nodes.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure that needs to be freed.
- **Control Flow**:
    - Initialize a pointer `node` to the head of the list.
    - Enter a loop that continues as long as `node` is not NULL.
    - Inside the loop, store the next node in a temporary pointer `next`.
    - Free the current node.
    - Move to the next node by setting `node` to `next`.
    - After the loop, free the `moveList` structure itself.
- **Output**: The function does not return any value; it frees the memory occupied by the `moveList` and its nodes.


