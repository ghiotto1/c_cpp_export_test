# Purpose
The provided code is a C++ header file, `piece.h`, which defines an abstract class `Piece` representing a game piece, likely for a board game such as chess. This class provides a broad functionality as it serves as a base class for different types of game pieces, encapsulating common attributes and behaviors that all pieces share. The class includes several virtual functions, indicating that it is designed to be subclassed, with derived classes implementing specific behaviors for different types of pieces. Key functionalities include moving a piece to a new square, determining if a move is legal, setting and getting the piece's location, and displaying the piece. The class also provides methods to check the piece's color and whether it is currently on a square.

The `Piece` class interfaces with other components such as `Square`, `Board`, and `Player`, suggesting it is part of a larger game framework. It includes public APIs for interacting with these components, such as `moveTo`, `setLocation`, and `canMoveTo`, which are essential for game logic. The use of pure virtual functions like `value`, `display`, and `canMoveTo` enforces that derived classes must provide specific implementations, allowing for polymorphic behavior. The class also manages internal state with attributes like `_isWhite`, `_color`, and `_square`, which are used to track the piece's color and current position on the board. Overall, this header file is a crucial part of a game engine, providing a flexible and extensible foundation for implementing various game pieces.
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
- **Description**: The `Piece` class represents a generic game piece in a board game, such as chess. It includes attributes to store the piece's color and its current location on the board. The class provides methods to move the piece, check if a move is legal, and determine the piece's value, among other functionalities. It serves as a base class for specific types of pieces, requiring derived classes to implement certain virtual functions like `value`, `display`, and `canMoveTo`. The class ensures that moves are legal and handles capturing opponent pieces while maintaining the integrity of the game state.
- **Member Functions**:
    - [`Piece::Piece`](piece.cpp.driver.md#PiecePiece)
    - [`Piece::~Piece`](piece.cpp.driver.md#PiecePiece)
    - [`Piece::moveTo`](piece.cpp.driver.md#PiecemoveTo)
    - [`Piece::setLocation`](piece.cpp.driver.md#PiecesetLocation)
    - [`Piece::isWhite`](piece.cpp.driver.md#PieceisWhite)
    - [`Piece::color`](piece.cpp.driver.md#Piececolor)
    - [`Piece::isOnSquare`](piece.cpp.driver.md#PieceisOnSquare)
    - [`Piece::location`](piece.cpp.driver.md#Piecelocation)


