# Purpose
The provided C++ source code file, `rook.cpp`, is part of a larger chess application, as indicated by its inclusion in the "ChessProject". This file specifically implements the behavior and characteristics of the Rook chess piece. The class [`Rook`](#Rook::Rook) inherits from a base class `RestrictedPiece`, which likely encapsulates common functionality for chess pieces with restricted movement patterns. The constructor initializes the Rook with a color, indicating whether it is a white or black piece, and the destructor is defined but does not perform any specific actions, suggesting that no special cleanup is required for this class.

The [`Rook`](#Rook::Rook) class defines several key methods that encapsulate its functionality. The `value()` method returns an integer value of 5, which is a common convention in chess programming to represent the relative strength of a Rook compared to other pieces. The `canMoveTo()` method determines if the Rook can legally move to a specified `Square` on the chessboard, checking for clear paths either vertically or horizontally, which aligns with the Rook's movement rules in chess. The `display()` method outputs the Rook's representation, which includes its color and the letter "R", to the console. This file is not a standalone executable but rather a component of a larger system, likely intended to be used in conjunction with other chess piece classes and a chessboard management system.
# Imports and Dependencies

---
- `rook.h`


# Data Structures

---
### Rook<!-- {{#data_structure:Rook}} -->
- **Description**: [See definition](rook.h.driver.md#Rook)
- **Member Functions**:
    - [`Rook::Rook`](#Rook::Rook)
    - [`Rook::~Rook`](#Rook::~Rook)
    - [`Rook::value`](#Rook::value)
    - [`Rook::canMoveTo`](#Rook::canMoveTo)
    - [`Rook::display`](#Rook::display)
- **Inherits from**:
    - `RestrictedPiece`

**Methods**

---
#### Rook::Rook<!-- {{#callable:Rook::Rook}} -->
The Rook constructor initializes a Rook object by calling the constructor of its parent class, RestrictedPiece, with a boolean indicating the piece's color.
- **Inputs**:
    - `isWhite`: A boolean value indicating whether the Rook is white (true) or black (false).
- **Control Flow**:
    - The constructor of the Rook class is called with a boolean parameter 'isWhite'.
    - The constructor of the parent class, RestrictedPiece, is invoked with the 'isWhite' parameter to initialize the Rook object.
- **Output**:
    - There is no output from this constructor function as it is used to initialize an object of the Rook class.
- **See also**: [`Rook`](rook.h.driver.md#Rook)  (Data Structure)


---
#### Rook::\~Rook<!-- {{#callable:Rook::~Rook}} -->
The destructor for the Rook class is a default destructor that performs no specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is called when a Rook object is destroyed.
    - No specific actions or resource deallocations are performed within the destructor.
- **Output**:
    - There is no output or return value from the destructor.
- **See also**: [`Rook`](rook.h.driver.md#Rook)  (Data Structure)


---
#### Rook::value<!-- {{#callable:Rook::value}} -->
The `value` function returns the point value of a Rook piece in a chess game.
- **Inputs**:
    - None
- **Control Flow**:
    - The function is a simple getter that directly returns the integer value 5, representing the point value of a Rook in chess.
- **Output**:
    - The function returns an integer value of 5, which is the standard point value assigned to a Rook in chess.
- **See also**: [`Rook`](rook.h.driver.md#Rook)  (Data Structure)


---
#### Rook::canMoveTo<!-- {{#callable:Rook::canMoveTo}} -->
The `canMoveTo` function determines if a Rook can legally move to a specified square on a chessboard by checking for clear vertical or horizontal paths.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the Rook is attempting to move.
- **Control Flow**:
    - Initialize a boolean variable `validMove` to `false`.
    - Check if the path from the Rook's current location to the target location is clear vertically using `Board::getBoard()->isClearVertical`.
    - If the vertical path is clear, set `validMove` to `true`.
    - If the vertical path is not clear, check if the path is clear horizontally using `Board::getBoard()->isClearHorizontal`.
    - If the horizontal path is clear, set `validMove` to `true`.
    - Return the value of `validMove`.
- **Output**:
    - Returns a boolean value indicating whether the Rook can legally move to the specified square, based on clear vertical or horizontal paths.
- **See also**: [`Rook`](rook.h.driver.md#Rook)  (Data Structure)


---
#### Rook::display<!-- {{#callable:Rook::display}} -->
The `display` function outputs the color and type of the Rook piece to the console.
- **Inputs**:
    - None
- **Control Flow**:
    - The function uses the `cout` stream to output the Rook's color followed by the letter 'R'.
- **Output**:
    - The function does not return any value; it outputs directly to the console.
- **See also**: [`Rook`](rook.h.driver.md#Rook)  (Data Structure)



