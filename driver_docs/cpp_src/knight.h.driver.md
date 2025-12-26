# Purpose
The provided code is a C++ header file, `knight.h`, which defines the `Knight` class, representing a knight piece in a chess game. This class inherits from a base class `Piece`, indicating that it is part of a larger chess-related software system. The `Knight` class encapsulates the specific behaviors and attributes of a knight chess piece, such as its color, point value, and movement capabilities. The class provides a constructor to initialize a knight with a specified color, a destructor, and several member functions that define its functionality. These functions include `value()`, which returns the point value of the knight, `canMoveTo()`, which determines if the knight can legally move to a specified square, and `display()`, which outputs the knight's representation to a given output stream.

The `Knight` class is a specialized component within a broader chess application, focusing on the unique movement and characteristics of the knight piece. It interfaces with other components, such as the `Square` class, to determine legal moves, suggesting that the system models a chessboard and its rules. The use of inheritance from the `Piece` class implies a polymorphic design, allowing for the extension and management of different chess pieces within the application. This header file is intended to be included in other parts of the program, providing a public API for interacting with knight objects, and it is likely part of a larger library or application that simulates or manages chess games.
# Imports and Dependencies

---
- `iostream`
- `square.h`
- `piece.h`


# Data Structures

---
### Knight<!-- {{#data_structure:Knight}} -->
- **Type**: `class`
- **Description**: The `Knight` class represents a chess knight piece and inherits from the `Piece` class. It includes a constructor to initialize the knight with a specified color, a destructor, and several member functions. The `value` function returns the point value of the knight, which is 3. The `canMoveTo` function determines if the knight can legally move to a given square based on the unique L-shaped movement pattern of a knight in chess. The `display` function outputs the knight's representation, which includes its color and the letter 'N' for knight.
- **Member Functions**:
    - [`Knight::Knight`](knight.cpp.driver.md#KnightKnight)
    - [`Knight::~Knight`](knight.cpp.driver.md#KnightKnight)
    - [`Knight::value`](knight.cpp.driver.md#Knightvalue)
    - [`Knight::canMoveTo`](knight.cpp.driver.md#KnightcanMoveTo)
    - [`Knight::display`](knight.cpp.driver.md#Knightdisplay)
- **Inherits From**:
    - `Piece`


