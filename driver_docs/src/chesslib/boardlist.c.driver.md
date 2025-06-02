# Purpose
This C source code file implements a linked list data structure specifically designed to manage a collection of chess boards, as indicated by the inclusion of "chesslib/boardlist.h". The primary purpose of this code is to provide a dynamic list that can store, retrieve, and manage chess board states, which is useful in applications such as chess engines or games where board states need to be tracked over time. The code defines several functions to create and manipulate the list: [`boardListCreate`](#boardListCreate) initializes a new list, [`boardListNodeCreate`](#boardListNodeCreate) creates a new node for a board, [`boardListAdd`](#boardListAdd) appends a board to the list, [`boardListGet`](#boardListGet) retrieves a board at a specified index, [`boardListUndo`](#boardListUndo) removes the last board from the list, and [`boardListFree`](#boardListFree) deallocates the entire list.

The implementation uses a singly linked list structure, with each node containing a pointer to a chess board and a pointer to the next node. The list maintains pointers to both the head and tail nodes, facilitating efficient additions to the end of the list. However, the [`boardListUndo`](#boardListUndo) function highlights a limitation of the singly linked list, as it requires traversal from the head to find the penultimate node when removing the last element. This code is part of a broader library, as suggested by the inclusion of a header file, and is intended to be used as a module within larger chess-related software systems. It does not define public APIs or external interfaces directly but provides essential internal functionality for managing sequences of chess board states.
# Imports and Dependencies

---
- `stdlib.h`
- `chesslib/boardlist.h`


# Functions

---
### boardListCreate<!-- {{#callable:boardListCreate}} -->
The `boardListCreate` function initializes and returns a new, empty `boardList` structure.
- **Inputs**:
    - None
- **Control Flow**:
    - Allocate memory for a new `boardList` structure.
    - Initialize the `head` pointer of the list to `NULL`, indicating the list is empty.
    - Initialize the `tail` pointer of the list to `NULL`, indicating the list is empty.
    - Set the `size` of the list to 0, indicating there are no elements in the list.
    - Return the pointer to the newly created `boardList`.
- **Output**:
    - A pointer to a newly allocated and initialized `boardList` structure.


---
### boardListNodeCreate<!-- {{#callable:boardListNodeCreate}} -->
The function `boardListNodeCreate` allocates memory for a new `boardListNode`, initializes it with a given `board`, and sets its `next` pointer to `NULL`.
- **Inputs**:
    - `b`: A pointer to a `board` structure that the new `boardListNode` will hold.
- **Control Flow**:
    - Allocate memory for a new `boardListNode` structure using `malloc`.
    - Assign the provided `board` pointer `b` to the `board` field of the newly created `boardListNode`.
    - Set the `next` pointer of the new `boardListNode` to `NULL`.
    - Return the pointer to the newly created `boardListNode`.
- **Output**:
    - A pointer to the newly created `boardListNode` structure.


---
### boardListAdd<!-- {{#callable:boardListAdd}} -->
The `boardListAdd` function appends a new board node to the end of a linked list of boards, updating the list's head, tail, and size accordingly.
- **Inputs**:
    - `list`: A pointer to a `boardList` structure, representing the linked list to which the board will be added.
    - `b`: A pointer to a `board` structure, representing the board to be added to the list.
- **Control Flow**:
    - Create a new `boardListNode` using the provided board `b`.
    - Check if the list's head is `NULL`, indicating the list is empty.
    - If the list is empty, set both the head and tail of the list to the new node.
    - If the list is not empty, link the current tail's `next` pointer to the new node and update the list's tail to the new node.
    - Increment the list's size by one.
- **Output**:
    - The function does not return a value; it modifies the `boardList` structure in place by adding a new node to it.
- **Functions called**:
    - [`boardListNodeCreate`](#boardListNodeCreate)


---
### boardListGet<!-- {{#callable:boardListGet}} -->
The `boardListGet` function retrieves a board from a linked list of boards at a specified index.
- **Inputs**:
    - `list`: A pointer to a `boardList` structure, which is a linked list of boards.
    - `index`: An unsigned integer representing the position in the list from which to retrieve the board.
- **Control Flow**:
    - Initialize `currNode` to the head of the list.
    - Iterate through the list, moving `currNode` to the next node and decrementing `index` until `index` reaches zero.
    - Return the board associated with the current node.
- **Output**:
    - Returns a pointer to the `board` at the specified index in the list.


---
### boardListUndo<!-- {{#callable:boardListUndo}} -->
The `boardListUndo` function removes the last node from a singly linked list of boards, freeing its memory and updating the list's tail and size.
- **Inputs**:
    - `list`: A pointer to a `boardList` structure, which represents a singly linked list of board nodes.
- **Control Flow**:
    - Check if the list is NULL or if the list's head is NULL; if so, return immediately as there is nothing to undo.
    - If the list contains only one node, free the board and the node, then set both the head and tail of the list to NULL.
    - If the list contains more than one node, traverse the list to find the last node and its predecessor.
    - Free the board and the last node, update the predecessor's next pointer to NULL, and set the list's tail to the predecessor.
    - Decrement the size of the list by one.
- **Output**:
    - The function does not return a value; it modifies the input `boardList` by removing the last node and updating its size and tail.


---
### boardListFree<!-- {{#callable:boardListFree}} -->
The `boardListFree` function deallocates all memory associated with a `boardList` and its nodes.
- **Inputs**:
    - `list`: A pointer to a `boardList` structure that needs to be freed.
- **Control Flow**:
    - Initialize a pointer `node` to the head of the list.
    - Enter a loop that continues as long as `node` is not NULL.
    - Inside the loop, store the next node in a temporary pointer `next`.
    - Free the memory allocated for the `board` in the current node.
    - Free the memory allocated for the current node itself.
    - Move to the next node by setting `node` to `next`.
    - After the loop, free the memory allocated for the `boardList` structure itself.
- **Output**:
    - The function does not return any value; it performs memory deallocation for the given `boardList` and its nodes.


