# Purpose
The provided code is a C++ header file (`restrictedPiece.h`) that defines a class `RestrictedPiece`, which inherits from a base class `Piece`. This class is designed to represent a chess piece with the additional functionality of tracking whether it has been moved, which is a narrow and specific functionality useful in chess game implementations. The class includes a constructor to initialize the piece with a color, a destructor, a method `moveTo` to attempt moving the piece to a new square, and a method `hasMoved` to check if the piece has been moved previously. The `_moved` attribute is a private member variable used to store the state of whether the piece has been moved. This header file is intended to be included in other C++ source files where the `RestrictedPiece` class functionality is required.
# Imports and Dependencies

---
- `piece.h`


# Data Structures

---
### RestrictedPiece<!-- {{#data_structure:RestrictedPiece}} -->
- **Type**: `class`
- **Members**:
    - `_moved`: A boolean attribute that indicates whether the piece has been moved.
- **Description**: The `RestrictedPiece` class is a specialized type of chess piece that extends the `Piece` class, adding functionality to track whether the piece has been moved. This is achieved through a private boolean attribute `_moved`, which is initially set to `false` and updated to `true` upon a successful move. The class provides methods to move the piece and check if it has been moved, thus allowing for game logic that depends on whether a piece has been moved, such as castling in chess.
- **Member Functions**:
    - [`RestrictedPiece::RestrictedPiece`](restrictedPiece.cpp.driver.md#RestrictedPiece::RestrictedPiece)
    - [`RestrictedPiece::~RestrictedPiece`](restrictedPiece.cpp.driver.md#RestrictedPiece::~RestrictedPiece)
    - [`RestrictedPiece::moveTo`](restrictedPiece.cpp.driver.md#RestrictedPiece::moveTo)
    - [`RestrictedPiece::hasMoved`](restrictedPiece.cpp.driver.md#RestrictedPiece::hasMoved)
- **Inherits from**:
    - [`Piece`](piece.h.driver.md#Piece)


