# Purpose
The provided code is a C++ header file (`queen.h`) that defines a class representing a chess queen piece, offering narrow functionality specific to chess game logic. This class, `Queen`, inherits from a base class `Piece`, suggesting a broader chess game framework where different pieces share common characteristics. The header file declares several member functions: a constructor to initialize the queen with a color, a destructor, a method to return the queen's point value, a method to check if a move to a specified square is legal, and a method to display the piece. This file is intended to be included in other parts of a chess application, where the implementation of these methods would be defined, likely in a corresponding `.cpp` file.
# Imports and Dependencies

---
- `iostream`
- `square.h`
- `piece.h`


# Data Structures

---
### Queen<!-- {{#data_structure:Queen}} -->
- **Type**: `class`
- **Description**: The `Queen` class represents a chess queen piece and inherits from the `Piece` class. It encapsulates the behavior and characteristics of a queen in a chess game, including its color, point value, and movement capabilities. The class provides methods to determine the point value of the queen, check if a move to a specific square is legal based on chess rules, and display the queen on the board. The queen can move vertically, horizontally, or diagonally as long as the path is clear, reflecting its powerful and versatile movement in chess.
- **Member Functions**:
    - [`Queen::Queen`](queen.cpp.driver.md#QueenQueen)
    - [`Queen::~Queen`](queen.cpp.driver.md#QueenQueen)
    - [`Queen::value`](queen.cpp.driver.md#Queenvalue)
    - [`Queen::canMoveTo`](queen.cpp.driver.md#QueencanMoveTo)
    - [`Queen::display`](queen.cpp.driver.md#Queendisplay)
- **Inherits from**:
    - [`Piece`](piece.h.driver.md#Piece)


