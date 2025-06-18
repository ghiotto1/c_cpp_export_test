# Purpose
The provided C++ source code file, `pawn.cpp`, is part of a chess game implementation, specifically handling the behavior and rules associated with the pawn piece. This file defines the [`Pawn`](#PawnPawn) class, which inherits from a `RestrictedPiece` class, indicating that it has specific movement constraints. The [`Pawn`](#PawnPawn) class encapsulates the logic for pawn-specific actions, such as moving forward, capturing diagonally, and promoting to a queen upon reaching the opponent's end of the board. The class uses a delegate pattern to handle the promotion of a pawn to a queen, dynamically switching its behavior to that of a `Queen` object when necessary.

The [`Pawn`](#PawnPawn) class provides several key methods: [`setLocation`](#PawnsetLocation) to update the pawn's position, [`value`](#Pawnvalue) to return the pawn's point value, [`moveTo`](#PawnmoveTo) to execute a move and handle promotion, and [`canMoveTo`](#PawncanMoveTo) to validate potential moves based on chess rules. The [`display`](#Pawndisplay) method outputs the pawn's representation, which changes if it has been promoted. The code is designed to be part of a larger chess application, interacting with other components like `Square`, `Player`, and `Board`. It does not define a public API but rather serves as an internal component of the chess game logic, focusing on the pawn's unique movement and promotion rules.
# Imports and Dependencies

---
- `pawn.h`
- `queen.h`
- `board.h`


# Data Structures

---
### Pawn<!-- {{#data_structure:Pawn}} -->
- **Description**: [See definition](pawn.h.driver.md#Pawn)
- **Member Functions**:
    - [`Pawn::Pawn`](#PawnPawn)
    - [`Pawn::~Pawn`](#PawnPawn)
    - [`Pawn::setLocation`](#PawnsetLocation)
    - [`Pawn::value`](#Pawnvalue)
    - [`Pawn::moveTo`](#PawnmoveTo)
    - [`Pawn::canMoveTo`](#PawncanMoveTo)
    - [`Pawn::display`](#Pawndisplay)
- **Inherits From**:
    - `RestrictedPiece`

**Methods**

---
#### Pawn::Pawn<!-- {{#callable:Pawn::Pawn}} -->
The `Pawn` constructor initializes a `Pawn` object with a specified color and sets its delegate to NULL.
- **Inputs**:
    - `isWhite`: A boolean indicating whether the pawn is white (true) or black (false).
- **Control Flow**:
    - The constructor initializes the `Pawn` object by calling the constructor of its superclass `RestrictedPiece` with the `isWhite` parameter.
    - It sets the private member `_delegate` to NULL, indicating that the pawn has not been promoted to another piece.
- **Output**: A `Pawn` object is created with the specified color and no delegate piece.
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)


---
#### Pawn::\~Pawn<!-- {{#callable:Pawn::~Pawn}} -->
The destructor for the `Pawn` class deallocates memory for the `_delegate` member if it is not null.
- **Inputs**: None
- **Control Flow**:
    - Check if the `_delegate` pointer is not null.
    - If `_delegate` is not null, delete the memory allocated for `_delegate`.
- **Output**: The destructor does not return any value.
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)


---
#### Pawn::setLocation<!-- {{#callable:Pawn::setLocation}} -->
The `setLocation` function sets the location of a `Pawn` object by calling the `setLocation` method of its base class `Piece`.
- **Inputs**:
    - `location`: A pointer to a `Square` object representing the new location for the `Pawn`.
- **Control Flow**:
    - The function takes a `Square*` as an argument, which represents the new location for the `Pawn`.
    - It calls the `setLocation` method of the base class `Piece` with the provided `location` argument.
- **Output**: The function does not return any value.
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)


---
#### Pawn::value<!-- {{#callable:Pawn::value}} -->
The `value` function returns the point value of a Pawn piece in a chess game.
- **Inputs**: None
- **Control Flow**:
    - The function is a simple getter that returns a constant integer value.
    - There are no conditional statements or loops; it directly returns the integer 1.
- **Output**: The function returns an integer value of 1, representing the point value of a Pawn in chess.
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)


---
#### Pawn::moveTo<!-- {{#callable:Pawn::moveTo}} -->
The `moveTo` function attempts to move a pawn to a specified square, handling both normal pawn movement and promotion to a queen if applicable.
- **Inputs**:
    - `byPlayer`: A reference to the Player object attempting to move the pawn.
    - `to`: A reference to the Square object representing the destination square for the pawn.
- **Control Flow**:
    - Initialize a boolean variable `valid` to false to track the validity of the move.
    - Check if the pawn has been promoted by verifying if `_delegate` is not null.
    - If promoted, use the delegate piece's `moveTo` method to determine move validity.
    - If the move is valid, update the pawn's current and new square occupiers and set the new location.
    - If not promoted, use the `RestrictedPiece`'s `moveTo` method to attempt a normal pawn move.
    - If the move is valid and the pawn reaches the opponent's end row, promote the pawn to a queen by creating a new `Queen` object and setting it as the delegate.
    - Return the boolean `valid` indicating whether the move was successful.
- **Output**: A boolean value indicating whether the move was successful.
- **Functions called**:
    - [`Pawn::setLocation`](#PawnsetLocation)
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)


---
#### Pawn::canMoveTo<!-- {{#callable:Pawn::canMoveTo}} -->
The `canMoveTo` function determines if a pawn can legally move to a specified square based on its current position, movement rules, and whether it has been promoted.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the pawn is attempting to move.
- **Control Flow**:
    - Initialize `validMove` to false and calculate `translationX` and `translationY` as the differences in x and y coordinates between the target location and the pawn's current location.
    - Check if the pawn has been promoted (i.e., has a delegate piece); if so, use the delegate's `canMoveTo` method to determine move validity.
    - If the pawn is not promoted, adjust `translationX` and `translationY` for black pieces to account for their movement direction being opposite to white pieces.
    - Check if the move is a valid one-square forward move to an unoccupied square and set `validMove` to true if so.
    - Check if the move is a valid two-square forward move from the starting position to an unoccupied square along a clear vertical path and set `validMove` to true if so.
    - Check if the move is a valid capture move to an occupied square on an adjacent diagonal and set `validMove` to true if so.
    - Return the value of `validMove`.
- **Output**: A boolean value indicating whether the pawn can legally move to the specified square.
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)


---
#### Pawn::display<!-- {{#callable:Pawn::display}} -->
The `display` function outputs the visual representation of a `Pawn` object, either by delegating to another piece or displaying its own symbol.
- **Inputs**: None
- **Control Flow**:
    - Check if the `_delegate` pointer is not null.
    - If `_delegate` is not null, call the `display` method on the `_delegate` object.
    - If `_delegate` is null, output the pawn's color followed by the letter 'P' to represent the pawn.
- **Output**: The function outputs the pawn's representation to the standard output stream.
- **See also**: [`Pawn`](pawn.h.driver.md#Pawn)  (Data Structure)



