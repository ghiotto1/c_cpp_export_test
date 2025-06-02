# Purpose
This C source code file implements a linked list data structure specifically designed to manage a list of moves, likely for a chess game, as suggested by the inclusion of "chesslib/movelist.h". The primary components of this implementation include functions for creating and managing a `moveList`, which is a singly linked list where each node represents a move. Key functions include [`moveListCreate`](#moveListCreate) for initializing a new list, [`moveListNodeCreate`](#moveListNodeCreate) for creating a new node, [`moveListAdd`](#moveListAdd) for appending a move to the list, [`moveListGet`](#moveListGet) for retrieving a move by its index, and [`moveListUndo`](#moveListUndo) for removing the last move from the list. Additionally, the [`moveListGetUciString`](#moveListGetUciString) function generates a UCI (Universal Chess Interface) formatted string from the list of moves, which is a common format used in chess engines for move representation.

The code is structured to provide a narrow functionality focused on managing a sequence of moves, with a clear emphasis on operations typical for a linked list, such as adding, retrieving, and removing elements. The implementation is not a standalone executable but rather a component intended to be part of a larger system, likely a chess engine or application, as indicated by its reliance on external definitions such as `move` and `moveGetUci`. The file does not define public APIs or external interfaces directly but provides essential internal functionality that can be utilized by other parts of the chess application through the `movelist.h` header. The code also includes memory management functions like [`moveListFree`](#moveListFree) to ensure proper deallocation of resources, highlighting the importance of efficient memory handling in C programming.
# Imports and Dependencies

---
- `stdlib.h`
- `string.h`
- `chesslib/movelist.h`


# Functions

---
### moveListCreate<!-- {{#callable:moveListCreate}} -->
The `moveListCreate` function allocates and initializes a new `moveList` structure with default values.
- **Inputs**:
    - None
- **Control Flow**:
    - Allocate memory for a new `moveList` structure using `malloc`.
    - Initialize the `head` pointer of the list to `NULL`, indicating an empty list.
    - Initialize the `tail` pointer of the list to `NULL`, indicating an empty list.
    - Set the `size` of the list to `0`, indicating that the list is currently empty.
    - Return the pointer to the newly created `moveList` structure.
- **Output**:
    - A pointer to a newly allocated and initialized `moveList` structure.


---
### moveListNodeCreate<!-- {{#callable:moveListNodeCreate}} -->
The function `moveListNodeCreate` allocates memory for a new `moveListNode`, initializes it with a given move, and sets its next pointer to NULL.
- **Inputs**:
    - `move`: A `move` structure that contains the data to be stored in the new node.
- **Control Flow**:
    - Allocate memory for a new `moveListNode` using `malloc`.
    - Assign the provided `move` to the `move` field of the newly created node.
    - Set the `next` pointer of the node to `NULL` to indicate it is the last node in the list.
    - Return the pointer to the newly created node.
- **Output**:
    - A pointer to the newly created `moveListNode` containing the specified move and a `NULL` next pointer.


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
    - If the list is not empty, set the `next` pointer of the current `tail` node to the new node and update the `tail` to the new node.
    - Increment the `size` of the list by one.
- **Output**:
    - The function does not return a value; it modifies the `moveList` structure in place by adding a new node to it.
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
- **Output**:
    - The function returns the `move` located at the specified index in the `moveList`.


---
### moveListUndo<!-- {{#callable:moveListUndo}} -->
The `moveListUndo` function removes the last move from a singly linked list of moves, updating the list's head, tail, and size accordingly.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure, which represents a singly linked list of moves.
- **Control Flow**:
    - Check if the list is NULL or if the list's head is NULL; if so, return immediately as there is nothing to undo.
    - If the list contains only one node, free the head node and set both the head and tail pointers to NULL.
    - If the list contains more than one node, traverse the list to find the second-to-last node.
    - Free the last node, update the second-to-last node's next pointer to NULL, and set the list's tail to the second-to-last node.
    - Decrement the list's size by one.
- **Output**:
    - The function does not return a value; it modifies the input `moveList` in place by removing the last node and updating the list's metadata.


---
### moveListGetUciString<!-- {{#callable:moveListGetUciString}} -->
The function `moveListGetUciString` generates a UCI (Universal Chess Interface) formatted string from a list of chess moves.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure, which contains a linked list of chess moves.
- **Control Flow**:
    - Check if the move list is empty; if so, allocate a single character for the string, set it to null, and return it.
    - If the move list contains only one move, convert that move to a UCI string and return it.
    - Calculate the required size for the UCI string, considering 4 characters per move, a space between moves, and additional space for promotion characters.
    - Allocate memory for the UCI string based on the calculated size.
    - Iterate over each move in the list, convert it to a UCI string, append it to the result string, and add a space after each move.
    - Replace the last space with a null terminator to properly end the string.
    - Return the constructed UCI string.
- **Output**:
    - A dynamically allocated string containing the UCI representation of the moves in the list, which must be freed by the caller.
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
- **Output**:
    - The function does not return any value; it performs memory deallocation for the provided `moveList` and its nodes.


