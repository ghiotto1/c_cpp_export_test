# Purpose
The provided code is a C++ header file (`king.h`) that defines a class representing a chess king piece, which is part of a broader chess game application. This class, `King`, inherits from a base class `RestrictedPiece`, suggesting it shares common functionality with other restricted chess pieces, such as the queen or bishop. The class offers narrow functionality specific to the king piece, including methods to determine its point value, check if a move is legal, and display the piece. The constructor initializes the king with a specified color, and the destructor is defined but not explicitly implemented in this header. This file is intended to be included in other parts of the application where the king's behavior and properties are needed.
# Imports and Dependencies

---
- `iostream`
- `restrictedPiece.h`


# Data Structures

---
### King<!-- {{#data_structure:King}} -->
- **Type**: `class`
- **Description**: The `King` class represents a chess king piece and inherits from the `RestrictedPiece` class. It includes a constructor to initialize the king with a specified color, a destructor, and methods to determine the point value of the king, check if a move to a specific square is legal, and display the king on an output stream. The king can move one square in any direction, which is implemented in the `canMoveTo` method.
- **Member Functions**:
    - [`King::King`](king.cpp.driver.md#KingKing)
    - [`King::~King`](king.cpp.driver.md#KingKing)
    - [`King::value`](king.cpp.driver.md#Kingvalue)
    - [`King::canMoveTo`](king.cpp.driver.md#KingcanMoveTo)
    - [`King::display`](king.cpp.driver.md#Kingdisplay)
- **Inherits From**:
    - [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)


