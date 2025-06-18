# Purpose
The provided code is a C++ source file, likely part of a larger project, specifically a chess-related application named "ChessProject." It defines the implementation of a [`Square`](#SquareSquare) class, which represents a square on a chessboard. The class provides narrow functionality focused on managing the state of a single square, including its coordinates (`_x` and `_y`) and the chess piece occupying it (`_piece`). The class includes methods to set and retrieve the piece occupying the square, check if the square is occupied, and access the square's coordinates. This file is intended to be compiled as part of the project and is not a standalone executable, as it lacks a `main` function.
# Imports and Dependencies

---
- `piece.h`
- `square.h`


# Data Structures

---
### Square<!-- {{#data_structure:Square}} -->
- **Description**: [See definition](square.h.driver.md#Square)
- **Member Functions**:
    - [`Square::Square`](#SquareSquare)
    - [`Square::~Square`](#SquareSquare)
    - [`Square::setOccupier`](#SquaresetOccupier)
    - [`Square::getX`](#SquaregetX)
    - [`Square::getY`](#SquaregetY)
    - [`Square::occupied`](#Squareoccupied)
    - [`Square::occupiedBy`](#SquareoccupiedBy)

**Methods**

---
#### Square::Square<!-- {{#callable:Square::Square}} -->
The `Square` constructor initializes a `Square` object with specified x and y coordinates and sets the occupying piece to NULL.
- **Inputs**:
    - `x`: The x-coordinate of the square on the board.
    - `y`: The y-coordinate of the square on the board.
- **Control Flow**:
    - The constructor initializes the private member variable `_x` with the value of the input parameter `x`.
    - The constructor initializes the private member variable `_y` with the value of the input parameter `y`.
    - The constructor sets the private member variable `_piece` to NULL, indicating that the square is initially unoccupied.
- **Output**: There is no return value as this is a constructor for the `Square` class.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::\~Square<!-- {{#callable:Square::~Square}} -->
The destructor for the `Square` class is a default destructor that performs no specific actions.
- **Inputs**: None
- **Control Flow**:
    - The destructor `~Square()` is defined but contains no code, indicating it performs no operations when a `Square` object is destroyed.
- **Output**: There is no output or return value from the destructor, as it is a default destructor with no specific logic implemented.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::setOccupier<!-- {{#callable:Square::setOccupier}} -->
The `setOccupier` function assigns a `Piece` pointer to the `_piece` member variable of a `Square` object, indicating which piece occupies the square.
- **Inputs**:
    - `piece`: A pointer to a `Piece` object that is to be set as the occupier of the square.
- **Control Flow**:
    - The function takes a single argument, `piece`, which is a pointer to a `Piece` object.
    - The function assigns the `piece` pointer to the private member variable `_piece` of the `Square` class.
- **Output**: The function does not return any value.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::getX<!-- {{#callable:Square::getX}} -->
The `getX` function returns the X-coordinate of a `Square` object.
- **Inputs**: None
- **Control Flow**:
    - The function accesses the private member variable `_x` of the `Square` class.
    - It returns the value of `_x`.
- **Output**: The function returns an integer representing the X-coordinate of the square.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::getY<!-- {{#callable:Square::getY}} -->
The `getY` function returns the Y-coordinate of a `Square` object.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `_y`.
- **Output**: The function returns an integer representing the Y-coordinate of the square.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::occupied<!-- {{#callable:Square::occupied}} -->
The `occupied` function checks if a `Square` object is occupied by a `Piece`.
- **Inputs**: None
- **Control Flow**:
    - The function accesses the private member `_piece` of the `Square` class.
    - It returns the boolean value of `_piece`, which is `true` if `_piece` is not `NULL` (indicating the square is occupied), and `false` if `_piece` is `NULL` (indicating the square is not occupied).
- **Output**: A boolean value indicating whether the square is occupied by a piece.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::occupiedBy<!-- {{#callable:Square::occupiedBy}} -->
The `occupiedBy` function returns the `Piece` object that currently occupies the `Square`.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the private member variable `_piece`, which is a pointer to a `Piece` object.
- **Output**: A pointer to a `Piece` object that occupies the `Square`, or `NULL` if no piece is present.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)



