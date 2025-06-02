# Purpose
This C header file defines a data structure and associated functions for managing a "square set" in a chess-related application. The square set is represented as a 64-bit integer (`uint64_t`), where each bit corresponds to a square on a chessboard, indicating whether it is "on" or "off." The file includes function prototypes for [`sqSetSet`](#sqSetSet) and [`sqSetGet`](#sqSetGet), which are used to modify and retrieve the state of a specific square within the set, respectively. The file also includes a note to potentially add conditional typedefs for systems that do not support `uint64_t`, suggesting a future enhancement for broader compatibility. This header is part of a larger library, as indicated by the inclusion of "chesslib/square.h".
# Imports and Dependencies

---
- `chesslib/square.h`


# Function Declarations (Public API)

---
### sqSetSet<!-- {{#callable_declaration:sqSetSet}} -->
Sets the state of a square in a square set.
- **Description**: This function modifies the state of a specific square within a square set, which is represented as a 64-bit integer. It should be used to mark a square as either 'on' or 'off' based on the provided value. The function does nothing if the square is invalid, ensuring that only valid squares are modified. This function is typically used in scenarios where you need to track the state of multiple squares on a chessboard, such as in board games or simulations. The square set must be properly initialized before calling this function.
- **Inputs**:
    - `ss`: A pointer to the square set (sqSet) to be modified. Must not be null, and the caller retains ownership.
    - `s`: The square (sq) whose state is to be set. Must be a valid square; otherwise, the function will not modify the square set.
    - `value`: A uint8_t value indicating the desired state of the square: non-zero to set the square 'on', zero to set it 'off'.
- **Output**: None
- **See also**: [`sqSetSet`](../../src/chesslib/squareset.c.driver.md#sqSetSet)  (Implementation)


---
### sqSetGet<!-- {{#callable_declaration:sqSetGet}} -->
Retrieve the status of a square in a square set.
- **Description**: This function checks whether a specific square in a square set is marked as 'on' or 'off'. It is used to determine the current state of a square within a 64-bit representation of a chessboard. The function should be called with a valid square set and a valid square identifier. If the square identifier is invalid, the function returns 0, indicating the square is 'off'. This function is useful for querying the state of individual squares in board-related operations.
- **Inputs**:
    - `ss`: A pointer to a sqSet, which is a 64-bit integer representing the state of each square on a chessboard. The pointer must not be null, and the caller retains ownership.
    - `s`: A square identifier of type sq. It must represent a valid square on the board. If the square is invalid (e.g., SQ_INVALID), the function returns 0.
- **Output**: Returns 1 if the specified square is 'on' in the set, and 0 if it is 'off' or if the square is invalid.
- **See also**: [`sqSetGet`](../../src/chesslib/squareset.c.driver.md#sqSetGet)  (Implementation)


