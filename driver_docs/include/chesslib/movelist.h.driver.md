# Purpose
This C header file defines a data structure and associated operations for managing a list of chess moves, likely as part of a larger chess application. It includes the definition of two structures: `moveListNode`, which represents a single node in the list containing a chess move and a pointer to the next node, and `moveList`, which represents the entire list with pointers to the head and tail nodes and a size indicator. The file declares several functions for creating and manipulating these lists, such as adding moves, retrieving moves by index, undoing the last move, and converting the list to a UCI (Universal Chess Interface) string format. Additionally, it provides a function to free the memory allocated for the list and its nodes, ensuring proper resource management. This header file is essential for managing sequences of moves in a chess game, facilitating operations like move tracking and conversion to standard formats.
# Imports and Dependencies

---
- `stddef.h`
- `chesslib/move.h`


# Global Variables

---
### moveListCreate
- **Type**: `function`
- **Description**: The `moveListCreate` function is a global function that is responsible for creating and initializing a new instance of a `moveList` structure. This structure is used to manage a list of moves, typically in a chess game context, and includes a head and tail pointer to `moveListNode` structures, as well as a size to track the number of moves.
- **Use**: This function is used to create an empty `moveList` that can be populated with moves using other functions like `moveListAdd`.


---
### moveListNodeCreate
- **Type**: `function`
- **Description**: The `moveListNodeCreate` function is a constructor for creating a new node in a linked list of moves, specifically for a chess game. It takes a `move` as an argument and returns a pointer to a newly allocated `moveListNode` structure, which contains the move and a pointer to the next node in the list.
- **Use**: This function is used to initialize and allocate memory for a new node in a move list, which is part of a linked list structure representing a sequence of chess moves.


---
### moveListGetUciString
- **Type**: `function pointer`
- **Description**: The `moveListGetUciString` is a function that takes a pointer to a `moveList` structure and returns a dynamically allocated string representing the moves in the list in UCI (Universal Chess Interface) format. The returned string must be freed by the caller to avoid memory leaks.
- **Use**: This function is used to convert a list of chess moves into a UCI-compliant string representation.


# Data Structures

---
### moveListNode
- **Type**: `struct`
- **Members**:
    - `move`: A `move` object representing a single move in a chess game.
    - `next`: A pointer to the next `moveListNode` in the linked list.
- **Description**: The `moveListNode` is a structure used to represent a node in a singly linked list of chess moves. Each node contains a `move` object, which holds the details of a single chess move, and a pointer to the next node in the list, allowing for traversal through the sequence of moves. This structure is part of a larger system for managing and manipulating lists of chess moves, facilitating operations such as adding, retrieving, and undoing moves.


---
### moveList
- **Type**: `struct`
- **Members**:
    - `head`: A pointer to the first node in the move list.
    - `tail`: A pointer to the last node in the move list.
    - `size`: The number of nodes currently in the move list.
- **Description**: The `moveList` structure is a linked list designed to store a sequence of chess moves. It maintains pointers to the head and tail of the list for efficient insertion and removal of moves, and it tracks the total number of moves with the `size` member. This structure is used to manage and manipulate a list of moves in a chess game, allowing operations such as adding new moves, retrieving moves by index, undoing the last move, and converting the list to a UCI string format.


# Function Declarations (Public API)

---
### moveListCreate<!-- {{#callable_declaration:moveListCreate}} -->
Create an empty move list.
- **Description**: This function initializes and returns a new, empty move list, which is a data structure used to store a sequence of chess moves. It allocates memory for the move list and sets its initial state with no moves. This function should be called when a new move list is needed, and the returned pointer must be managed by the caller, who is responsible for freeing it using `moveListFree` to avoid memory leaks.
- **Inputs**:
    - None
- **Output**: A pointer to a newly allocated `moveList` structure, initialized to be empty.
- **See also**: [`moveListCreate`](../../src/chesslib/movelist.c.driver.md#moveListCreate)  (Implementation)


---
### moveListNodeCreate<!-- {{#callable_declaration:moveListNodeCreate}} -->
Creates a new move list node with the specified move.
- **Description**: This function is used to create a new node for a move list, initializing it with a specified move. It allocates memory for the node and sets its move field to the provided move, while the next pointer is initialized to NULL. This function is typically used when constructing or modifying a move list in a chess application. The caller is responsible for managing the memory of the created node, including freeing it when it is no longer needed.
- **Inputs**:
    - `move`: The move to be stored in the new node. It is expected to be a valid move as defined by the chess library. The function does not validate the move, so the caller must ensure its correctness.
- **Output**: A pointer to the newly created moveListNode containing the specified move, or NULL if memory allocation fails.
- **See also**: [`moveListNodeCreate`](../../src/chesslib/movelist.c.driver.md#moveListNodeCreate)  (Implementation)


---
### moveListAdd<!-- {{#callable_declaration:moveListAdd}} -->
Adds a move to the end of a move list.
- **Description**: This function appends a new move to the end of the specified move list, updating the list's size and maintaining the correct order of moves. It should be used when you need to record a new move in a sequence of moves, such as in a chess game. The function assumes that the move list has been properly initialized before calling. It handles the case where the list is initially empty by setting both the head and tail to the new node. The function does not handle invalid input and assumes that the provided move list pointer is valid and non-null.
- **Inputs**:
    - `list`: A pointer to a moveList structure where the move will be added. Must not be null and should be properly initialized before calling this function. The caller retains ownership.
    - `move`: A move to be added to the list. The function does not impose any specific constraints on the move's value.
- **Output**: None
- **See also**: [`moveListAdd`](../../src/chesslib/movelist.c.driver.md#moveListAdd)  (Implementation)


---
### moveListGet<!-- {{#callable_declaration:moveListGet}} -->
Retrieve a move from the move list at a specified index.
- **Description**: This function is used to access a specific move from a move list by providing an index. It is useful when you need to retrieve a move at a particular position in the list. The function assumes that the index is within the bounds of the list, so it should only be called with a valid index that is less than the size of the list. The move list must be properly initialized and populated with moves before calling this function.
- **Inputs**:
    - `list`: A pointer to a moveList structure from which the move is to be retrieved. Must not be null and should be properly initialized.
    - `index`: An unsigned integer representing the position of the move to retrieve. Must be less than the size of the list to avoid undefined behavior.
- **Output**: The move located at the specified index in the move list.
- **See also**: [`moveListGet`](../../src/chesslib/movelist.c.driver.md#moveListGet)  (Implementation)


---
### moveListUndo<!-- {{#callable_declaration:moveListUndo}} -->
Removes the last move from the move list.
- **Description**: This function is used to remove the last move from a move list, effectively undoing the most recent move. It should be called when you need to backtrack or reverse the last action in a sequence of moves. The function safely handles cases where the list is empty or contains only one move, ensuring no operations are performed on a null or invalid list. It decrements the size of the list accordingly and updates the list's tail pointer.
- **Inputs**:
    - `list`: A pointer to a moveList structure representing the list of moves. Must not be null. If the list is empty or null, the function performs no action. The caller retains ownership of the list.
- **Output**: None
- **See also**: [`moveListUndo`](../../src/chesslib/movelist.c.driver.md#moveListUndo)  (Implementation)


---
### moveListGetUciString<!-- {{#callable_declaration:moveListGetUciString}} -->
Creates a UCI string representation of the moves in the list.
- **Description**: This function generates a string in UCI (Universal Chess Interface) format representing all the moves contained in the provided move list. It is useful for exporting or displaying the sequence of moves in a standardized format. The function allocates memory for the resulting string, which the caller is responsible for freeing. If the list is empty, the function returns an empty string. If the list contains only one move, the string will represent that single move without any trailing space. The function handles promotion moves by including the promotion character in the string.
- **Inputs**:
    - `list`: A pointer to a moveList structure containing the moves to be converted to a UCI string. Must not be null. The function assumes the list is properly initialized and populated with valid moves.
- **Output**: A dynamically allocated string containing the UCI representation of the moves in the list. The caller is responsible for freeing this string. If the list is empty, an empty string is returned.
- **See also**: [`moveListGetUciString`](../../src/chesslib/movelist.c.driver.md#moveListGetUciString)  (Implementation)


---
### moveListFree<!-- {{#callable_declaration:moveListFree}} -->
Frees a move list and all its nodes.
- **Description**: Use this function to release all memory associated with a move list, including all its nodes. It should be called when the move list is no longer needed to prevent memory leaks. Ensure that the list pointer is valid and was previously allocated by moveListCreate. After calling this function, the list pointer should not be used unless it is reinitialized.
- **Inputs**:
    - `list`: A pointer to a moveList structure that must have been created by moveListCreate. The pointer must not be null, and the function will free all nodes within the list as well as the list itself. Passing a null pointer will result in undefined behavior.
- **Output**: None
- **See also**: [`moveListFree`](../../src/chesslib/movelist.c.driver.md#moveListFree)  (Implementation)


