# Purpose
The provided C++ source file, `piece.cpp`, is part of a larger chess application, likely named "ChessProject". This file implements the [`Piece`](#PiecePiece) class, which represents a chess piece in the game. The class provides functionality to manage the state and behavior of a chess piece, including its color, current location on the board, and the ability to move to a new square. The [`Piece`](#PiecePiece) class constructor initializes the piece's color based on whether it is white or black, and the destructor is defined but does not perform any specific actions.

The core functionality of the [`Piece`](#PiecePiece) class is encapsulated in the [`moveTo`](#PiecemoveTo) method, which handles the logic for moving a piece from its current square to a target square. This method checks if the move is valid by ensuring it is performed by the correct player, adheres to the piece's movement rules, and does not leave the player's king in check. The method also manages capturing opponent pieces and updating the board state accordingly. Additional methods such as [`setLocation`](#PiecesetLocation), [`isWhite`](#PieceisWhite), [`color`](#Piececolor), [`isOnSquare`](#PieceisOnSquare), and [`location`](#Piecelocation) provide access to the piece's attributes and current state. This file is a crucial component of the chess application, focusing on the individual behavior and rules governing chess pieces.
# Imports and Dependencies

---
- `string`
- `piece.h`
- `player.h`


# Data Structures

---
### Piece<!-- {{#data_structure:Piece}} -->
- **Description**: [See definition](piece.h.driver.md#Piece)
- **Member Functions**:
    - [`Piece::Piece`](#PiecePiece)
    - [`Piece::~Piece`](#PiecePiece)
    - [`Piece::moveTo`](#PiecemoveTo)
    - [`Piece::setLocation`](#PiecesetLocation)
    - [`Piece::isWhite`](#PieceisWhite)
    - [`Piece::color`](#Piececolor)
    - [`Piece::isOnSquare`](#PieceisOnSquare)
    - [`Piece::location`](#Piecelocation)

**Methods**

---
#### Piece::Piece<!-- {{#callable:Piece::Piece}} -->
The `Piece` constructor initializes a chess piece with a specified color and sets its initial square to null.
- **Inputs**:
    - `isWhite`: A boolean indicating whether the piece is white (true) or black (false).
- **Control Flow**:
    - The constructor initializes the `_isWhite` member variable with the value of `isWhite`.
    - The `_square` member variable is initialized to `NULL`, indicating that the piece is not on any square initially.
    - A conditional check is performed on `isWhite` to set the `_color` member variable to "W" if `isWhite` is true, or "B" if false.
- **Output**: The constructor does not return a value as it is used to initialize an object of the `Piece` class.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::\~Piece<!-- {{#callable:Piece::~Piece}} -->
The `Piece::~Piece()` function is the default destructor for the `Piece` class, which currently performs no specific actions upon object destruction.
- **Inputs**: None
- **Control Flow**:
    - The destructor is called when a `Piece` object goes out of scope or is explicitly deleted.
    - Currently, the destructor does not contain any code, so it performs no operations.
- **Output**: There is no output from this destructor as it performs no actions.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::moveTo<!-- {{#callable:Piece::moveTo}} -->
The `moveTo` function attempts to move a chess piece to a specified square, ensuring the move is legal according to chess rules and does not leave the player's king in check.
- **Inputs**:
    - `byPlayer`: A reference to the Player object attempting to move the piece, used to verify the move's legality and color.
    - `toSquare`: A reference to the Square object representing the destination square for the piece.
- **Control Flow**:
    - Initialize `validMove` to false and `toCapture` to NULL, and store the current square in `fromSquare`.
    - Check if the piece is being moved by its owner by comparing the piece's color with the player's color.
    - Verify if the piece can legally move to the target square using `canMoveTo`.
    - If the target square is occupied, check if the occupying piece can be captured (i.e., it is of the opposite color).
    - If the move is valid, tentatively move the piece to the target square and update the square's occupier.
    - Check if the move leaves the player's king in check using `byPlayer.inCheck()`.
    - If the move results in a check, undo the move and restore the original state.
    - If the move does not result in a check, finalize the move and capture the opponent's piece if applicable.
- **Output**: Returns a boolean indicating whether the move was valid and successfully executed.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::setLocation<!-- {{#callable:Piece::setLocation}} -->
The `setLocation` function assigns a new square location to a chess piece.
- **Inputs**:
    - `location`: A pointer to a `Square` object representing the new location for the piece.
- **Control Flow**:
    - The function assigns the provided `Square` pointer to the private member variable `_square`, effectively updating the piece's current location.
- **Output**: This function does not return any value.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::isWhite<!-- {{#callable:Piece::isWhite}} -->
The `isWhite` function checks if a chess piece is white.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `_isWhite`.
- **Output**: A boolean value indicating whether the piece is white (`true`) or not (`false`).
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::color<!-- {{#callable:Piece::color}} -->
The `color` function returns the color of the chess piece as a string.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `_color`.
- **Output**: A string representing the color of the piece, either "W" for white or "B" for black.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::isOnSquare<!-- {{#callable:Piece::isOnSquare}} -->
The `isOnSquare` function checks if a chess piece is currently located on a square.
- **Inputs**: None
- **Control Flow**:
    - The function simply returns the value of the private member variable `_square`.
- **Output**: A boolean value indicating whether the piece is on a square (true if `_square` is not null, false otherwise).
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::location<!-- {{#callable:Piece::location}} -->
The `location` function returns the current square on which the piece is located.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the private member variable `_square`.
- **Output**: A pointer to a `Square` object representing the current location of the piece.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)



