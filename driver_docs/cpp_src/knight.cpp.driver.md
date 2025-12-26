# Purpose
The `knight.cpp` file is part of a larger Chess project and implements the behavior specific to the Knight piece in a game of chess. This file provides a narrow functionality focused on defining the characteristics and movement rules of the Knight. It includes the implementation of the [`Knight`](#KnightKnight) class, which inherits from a base class `Piece`, indicating that it is part of a polymorphic design where different chess pieces share common attributes and behaviors. The constructor initializes the Knight with a color, and the destructor is defined, though it does not perform any specific actions.

The file defines several key methods for the Knight. The `value()` method returns the standard chess value of a Knight, which is 3. The `canMoveTo(Square& location)` method implements the unique L-shaped movement pattern of the Knight, checking if a move to a given square is valid based on the Knight's ability to move two squares in one direction and one square in a perpendicular direction. The `display()` method outputs a representation of the Knight, using "N" to denote the piece, prefixed by its color. This file is intended to be part of a larger system, likely imported and used by other components of the Chess project to simulate and manage the game state.
# Imports and Dependencies

---
- `knight.h`


# Data Structures

---
### Knight<!-- {{#data_structure:Knight}} -->
- **Description**: [See definition](knight.h.driver.md#Knight)
- **Member Functions**:
    - [`Knight::Knight`](#KnightKnight)
    - [`Knight::~Knight`](#KnightKnight)
    - [`Knight::value`](#Knightvalue)
    - [`Knight::canMoveTo`](#KnightcanMoveTo)
    - [`Knight::display`](#Knightdisplay)
- **Inherits From**:
    - `Piece`

**Methods**

---
#### Knight::Knight<!-- {{#callable:Knight::Knight}} -->
The `Knight` constructor initializes a `Knight` object by calling the `Piece` constructor with a boolean indicating the piece's color.
- **Inputs**:
    - `isWhite`: A boolean value indicating whether the knight is white (true) or black (false).
- **Control Flow**:
    - The constructor `Knight::Knight(bool isWhite)` is called with a boolean parameter `isWhite`.
    - The constructor initializes the `Knight` object by invoking the constructor of its base class `Piece` with the `isWhite` parameter.
- **Output**: A `Knight` object is created and initialized with the specified color.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::\~Knight<!-- {{#callable:Knight::~Knight}} -->
The `Knight::~Knight` function is the default destructor for the `Knight` class, which currently performs no specific actions upon object destruction.
- **Inputs**: None
- **Control Flow**:
    - The destructor is called when a `Knight` object goes out of scope or is explicitly deleted.
    - Currently, the destructor does not contain any code, so it performs no operations.
- **Output**: There is no output from this destructor as it is empty and performs no actions.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::value<!-- {{#callable:Knight::value}} -->
The `value` function returns the point value of a Knight piece in a chess game.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the integer value 3, representing the point value of a Knight in chess.
- **Output**: The function returns an integer value of 3.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::canMoveTo<!-- {{#callable:Knight::canMoveTo}} -->
The `canMoveTo` function determines if a Knight piece can legally move to a specified square based on chess movement rules for a Knight.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the Knight is attempting to move.
- **Control Flow**:
    - Initialize `validMove` to `false`.
    - Calculate `translationX` as the difference between the target square's x-coordinate and the Knight's current x-coordinate.
    - Calculate `translationY` as the difference between the target square's y-coordinate and the Knight's current y-coordinate.
    - Check if the move is valid by verifying if the absolute values of `translationY` and `translationX` match the Knight's L-shaped movement pattern (1 square in one direction and 2 squares in the perpendicular direction).
    - If either condition for a valid Knight move is met, set `validMove` to `true`.
    - Return the value of `validMove`.
- **Output**: A boolean value indicating whether the Knight can legally move to the specified square (`true` if the move is valid, `false` otherwise).
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)


---
#### Knight::display<!-- {{#callable:Knight::display}} -->
The `display` function outputs the knight's color followed by the letter 'N' to represent the knight piece in a chess game.
- **Inputs**: None
- **Control Flow**:
    - The function uses the `cout` stream to output the knight's color concatenated with the letter 'N'.
- **Output**: The function outputs a string to the standard output stream, representing the knight's color and type.
- **See also**: [`Knight`](knight.h.driver.md#Knight)  (Data Structure)



