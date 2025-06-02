# Purpose
The provided C++ source code file, `knight.cpp`, is part of a larger project, likely a chess game, as indicated by the file name and the project name `ChessProject`. This file specifically implements the behavior of the Knight piece in a chess game. It defines the [`Knight`](#KnightKnight) class, which inherits from a base class `Piece`, suggesting a class hierarchy where different chess pieces share common functionality. The [`Knight`](#KnightKnight) class constructor initializes the piece with a color, and the destructor is defined but does not perform any specific actions, which is typical when no dynamic memory or resources need to be released.

The [`Knight`](#KnightKnight) class provides several key functionalities. The `value()` method returns the integer value `3`, which is a common convention in chess programming to represent the relative strength of a Knight. The `canMoveTo(Square& location)` method implements the unique movement logic of the Knight, which can move in an "L" shape: two squares in one direction and one square perpendicular, or vice versa. This method checks the validity of a move based on these rules. The `display()` method outputs the Knight's representation, which includes its color and the letter "N", typically used to denote a Knight in chess notation. This file is likely part of a broader collection of files, each implementing different chess pieces, and it does not define a public API or external interface, as it is intended to be used internally within the chess game application.
# Imports and Dependencies

---
- `knight.h`


# Data Structures

---
### Knight<!-- {{#data_structure:Knight}} -->
- **Description**: [See definition](knight.h.driver.md#Knight)
- **Member Functions**:
    - [`Knight::Knight`](#KnightKnight)
    - [`Knight::~Knight`](#KnightKnight)
    - [`Knight::value`](#Knightvalue)
    - [`Knight::canMoveTo`](#KnightcanMoveTo)
    - [`Knight::display`](#Knightdisplay)
- **Inherits from**:
    - `Piece`

**Methods**

---
#### Knight::Knight<!-- {{#callable:Knight::Knight}} -->
The `Knight` constructor initializes a `Knight` object by calling the `Piece` constructor with a boolean indicating the piece's color.
- **Inputs**:
    - `isWhite`: A boolean value indicating whether the knight is white (true) or black (false).
- **Control Flow**:
    - The constructor `Knight::Knight(bool isWhite)` is called with a boolean parameter `isWhite`.
    - The constructor initializes the `Knight` object by invoking the constructor of its base class `Piece` with the `isWhite` parameter.
- **Output**:
    - There is no return value as this is a constructor for initializing a `Knight` object.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::\~Knight<!-- {{#callable:Knight::~Knight}} -->
The destructor for the Knight class is a default destructor that performs no specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is defined but contains no code, indicating it performs no operations when a Knight object is destroyed.
- **Output**:
    - There is no output or return value from this destructor.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::value<!-- {{#callable:Knight::value}} -->
The `value` function returns the fixed point value of a Knight piece in chess.
- **Inputs**:
    - None
- **Control Flow**:
    - The function directly returns the integer value 3, representing the point value of a Knight in chess.
- **Output**:
    - The function returns an integer value of 3, which is the standard point value assigned to a Knight in chess.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::canMoveTo<!-- {{#callable:Knight::canMoveTo}} -->
The `canMoveTo` function determines if a Knight piece can legally move to a specified square based on chess movement rules for a Knight.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the Knight is attempting to move.
- **Control Flow**:
    - Initialize `validMove` to `false`.
    - Calculate `translationX` as the difference between the target square's x-coordinate and the Knight's current x-coordinate.
    - Calculate `translationY` as the difference between the target square's y-coordinate and the Knight's current y-coordinate.
    - Check if the move is valid by verifying if the absolute values of `translationY` and `translationX` match the Knight's L-shaped movement pattern (1 square in one direction and 2 squares in the perpendicular direction).
    - If either of the conditions for a valid Knight move is met, set `validMove` to `true`.
    - Return the value of `validMove`.
- **Output**:
    - A boolean value indicating whether the Knight can legally move to the specified square.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::display<!-- {{#callable:Knight::display}} -->
The `display` function outputs the color and type of the Knight piece to the console.
- **Inputs**:
    - None
- **Control Flow**:
    - The function accesses the `_color` attribute of the Knight object, which indicates the color of the piece (e.g., 'W' for white or 'B' for black).
    - It concatenates the color with the character 'N', which represents the Knight piece in chess notation.
    - The concatenated string is then output to the console using `cout`.
- **Output**:
    - The function outputs a string to the console that represents the Knight piece, including its color and type.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)



