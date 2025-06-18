# Purpose
The provided code is a C++ header file (`restrictedPiece.h`) that defines a class `RestrictedPiece`, which inherits from a base class `Piece`. This class is designed to represent a chess piece with the additional functionality of tracking whether it has been moved. The functionality is relatively narrow, focusing specifically on the movement state of a chess piece. The class includes a constructor to initialize the piece with a color, a destructor, a method `moveTo` to attempt moving the piece to a new square, and a method `hasMoved` to check if the piece has been moved previously. The private attribute `_moved` is used to store the movement state of the piece. This header file is intended to be included in other C++ files where the `RestrictedPiece` class functionality is required.
# Imports and Dependencies

---
- `piece.h`


# Data Structures

---
### RestrictedPiece<!-- {{#data_structure:RestrictedPiece}} -->
- **Type**: `class`
- **Members**:
    - `_moved`: A boolean attribute that indicates whether the piece has been moved.
- **Description**: The `RestrictedPiece` class is a specialized type of chess piece that extends the `Piece` class, adding functionality to track whether the piece has been moved. It includes a private boolean attribute `_moved` to store this state. The class provides a constructor to initialize the piece with a color, a destructor, and methods to move the piece and check if it has been moved. The `moveTo` method updates the `_moved` attribute only if a valid move is made and the piece has not been moved before, ensuring that the state accurately reflects the piece's movement history.
- **Member Functions**:
    - [`RestrictedPiece::RestrictedPiece`](restrictedPiece.cpp.driver.md#RestrictedPieceRestrictedPiece)
    - [`RestrictedPiece::~RestrictedPiece`](restrictedPiece.cpp.driver.md#RestrictedPieceRestrictedPiece)
    - [`RestrictedPiece::moveTo`](restrictedPiece.cpp.driver.md#RestrictedPiecemoveTo)
    - [`RestrictedPiece::hasMoved`](restrictedPiece.cpp.driver.md#RestrictedPiecehasMoved)
- **Inherits From**:
    - `Piece`


