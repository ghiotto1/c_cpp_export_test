# Purpose
The `restrictedPiece.cpp` file is part of a larger chess application, as indicated by its inclusion in the "ChessProject." This file defines the implementation of the [`RestrictedPiece`](#RestrictedPieceRestrictedPiece) class, which inherits from a base class `Piece`. The primary purpose of this class is to represent a chess piece with movement restrictions, specifically tracking whether the piece has moved from its initial position. This functionality is crucial for implementing chess rules that depend on a piece's movement history, such as castling for rooks and pawns' initial double-step move.

The file includes two header files, `player.h` and `restrictedPiece.h`, suggesting that it interacts with player-related functionality and defines its own interface in `restrictedPiece.h`. The class constructor initializes the piece's color and sets a private member `_moved` to `false`, indicating that the piece has not yet moved. The [`moveTo`](#RestrictedPiecemoveTo) method overrides a similar method in the base class to update the `_moved` status only if a valid move is executed and the piece has not moved before. The [`hasMoved`](#RestrictedPiecehasMoved) method provides a public interface to check the movement status of the piece. This file is a focused implementation, providing specific functionality related to movement restrictions within the broader context of a chess game.
# Imports and Dependencies

---
- `player.h`
- `restrictedPiece.h`


# Data Structures

---
### RestrictedPiece<!-- {{#data_structure:RestrictedPiece}} -->
- **Description**: [See definition](restrictedPiece.h.driver.md#RestrictedPiece)
- **Member Functions**:
    - [`RestrictedPiece::RestrictedPiece`](#RestrictedPieceRestrictedPiece)
    - [`RestrictedPiece::~RestrictedPiece`](#RestrictedPieceRestrictedPiece)
    - [`RestrictedPiece::moveTo`](#RestrictedPiecemoveTo)
    - [`RestrictedPiece::hasMoved`](#RestrictedPiecehasMoved)
- **Inherits from**:
    - `Piece`

**Methods**

---
#### RestrictedPiece::RestrictedPiece<!-- {{#callable:RestrictedPiece::RestrictedPiece}} -->
The `RestrictedPiece` constructor initializes a chess piece with a specified color and sets its moved status to false.
- **Inputs**:
    - `isWhite`: A boolean indicating whether the piece is white (true) or black (false).
- **Control Flow**:
    - The constructor initializes the base class `Piece` with the `isWhite` parameter to set the color of the piece.
    - It sets the private member variable `_moved` to `false`, indicating that the piece has not been moved yet.
- **Output**:
    - There is no return value as this is a constructor for the `RestrictedPiece` class.
- **See also**: [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)  (Data Structure)


---
#### RestrictedPiece::\~RestrictedPiece<!-- {{#callable:RestrictedPiece::~RestrictedPiece}} -->
The destructor for the RestrictedPiece class performs no specific actions upon object destruction.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is defined but contains no code, indicating no special cleanup or resource management is needed for this class.
- **Output**:
    - There is no output or return value from a destructor.
- **See also**: [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)  (Data Structure)


---
#### RestrictedPiece::moveTo<!-- {{#callable:RestrictedPiece::moveTo}} -->
The `moveTo` function attempts to move a `RestrictedPiece` to a specified square and updates its moved status if the move is valid and the piece hasn't been moved before.
- **Inputs**:
    - `byPlayer`: A reference to the `Player` object attempting to move the piece.
    - `to`: A reference to the `Square` object representing the destination square for the move.
- **Control Flow**:
    - Call the `moveTo` method of the base class `Piece` to determine if the move is valid, storing the result in `validMove`.
    - Check if `validMove` is true and the `_moved` attribute is false, indicating a valid move and that the piece hasn't been moved before.
    - If both conditions are met, set `_moved` to true to indicate the piece has been moved.
    - Return the value of `validMove` to indicate whether the move was successful.
- **Output**:
    - A boolean value indicating whether the move was successful.
- **See also**: [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)  (Data Structure)


---
#### RestrictedPiece::hasMoved<!-- {{#callable:RestrictedPiece::hasMoved}} -->
The `hasMoved` function checks if a `RestrictedPiece` has been moved from its initial position.
- **Inputs**:
    - None
- **Control Flow**:
    - The function simply returns the value of the private member variable `_moved`.
- **Output**:
    - A boolean value indicating whether the `RestrictedPiece` has been moved (`true`) or not (`false`).
- **See also**: [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)  (Data Structure)



