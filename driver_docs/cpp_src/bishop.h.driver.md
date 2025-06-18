# Purpose
The provided code is a C++ header file, `bishop.h`, which defines a class representing a chess bishop piece. This class, `Bishop`, inherits from a base class `Piece`, suggesting a broader chess game application where different chess pieces are modeled as classes. The functionality of this code is relatively narrow, focusing specifically on the behavior and characteristics of a bishop in a chess game. It includes methods for creating a bishop with a specified color, determining its point value, checking if a move to a given square is legal, and displaying the piece. This header file is intended to be included in other parts of a chess program, where the implementation details of these methods would be defined, likely in a corresponding `.cpp` file.
# Imports and Dependencies

---
- `iostream`
- `piece.h`
- `square.h`


# Data Structures

---
### Bishop<!-- {{#data_structure:Bishop}} -->
- **Type**: `class`
- **Description**: The `Bishop` class represents a chess bishop piece in a chess game, inheriting from the `Piece` class. It includes a constructor to initialize the bishop with a color, a destructor, and methods to get the point value of the bishop, determine if a move to a given square is legal based on diagonal movement, and display the bishop on the board. The bishop's value is set to 3, and it can move diagonally across the board if the path is clear.
- **Member Functions**:
    - [`Bishop::Bishop`](bishop.cpp.driver.md#BishopBishop)
    - [`Bishop::~Bishop`](bishop.cpp.driver.md#BishopBishop)
    - [`Bishop::value`](bishop.cpp.driver.md#Bishopvalue)
    - [`Bishop::canMoveTo`](bishop.cpp.driver.md#BishopcanMoveTo)
    - [`Bishop::display`](bishop.cpp.driver.md#Bishopdisplay)
- **Inherits From**:
    - `Piece`


