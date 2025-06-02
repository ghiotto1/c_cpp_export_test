# Purpose
The `king.cpp` file is part of a chess game project, specifically implementing the behavior and characteristics of the King chess piece. This file provides a narrow functionality focused on defining the movement rules and display characteristics of the King piece within the game. The class [`King`](#King::King) inherits from `RestrictedPiece`, indicating that it is a specialized type of chess piece with specific movement restrictions. The constructor initializes the King with a color attribute, and the destructor is defined but does not perform any specific actions.

The most important technical components of this file include the [`canMoveTo`](#King::canMoveTo) method, which encapsulates the logic for determining valid moves for the King piece. This method checks if the King can move one square in any direction—forward, backward, sideways, or diagonally—consistent with the rules of chess. The [`value`](#King::value) method returns a constant value of 0, which might be used in the context of the game to represent the King's value in terms of gameplay strategy. The [`display`](#King::display) method outputs the King's representation on the board, using the color attribute to distinguish between white and black pieces. This file is intended to be part of a larger chess application, likely interacting with other components such as the board and other piece classes.
# Imports and Dependencies

---
- `king.h`


# Data Structures

---
### King<!-- {{#data_structure:King}} -->
- **Description**: [See definition](king.h.driver.md#King)
- **Member Functions**:
    - [`King::King`](#King::King)
    - [`King::~King`](#King::~King)
    - [`King::value`](#King::value)
    - [`King::canMoveTo`](#King::canMoveTo)
    - [`King::display`](#King::display)
- **Inherits from**:
    - `RestrictedPiece`

**Methods**

---
#### King::King<!-- {{#callable:King::King}} -->
The King constructor initializes a King object by calling the constructor of its parent class, RestrictedPiece, with a boolean indicating the piece's color.
- **Inputs**:
    - `isWhite`: A boolean value indicating whether the King piece is white (true) or black (false).
- **Control Flow**:
    - The constructor takes a boolean parameter 'isWhite'.
    - It calls the constructor of the parent class, RestrictedPiece, passing 'isWhite' to it.
- **Output**:
    - There is no return value as this is a constructor for the King class.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::\~King<!-- {{#callable:King::~King}} -->
The destructor for the King class is a default destructor that performs no specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is defined but contains no code, indicating it performs no operations when a King object is destroyed.
- **Output**:
    - There is no output or return value from this destructor.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::value<!-- {{#callable:King::value}} -->
The `value` function returns the point value of the King piece, which is 0.
- **Inputs**:
    - None
- **Control Flow**:
    - The function simply returns the integer value 0.
- **Output**:
    - The function returns an integer value representing the point value of the King piece, which is 0.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::canMoveTo<!-- {{#callable:King::canMoveTo}} -->
The `canMoveTo` function determines if a King chess piece can legally move to a specified square based on standard chess rules for a King's movement.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the King is attempting to move.
- **Control Flow**:
    - Initialize `validMove` to `false` to track if the move is valid.
    - Calculate `translationX` as the difference between the target square's x-coordinate and the King's current x-coordinate.
    - Calculate `translationY` as the difference between the target square's y-coordinate and the King's current y-coordinate.
    - Check if the move is one square forward or backward by verifying if `abs(translationY) == 1` and `translationX == 0`; if true, set `validMove` to `true`.
    - Check if the move is one square sideways by verifying if `abs(translationX) == 1` and `translationY == 0`; if true, set `validMove` to `true`.
    - Check if the move is one square diagonally by verifying if `abs(translationX) == 1` and `abs(translationY) == 1`; if true, set `validMove` to `true`.
    - Return the value of `validMove`, indicating whether the move is valid.
- **Output**:
    - A boolean value indicating whether the King can legally move to the specified square.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)


---
#### King::display<!-- {{#callable:King::display}} -->
The `display` function outputs the color and symbol of the King piece to the console.
- **Inputs**:
    - None
- **Control Flow**:
    - The function uses the `cout` stream to output the color of the King piece followed by the character 'K'.
- **Output**:
    - The function outputs a string to the console, which is the color of the King piece concatenated with the letter 'K'.
- **See also**: [`King`](king.h.driver.md#King)  (Data Structure)



