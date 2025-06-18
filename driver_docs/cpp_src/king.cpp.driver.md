# Purpose
The provided code is a C++ source file, `king.cpp`, which is part of a larger chess project. It defines the implementation of the [`King`](#KingKing) class, which inherits from a `RestrictedPiece` class, likely representing a chess piece with limited movement capabilities. The [`King`](#KingKing) class constructor initializes the piece's color, and the destructor is defined but does not perform any specific actions. The [`value`](#Kingvalue) method returns a constant integer, possibly indicating the king's value in the game, though it is set to zero, which might imply a special status rather than a point value. The [`canMoveTo`](#KingcanMoveTo) method implements the king's movement logic, allowing it to move one square in any direction (forward, backward, sideways, or diagonally), adhering to standard chess rules. Finally, the [`display`](#Kingdisplay) method outputs the king's representation, combining its color and the letter "K" to the console, which is useful for visualizing the board state. This code provides narrow functionality specific to the behavior and representation of a king piece in a chess game.
# Imports and Dependencies

---
- `king.h`


# Data Structures

---
### King<!-- {{#data_structure:King}} -->
- **Description**: [See definition](king.h.driver.md#King)
- **Member Functions**:
    - [`King::King`](#KingKing)
    - [`King::~King`](#KingKing)
    - [`King::value`](#Kingvalue)
    - [`King::canMoveTo`](#KingcanMoveTo)
    - [`King::display`](#Kingdisplay)
- **Inherits From**:
    - `RestrictedPiece`

**Methods**

---
#### King::King<!-- {{#callable:King::King}} -->
The `King` constructor initializes a `King` object by calling the constructor of its parent class `RestrictedPiece` with a boolean indicating the piece's color.
- **Inputs**:
    - `isWhite`: A boolean indicating whether the King piece is white (true) or black (false).
- **Control Flow**:
    - The constructor `King::King(bool isWhite)` is called with a boolean parameter `isWhite`.
    - The constructor initializes the `King` object by invoking the constructor of its parent class `RestrictedPiece` with the `isWhite` parameter.
- **Output**: There is no return value as this is a constructor for the `King` class.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::\~King<!-- {{#callable:King::~King}} -->
The destructor `~King()` is a default destructor for the `King` class that performs no specific actions.
- **Inputs**: None
- **Control Flow**:
    - The destructor `~King()` is called when a `King` object is destroyed.
    - No specific actions or resource deallocations are performed within the destructor.
- **Output**: There is no output or return value from the destructor.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::value<!-- {{#callable:King::value}} -->
The `value` function returns the point value of the King piece, which is 0.
- **Inputs**: None
- **Control Flow**:
    - The function simply returns the integer value 0.
- **Output**: The function returns an integer value of 0, representing the point value of the King piece in a chess game.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::canMoveTo<!-- {{#callable:King::canMoveTo}} -->
The `canMoveTo` function determines if a King chess piece can legally move to a specified square based on standard chess rules for a King's movement.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the King is attempting to move.
- **Control Flow**:
    - Initialize `validMove` to `false`.
    - Calculate `translationX` as the difference between the x-coordinate of the target location and the current x-coordinate of the King.
    - Calculate `translationY` as the difference between the y-coordinate of the target location and the current y-coordinate of the King.
    - Check if the move is one square forward or backward (i.e., `abs(translationY) == 1` and `translationX == 0`), and set `validMove` to `true` if so.
    - Check if the move is one square sideways (i.e., `abs(translationX) == 1` and `translationY == 0`), and set `validMove` to `true` if so.
    - Check if the move is one square diagonally (i.e., `abs(translationX) == 1` and `abs(translationY) == 1`), and set `validMove` to `true` if so.
    - Return the value of `validMove`.
- **Output**: A boolean value indicating whether the King can legally move to the specified square (`true` if the move is legal, `false` otherwise).
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::display<!-- {{#callable:King::display}} -->
The `display` function outputs the color and type of the King piece to the console.
- **Inputs**: None
- **Control Flow**:
    - The function accesses the `_color` member variable of the `King` class, which indicates the color of the piece.
    - It concatenates the color with the character 'K', representing the King piece.
    - The concatenated string is then output to the console using `cout`.
- **Output**: The function outputs a string to the console, which is the color of the King piece followed by the letter 'K'.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)



