# Purpose
The `board.cpp` file is part of a Chess project and is responsible for implementing the [`Board`](#Board::Board) class, which models the chessboard. This file provides the core functionality for managing the board's state, including the setup and teardown of the board's squares, checking the clarity of paths (vertical, horizontal, and diagonal) between squares, and displaying the board's current state. The [`Board`](#Board::Board) class uses a singleton pattern, as evidenced by the `getBoard()` method, which ensures that only one instance of the board exists throughout the application. This is achieved by maintaining a static pointer `_theBoard` to the single instance of the [`Board`](#Board::Board).

The file includes several key methods that facilitate chess gameplay. The constructor initializes the board by creating a grid of `Square` objects, while the destructor ensures proper memory management by deleting these objects. The [`isClearVertical`](#Board::isClearVertical), [`isClearHorizontal`](#Board::isClearHorizontal), and [`isClearDiagonal`](#Board::isClearDiagonal) methods are crucial for determining if a path between two squares is unobstructed, which is essential for validating moves in chess. The [`isEndRow`](#Board::isEndRow) method checks if a square is in the first or last row, which can be important for pawn promotion. Finally, the [`display`](#Board::display) method outputs the current state of the board to a given output stream, showing the position of pieces and the board's layout. This file is integral to the chess game's functionality, providing both the data structure and the logic needed to manage the board's state and interactions.
# Imports and Dependencies

---
- `board.h`
- `piece.h`


# Global Variables

---
### \_theBoard
- **Type**: `Board*`
- **Description**: `_theBoard` is a static pointer to a `Board` object, used to implement the singleton pattern for the `Board` class. It is initialized to `NULL` and is intended to ensure that only one instance of the `Board` class exists throughout the program.
- **Use**: This variable is used to store and provide access to the single instance of the `Board` class, ensuring that all operations on the board are performed on the same instance.


# Data Structures

---
### Board<!-- {{#data_structure:Board}} -->
- **Description**: [See definition](board.h.driver.md#Board)
- **Member Functions**:
    - [`Board::Board`](#Board::Board)
    - [`Board::~Board`](#Board::~Board)
    - [`Board::getBoard`](#Board::getBoard)
    - [`Board::squareAt`](#Board::squareAt)
    - [`Board::isClearVertical`](#Board::isClearVertical)
    - [`Board::isClearHorizontal`](#Board::isClearHorizontal)
    - [`Board::isClearDiagonal`](#Board::isClearDiagonal)
    - [`Board::isEndRow`](#Board::isEndRow)
    - [`Board::display`](#Board::display)

**Methods**

---
#### Board::Board<!-- {{#callable:Board::Board}} -->
The `Board` constructor initializes an 8x8 chess board by creating `Square` objects for each position on the board.
- **Inputs**:
    - None
- **Control Flow**:
    - The constructor iterates over a fixed dimension (8x8) using two nested loops.
    - For each pair of indices (i, j), it creates a new `Square` object with coordinates (i, j).
    - The newly created `Square` object is assigned to the corresponding position in the `_squares` array.
- **Output**:
    - The function does not return any value as it is a constructor.
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::\~Board<!-- {{#callable:Board::~Board}} -->
The destructor `~Board` deallocates memory for the 2D array of `Square` objects in the `Board` class.
- **Inputs**:
    - None
- **Control Flow**:
    - Iterates over each row of the `_squares` 2D array using a loop with index `i`.
    - For each row, iterates over each column using a loop with index `j` and deletes the `Square` object at `_squares[i][j]`.
    - After deleting all `Square` objects in a row, deletes the row itself using `delete[] _squares[i]`.
    - Finally, deletes the entire `_squares` array using `delete[] _squares`.
- **Output**:
    - The function does not return any value as it is a destructor.
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::getBoard<!-- {{#callable:Board::getBoard}} -->
The `getBoard` function implements the singleton pattern to ensure only one instance of the `Board` class is created and returned.
- **Inputs**:
    - None
- **Control Flow**:
    - Check if the static member `_theBoard` is `NULL`.
    - If `_theBoard` is `NULL`, create a new instance of `Board` and assign it to `_theBoard`.
    - Return the `_theBoard` instance.
- **Output**:
    - Returns a pointer to the single instance of the `Board` class.
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::squareAt<!-- {{#callable:Board::squareAt}} -->
The `squareAt` function retrieves a pointer to a `Square` object located at the specified coordinates on the board.
- **Inputs**:
    - `x`: The x-coordinate of the square on the board, representing the column index.
    - `y`: The y-coordinate of the square on the board, representing the row index.
- **Control Flow**:
    - Access the 2D array `_squares` using the provided x and y coordinates.
    - Return the `Square` pointer located at `_squares[x][y]`.
- **Output**:
    - A pointer to the `Square` object located at the specified (x, y) coordinates on the board.
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::isClearVertical<!-- {{#callable:Board::isClearVertical}} -->
The `isClearVertical` function checks if the vertical path between two squares on a chess board is clear of any occupied squares.
- **Inputs**:
    - `from`: A reference to the starting `Square` object.
    - `to`: A reference to the ending `Square` object.
- **Control Flow**:
    - Initialize pointers `start` and `end` to determine the order of squares based on their y-values.
    - Assign `start` to the square with the smaller y-value and `end` to the other square.
    - Check if the x-values of `start` and `end` are equal to ensure no horizontal movement; if not, set `valid` to false.
    - If the x-values are equal, iterate over the y-values between `start` and `end`.
    - For each square in the vertical path, check if it is occupied using the [`squareAt`](#Board::squareAt) method.
    - If any square is occupied, set `valid` to false.
    - Return the boolean `valid` indicating if the path is clear.
- **Output**:
    - A boolean value indicating whether the vertical path between the two squares is clear (true) or not (false).
- **Functions called**:
    - [`Board::squareAt`](#Board::squareAt)
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::isClearHorizontal<!-- {{#callable:Board::isClearHorizontal}} -->
The `isClearHorizontal` function checks if the horizontal path between two squares on a chess board is clear of any occupied squares.
- **Inputs**:
    - `from`: A reference to the starting `Square` object.
    - `to`: A reference to the ending `Square` object.
- **Control Flow**:
    - Initialize pointers `start` and `end` to determine the direction of horizontal traversal based on the x-values of `from` and `to`.
    - Check if there is any vertical movement by comparing the y-values of `start` and `end`; if they differ, set `valid` to false.
    - If there is no vertical movement, iterate over the horizontal path between `start` and `end` (excluding the endpoints) to check if any square is occupied.
    - If any square in the path is occupied, set `valid` to false.
    - Return the value of `valid`, which indicates whether the path is clear.
- **Output**:
    - A boolean value indicating whether the horizontal path between the two squares is clear (true) or not (false).
- **Functions called**:
    - [`Board::squareAt`](#Board::squareAt)
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::isClearDiagonal<!-- {{#callable:Board::isClearDiagonal}} -->
The `isClearDiagonal` function checks if the path between two squares on a chess board is a clear diagonal, meaning no pieces are blocking the path.
- **Inputs**:
    - `from`: A reference to the starting Square object on the board.
    - `to`: A reference to the ending Square object on the board.
- **Control Flow**:
    - Initialize a boolean variable `valid` to true, which will be used to determine if the diagonal path is clear.
    - Calculate the translation in the x and y directions between the `from` and `to` squares.
    - Determine the direction of movement in both x and y directions by setting `xDir` and `yDir` to 1 or -1 based on the sign of the translations.
    - Check if the absolute values of the x and y translations are equal; if not, set `valid` to false as the path is not diagonal.
    - If the path is diagonal, iterate over each square along the diagonal path (excluding the starting and ending squares).
    - For each square along the path, check if it is occupied using the [`squareAt`](#Board::squareAt) method; if any square is occupied, set `valid` to false.
    - Return the value of `valid`, indicating whether the diagonal path is clear.
- **Output**:
    - A boolean value indicating whether the diagonal path between the two squares is clear (true) or blocked (false).
- **Functions called**:
    - [`Board::squareAt`](#Board::squareAt)
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::isEndRow<!-- {{#callable:Board::isEndRow}} -->
The `isEndRow` function checks if a given square is located on the first or last row of the board.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the location on the board to be checked.
- **Control Flow**:
    - Retrieve the Y-coordinate of the `location` square using `location.getY()`.
    - Check if the Y-coordinate is equal to 0 or `_DIMENSION - 1` (indicating the first or last row of the board).
    - Return `true` if the Y-coordinate matches either condition, otherwise return `false`.
- **Output**:
    - A boolean value indicating whether the square is on the first or last row of the board.
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)


---
#### Board::display<!-- {{#callable:Board::display}} -->
The `display` function outputs the current state of the chess board to a given output stream, showing the position of pieces on an 8x8 grid.
- **Inputs**:
    - `outStream`: An output stream (such as `std::cout`) where the board's display will be printed.
- **Control Flow**:
    - The function begins by printing the column labels (a to h) and a separator line to the output stream.
    - It then iterates over each row of the board from top to bottom (black pieces at the top, white at the bottom).
    - For each row, it prints the row number, followed by the contents of each square in that row, separated by vertical bars.
    - If a square is occupied by a piece, it calls the `display` method of the piece to print its representation; otherwise, it prints two spaces to indicate an empty square.
    - After printing all squares in a row, it prints the row number again and a separator line.
    - Finally, it prints the column labels again at the bottom of the board.
- **Output**:
    - The function does not return a value; it outputs the board's state to the provided output stream.
- **See also**: [`Board`](board.h.driver.md#Board)  (Data Structure)



