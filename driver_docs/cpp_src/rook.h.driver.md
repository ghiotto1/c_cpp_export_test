# Purpose
The provided code is a C++ header file, `rook.h`, which defines the interface for a `Rook` class, representing a rook piece in a chess game. This class inherits from `RestrictedPiece`, suggesting that it is part of a larger chess game framework where different types of chess pieces are implemented as subclasses of a more general piece class. The `Rook` class encapsulates the behavior and characteristics specific to a rook, such as its point value and movement capabilities on a chessboard.

The `Rook` class includes several public member functions that define its core functionality. The constructor `Rook(bool isWhite)` initializes a rook with a specified color, while the destructor `~Rook()` handles any necessary cleanup. The `value()` function returns the point value of the rook, which is a standard feature in chess to evaluate the strength of a piece. The `canMoveTo(Square& location)` function determines if a move to a specified square is legal, adhering to the rook's movement rules in chess. Lastly, the `display()` function outputs a representation of the rook, likely for visualization purposes in a console-based or graphical chess application. This header file is intended to be included in other parts of the program where the `Rook` class functionality is required, and it defines a clear public API for interacting with rook objects.
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
- **Inherits from**:
    - [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)


