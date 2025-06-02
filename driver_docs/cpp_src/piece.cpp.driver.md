# Purpose
The provided C++ source file, `piece.cpp`, is part of a larger chess application, as indicated by its inclusion in the "ChessProject". This file implements the [`Piece`](#PiecePiece) class, which represents a chess piece in the game. The class provides functionality to manage the piece's color, location, and movement on the chessboard. The constructor initializes the piece's color based on whether it is white or black, and the destructor is defined but does not perform any specific actions. The [`moveTo`](#PiecemoveTo) method is a critical component of this class, handling the logic for moving a piece from one square to another, including capturing opponent pieces and ensuring that moves do not leave the player's king in check. This method encapsulates the rules of chess regarding piece movement and captures, making it a central part of the game's mechanics.

The [`Piece`](#PiecePiece) class also includes several utility methods, such as [`setLocation`](#PiecesetLocation), [`isWhite`](#PieceisWhite), [`color`](#Piececolor), [`isOnSquare`](#PieceisOnSquare), and [`location`](#Piecelocation), which provide access to the piece's attributes and state. These methods facilitate interaction with the piece's properties, such as determining its color, checking its current position, and updating its location on the board. The file imports two headers, `piece.h` and `player.h`, suggesting that it relies on definitions from these files, likely for the [`Piece`](#PiecePiece) and `Player` classes, respectively. Overall, `piece.cpp` is a focused implementation that provides essential functionality for managing chess pieces within the broader context of a chess game application.
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
    - A conditional check is performed on `isWhite` to set the `_color` member variable to "W" if `isWhite` is true, otherwise to "B".
- **Output**:
    - The constructor does not return a value as it is used to initialize an object of the `Piece` class.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::\~Piece<!-- {{#callable:Piece::~Piece}} -->
The destructor for the `Piece` class is a default destructor that performs no specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is called when a `Piece` object is destroyed.
    - No specific actions or resource deallocations are performed within the destructor.
- **Output**:
    - There is no output or return value from the destructor.
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
    - Verify if the piece can move to the target square using the `canMoveTo` method.
    - If the target square is occupied, check if the occupying piece can be captured (i.e., it is of a different color).
    - If the move is valid, tentatively move the piece by updating the square occupancies and check if the move leaves the player's king in check.
    - If the move results in the king being in check, revert the move and restore the original state.
    - If the move does not leave the king in check, finalize the move and capture the opponent's piece if applicable.
    - Return `validMove` indicating whether the move was successfully executed.
- **Output**:
    - A boolean value indicating whether the move was valid and successfully executed.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::setLocation<!-- {{#callable:Piece::setLocation}} -->
The `setLocation` function assigns a new square location to a chess piece.
- **Inputs**:
    - `location`: A pointer to a `Square` object representing the new location for the piece.
- **Control Flow**:
    - The function takes a pointer to a `Square` object as an argument.
    - It assigns this pointer to the private member variable `_square`, effectively updating the piece's current location.
- **Output**:
    - The function does not return any value.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::isWhite<!-- {{#callable:Piece::isWhite}} -->
The `isWhite` function checks if a chess piece is white.
- **Inputs**:
    - None
- **Control Flow**:
    - The function directly returns the value of the private member variable `_isWhite`.
- **Output**:
    - A boolean value indicating whether the piece is white (`true`) or not (`false`).
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::color<!-- {{#callable:Piece::color}} -->
The `color` function returns the color of a chess piece as a string.
- **Inputs**:
    - None
- **Control Flow**:
    - The function simply returns the value of the private member variable `_color`.
- **Output**:
    - The function returns a `string` representing the color of the piece, which is either "W" for white or "B" for black.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::isOnSquare<!-- {{#callable:Piece::isOnSquare}} -->
The `isOnSquare` function checks if a chess piece is currently located on a square.
- **Inputs**:
    - None
- **Control Flow**:
    - The function returns the value of the private member variable `_square`.
- **Output**:
    - A boolean value indicating whether the piece is on a square (true if `_square` is not null, false otherwise).
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)


---
#### Piece::location<!-- {{#callable:Piece::location}} -->
The `location` function returns the current square on which the piece is located.
- **Inputs**:
    - None
- **Control Flow**:
    - The function directly returns the private member variable `_square`.
- **Output**:
    - A pointer to a `Square` object representing the current location of the piece.
- **See also**: [`Piece`](piece.h.driver.md#Piece)  (Data Structure)



