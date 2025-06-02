# Purpose
The provided code is a C++ header file, `king.h`, which defines a class representing a chess king piece. This class, `King`, inherits from a base class `RestrictedPiece`, suggesting that it is part of a larger chess game application where different types of chess pieces are modeled. The `King` class encapsulates the behavior and characteristics specific to a king piece in chess, such as its ability to move and its point value. The class provides a constructor to initialize a king piece with a specified color, a destructor, and several member functions that define its functionality.

The `King` class includes methods such as `value()`, which returns the point value of the king piece, and `canMoveTo(Square& location)`, which determines if the king can legally move to a specified square on the chessboard. Additionally, the `display()` method is provided to output the representation of the king piece, likely for visualization purposes in the game. This header file is intended to be included in other parts of the application, where the functionality of the king piece is required, and it defines a public API for interacting with king objects within the chess game.
# Imports and Dependencies

---
- `iostream`
- `restrictedPiece.h`


# Data Structures

---
### King<!-- {{#data_structure:King}} -->
- **Type**: `class`
- **Description**: The `King` class represents a chess king piece and inherits from the `RestrictedPiece` class. It includes a constructor to initialize the king with a specified color, a destructor, and several member functions. The `value` function returns the point value of the king, which is set to 0 in this implementation. The `canMoveTo` function determines if the king can legally move to a specified square, allowing moves one square in any direction (forward, backward, sideways, or diagonally). The `display` function outputs the king's representation, which includes its color and the letter 'K'.
- **Member Functions**:
    - [`King::King`](king.cpp.driver.md#King::King)
    - [`King::~King`](king.cpp.driver.md#King::~King)
    - [`King::value`](king.cpp.driver.md#King::value)
    - [`King::canMoveTo`](king.cpp.driver.md#King::canMoveTo)
    - [`King::display`](king.cpp.driver.md#King::display)
- **Inherits from**:
    - [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)


