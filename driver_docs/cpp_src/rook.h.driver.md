# Purpose
The provided code is a C++ header file (`rook.h`) that defines the interface for a `Rook` class, which represents a rook chess piece. This code offers narrow functionality, specifically tailored to encapsulate the behavior and characteristics of a rook within a chess game. The `Rook` class inherits from a `RestrictedPiece` class, suggesting that it shares common functionality with other restricted chess pieces, likely implementing specific movement rules. The class includes a constructor to initialize the rook's color, a destructor, and several member functions: `value()` to return the rook's point value, `canMoveTo()` to determine if a move to a specified square is legal, and `display()` to output the rook's representation. This header file is intended to be included in other C++ source files where the `Rook` class functionality is required.
# Imports and Dependencies

---
- `iostream`
- `restrictedPiece.h`
- `square.h`


# Data Structures

---
### Rook<!-- {{#data_structure:Rook}} -->
- **Type**: `class`
- **Description**: The `Rook` class represents a chess rook piece and is derived from the `RestrictedPiece` class. It encapsulates the behavior and characteristics of a rook, including its ability to move vertically or horizontally across the board, as determined by the `canMoveTo` method. The class provides a constructor to initialize the rook with a specific color, a destructor, a method to return the point value of the rook (which is 5), and a method to display the rook on the board. The `Rook` class does not have any additional member variables beyond those inherited from `RestrictedPiece`.
- **Member Functions**:
    - [`Rook::Rook`](rook.cpp.driver.md#RookRook)
    - [`Rook::~Rook`](rook.cpp.driver.md#RookRook)
    - [`Rook::value`](rook.cpp.driver.md#Rookvalue)
    - [`Rook::canMoveTo`](rook.cpp.driver.md#RookcanMoveTo)
    - [`Rook::display`](rook.cpp.driver.md#Rookdisplay)
- **Inherits From**:
    - [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)


