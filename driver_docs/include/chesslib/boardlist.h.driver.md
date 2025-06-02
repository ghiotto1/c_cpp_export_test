# Purpose
This C header file defines a data structure and associated operations for managing a linked list of chess boards, likely as part of a larger chess application. It includes the definition of two structures: `boardListNode`, which represents a node in the linked list containing a pointer to a `board` and a pointer to the next node, and `boardList`, which maintains the list's head, tail, and size. The file declares functions for creating and managing these lists, including [`boardListCreate`](#boardListCreate) and [`boardListNodeCreate`](#boardListNodeCreate) for initialization, [`boardListAdd`](#boardListAdd) for adding a board to the list, [`boardListGet`](#boardListGet) for retrieving a board by index, [`boardListUndo`](#boardListUndo) for removing the last added board, and [`boardListFree`](#boardListFree) for deallocating the list and its nodes. This header file is essential for handling dynamic collections of chess boards, facilitating operations such as move history management in a chess game.
# Imports and Dependencies

---
- `stddef.h`
- `chesslib/board.h`


# Global Variables

---
### boardListCreate
- **Type**: `function`
- **Description**: The `boardListCreate` function is a global function that is responsible for creating and initializing a new instance of the `boardList` data structure. This function sets up an empty list with no nodes and a size of zero, preparing it for further operations such as adding or retrieving board nodes.
- **Use**: This function is used to initialize a new `boardList` structure, which can then be used to manage a collection of `board` instances in a linked list format.


---
### boardListNodeCreate
- **Type**: `function pointer`
- **Description**: The `boardListNodeCreate` is a function that creates a new `boardListNode` structure, which is a node in a linked list containing a pointer to a `board` and a pointer to the next node in the list. This function is used to initialize a new node with a given `board` pointer, setting up the basic structure for a linked list of boards.
- **Use**: This function is used to create and initialize a new node in a linked list of boards, facilitating the management of a sequence of board states.


---
### boardListGet
- **Type**: `function`
- **Description**: The `boardListGet` function is a global function that retrieves a pointer to a `board` from a `boardList` at a specified index. It is part of a set of operations that manage a linked list of chess boards.
- **Use**: This function is used to access a specific board within a `boardList` by providing the list and the desired index.


# Data Structures

---
### boardListNode
- **Type**: `struct`
- **Members**:
    - `board`: A pointer to a `board` structure, representing a chess board.
    - `next`: A pointer to the next `boardListNode` in the linked list.
- **Description**: The `boardListNode` is a node structure used in a linked list to store a sequence of chess boards. Each node contains a pointer to a `board` structure, which represents a chess board, and a pointer to the next node in the list, allowing for traversal through the list. This structure is part of a larger system for managing a list of chess boards, enabling operations such as adding new boards, retrieving boards by index, and undoing moves by removing boards from the list.


---
### boardList
- **Type**: `struct`
- **Members**:
    - `head`: A pointer to the first node in the board list.
    - `tail`: A pointer to the last node in the board list.
    - `size`: The number of nodes currently in the board list.
- **Description**: The `boardList` structure is a linked list designed to manage a sequence of `board` objects, where each node in the list is represented by a `boardListNode`. It maintains pointers to the head and tail of the list for efficient insertion and removal operations, and tracks the total number of nodes with the `size` member. This structure is useful for applications that require dynamic management of chess board states, such as implementing undo functionality in a chess game.


# Function Declarations (Public API)

---
### boardListCreate<!-- {{#callable_declaration:boardListCreate}} -->
Create and initialize an empty board list.
- **Description**: This function allocates and initializes a new boardList structure, setting up an empty list ready for use. It should be called when a new board list is needed, typically at the start of operations involving board management. The function returns a pointer to the newly created boardList, which initially has no nodes and a size of zero. The caller is responsible for managing the memory of the returned boardList, including eventually freeing it with boardListFree to avoid memory leaks.
- **Inputs**:
    - None
- **Output**: A pointer to a newly allocated and initialized boardList structure.
- **See also**: [`boardListCreate`](../../src/chesslib/boardlist.c.driver.md#boardListCreate)  (Implementation)


---
### boardListNodeCreate<!-- {{#callable_declaration:boardListNodeCreate}} -->
Creates a new board list node with the specified board.
- **Description**: This function is used to create a new node for a linked list of boards, encapsulating the provided board pointer within a newly allocated node. It is typically used when constructing or modifying a linked list of boards, such as when implementing a history of board states in a chess game. The function allocates memory for the node, initializes it with the given board, and sets the next pointer to NULL. It is the caller's responsibility to ensure that the provided board pointer is valid and to manage the memory of the created node, including freeing it when it is no longer needed.
- **Inputs**:
    - `b`: A pointer to a board structure that the new node will encapsulate. The pointer must be valid, and the caller retains ownership of the board. The function does not check for nullity, so passing a null pointer will result in undefined behavior.
- **Output**: A pointer to the newly created boardListNode, or NULL if memory allocation fails.
- **See also**: [`boardListNodeCreate`](../../src/chesslib/boardlist.c.driver.md#boardListNodeCreate)  (Implementation)


---
### boardListAdd<!-- {{#callable_declaration:boardListAdd}} -->
Adds a board to the end of a board list.
- **Description**: This function appends a new board to the end of the specified board list. It should be used when you want to maintain a sequence of boards, such as in a game history. The function assumes that the list has been properly initialized and is not null. It updates the list's head and tail pointers as necessary and increments the size of the list. The function does not handle invalid input, so the caller must ensure that the list and board are valid and properly initialized before calling this function.
- **Inputs**:
    - `list`: A pointer to a boardList structure where the board will be added. Must not be null and should be initialized before use. The caller retains ownership.
    - `b`: A pointer to a board structure to be added to the list. Must not be null and should be a valid board. The caller retains ownership.
- **Output**: None
- **See also**: [`boardListAdd`](../../src/chesslib/boardlist.c.driver.md#boardListAdd)  (Implementation)


---
### boardListGet<!-- {{#callable_declaration:boardListGet}} -->
Retrieve a board from the board list at a specified index.
- **Description**: Use this function to access a specific board from a board list by providing the index of the desired board. The function assumes that the index is within the bounds of the list, meaning it should be less than the size of the list. It is important to ensure that the list is not empty and that the index is valid to avoid undefined behavior. This function does not modify the list or the boards within it.
- **Inputs**:
    - `list`: A pointer to a boardList from which a board is to be retrieved. Must not be null, and the list should be properly initialized and populated with boards.
    - `index`: An unsigned integer representing the position of the board to retrieve. Must be less than the size of the list to ensure valid access.
- **Output**: A pointer to the board at the specified index in the list. If the index is out of bounds, the behavior is undefined.
- **See also**: [`boardListGet`](../../src/chesslib/boardlist.c.driver.md#boardListGet)  (Implementation)


---
### boardListUndo<!-- {{#callable_declaration:boardListUndo}} -->
Removes the last board from the board list.
- **Description**: This function is used to remove the last board from a given board list, effectively undoing the last addition. It should be called when you want to revert the most recent change to the list. The function safely handles cases where the list is empty or contains only one element, ensuring no operation is performed if the list is already empty. It decrements the size of the list and updates the tail pointer accordingly. This function must be called with a valid boardList pointer, and the list should have been previously initialized.
- **Inputs**:
    - `list`: A pointer to a boardList structure. Must not be null. The function will handle the case where the list is empty or has only one node, performing no operation if the list is empty.
- **Output**: None
- **See also**: [`boardListUndo`](../../src/chesslib/boardlist.c.driver.md#boardListUndo)  (Implementation)


---
### boardListFree<!-- {{#callable_declaration:boardListFree}} -->
Frees all memory associated with a board list.
- **Description**: This function is used to release all memory allocated for a boardList and its associated nodes. It should be called when the board list is no longer needed to prevent memory leaks. The function traverses the list, freeing each board and node, and finally frees the list itself. It is important to ensure that the list is not used after this function is called, as it will be in an undefined state.
- **Inputs**:
    - `list`: A pointer to the boardList to be freed. Must not be null. The function will free all nodes and boards within the list, as well as the list structure itself. The caller should not use the list after this function is called.
- **Output**: None
- **See also**: [`boardListFree`](../../src/chesslib/boardlist.c.driver.md#boardListFree)  (Implementation)


