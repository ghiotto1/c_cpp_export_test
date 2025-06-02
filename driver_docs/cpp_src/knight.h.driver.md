# Purpose
The provided code is a C++ header file (`knight.h`) that defines a class representing a chess knight piece, indicating narrow functionality specific to chess game logic. This class, `Knight`, inherits from a base class `Piece`, suggesting it is part of a larger chess game framework. The header file declares several member functions: a constructor to initialize the knight with a color, a destructor, a method to return the knight's point value, a method to check if a move to a specified square is legal, and a method to display the knight. The inclusion of other headers, `square.h` and `piece.h`, implies dependencies on other components of the chess game, such as board squares and general piece behavior.
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
- **Inherits from**:
    - [`Piece`](piece.h.driver.md#Piece)


