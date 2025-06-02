# Purpose
The provided code is a C++ header file (`pawn.h`) that defines a class representing a chess pawn piece, which is a specific type of chess piece with restricted movement capabilities. This class, `Pawn`, inherits from a base class `RestrictedPiece`, suggesting that it is part of a broader chess game implementation where different pieces have varying movement rules. The class offers narrow functionality specific to the pawn's behavior, including methods for setting its location, determining its point value, moving to a new square, checking the legality of a move, and displaying the piece. The header file is intended to be included in other parts of a chess program, as indicated by the inclusion guards (`#ifndef PAWN_H` and `#define PAWN_H`) and the inclusion of other headers like `square.h` and `restrictedPiece.h`.
# Imports and Dependencies

---
- `iostream`
- `square.h`
- `restrictedPiece.h`


# Data Structures

---
### Pawn<!-- {{#data_structure:Pawn}} -->
- **Type**: `class`
- **Members**:
    - `_delegate`: A pointer to a Piece object used for delegation when the pawn is promoted.
- **Description**: The Pawn class represents a pawn piece in a chess game, inheriting from the RestrictedPiece class. It encapsulates the behavior and attributes specific to a pawn, including its movement rules and promotion to a queen when reaching the opponent's end of the board. The class uses a delegate pattern to handle the pawn's behavior after promotion, allowing it to adopt the movement rules of a queen. The Pawn class provides methods to set its location, determine its point value, move to a new square, check if a move is legal, and display itself.
- **Member Functions**:
    - [`Pawn::Pawn`](pawn.cpp.driver.md#PawnPawn)
    - [`Pawn::~Pawn`](pawn.cpp.driver.md#PawnPawn)
    - [`Pawn::setLocation`](pawn.cpp.driver.md#PawnsetLocation)
    - [`Pawn::value`](pawn.cpp.driver.md#Pawnvalue)
    - [`Pawn::moveTo`](pawn.cpp.driver.md#PawnmoveTo)
    - [`Pawn::canMoveTo`](pawn.cpp.driver.md#PawncanMoveTo)
    - [`Pawn::display`](pawn.cpp.driver.md#Pawndisplay)
- **Inherits from**:
    - [`RestrictedPiece`](restrictedPiece.h.driver.md#RestrictedPiece)


