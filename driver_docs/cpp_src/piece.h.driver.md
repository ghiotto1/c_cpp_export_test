# Purpose
The provided code is a C++ header file, `piece.h`, which defines an abstract class `Piece` representing a game piece, likely for a board game such as chess. This class provides a broad set of functionalities related to the management and behavior of game pieces, including movement, color determination, and location management. The class is designed to be extended, as indicated by the presence of pure virtual functions like `value()`, `display()`, and `canMoveTo()`, which must be implemented by derived classes. This design allows for the creation of specific types of pieces with unique behaviors and characteristics.

The `Piece` class includes several important technical components. It maintains attributes such as `_isWhite` to determine the piece's color and `_square` to track its current location on the board. The class provides public methods for moving the piece (`moveTo`), setting and getting its location (`setLocation`, `location`), and checking its color (`isWhite`, `color`). The inclusion of the `Player`, `Square`, and `Board` classes, as well as the use of the `ostream` library, suggests that this class is part of a larger game framework. The header file defines a public API for interacting with game pieces, making it a crucial component for any game logic that involves piece movement and interaction on a board.
# Imports and Dependencies

---
- `ostream`
- `square.h`
- `board.h`


# Data Structures

---
### Piece<!-- {{#data_structure:Piece}} -->
- **Type**: `class`
- **Members**:
    - `_isWhite`: A boolean indicating if the piece is white.
    - `_color`: A string representing the color of the piece, either 'W' for white or 'B' for black.
    - `_square`: A pointer to the Square object where the piece is currently located.
- **Description**: The `Piece` class represents a game piece in a board game, such as chess. It includes attributes to determine the piece's color and its current location on the board. The class provides methods to move the piece, check if a move is legal, and determine the piece's value, among other functionalities. It serves as a base class for specific types of pieces, requiring derived classes to implement certain virtual functions like `value`, `display`, and `canMoveTo`. The class ensures that moves are legal and handles capturing of opponent pieces, while also checking if a move results in a player's king being in check.
- **Member Functions**:
    - [`Piece::Piece`](piece.cpp.driver.md#PiecePiece)
    - [`Piece::~Piece`](piece.cpp.driver.md#PiecePiece)
    - [`Piece::moveTo`](piece.cpp.driver.md#PiecemoveTo)
    - [`Piece::setLocation`](piece.cpp.driver.md#PiecesetLocation)
    - [`Piece::isWhite`](piece.cpp.driver.md#PieceisWhite)
    - [`Piece::color`](piece.cpp.driver.md#Piececolor)
    - [`Piece::isOnSquare`](piece.cpp.driver.md#PieceisOnSquare)
    - [`Piece::location`](piece.cpp.driver.md#Piecelocation)


