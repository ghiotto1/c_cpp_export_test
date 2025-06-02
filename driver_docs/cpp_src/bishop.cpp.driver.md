# Purpose
This C++ code defines the implementation of a [`Bishop`](#BishopBishop) class, which is part of a chess game project. The code provides narrow functionality specific to the behavior and characteristics of a bishop piece in chess. It is a C++ source file intended to be compiled as part of a larger chess application, likely alongside other piece classes. The [`Bishop`](#BishopBishop) class inherits from a `Piece` class, indicating a class hierarchy for different chess pieces. It includes methods to determine the bishop's value, check if a move is valid based on diagonal movement, and display the bishop's representation. The code relies on external components such as a `Board` class and a `Square` class, suggesting it is part of a modular design where each piece type has its own implementation file.
# Imports and Dependencies

---
- `bishop.h`


# Data Structures

---
### Bishop<!-- {{#data_structure:Bishop}} -->
- **Description**: [See definition](bishop.h.driver.md#Bishop)
- **Member Functions**:
    - [`Bishop::Bishop`](#BishopBishop)
    - [`Bishop::~Bishop`](#BishopBishop)
    - [`Bishop::value`](#Bishopvalue)
    - [`Bishop::canMoveTo`](#BishopcanMoveTo)
    - [`Bishop::display`](#Bishopdisplay)
- **Inherits from**:
    - `Piece`

**Methods**

---
#### Bishop::Bishop<!-- {{#callable:Bishop::Bishop}} -->
The `Bishop` constructor initializes a Bishop object with a specified color by calling the base class `Piece` constructor.
- **Inputs**:
    - `isWhite`: A boolean indicating whether the Bishop is white (true) or black (false).
- **Control Flow**:
    - The constructor `Bishop::Bishop(bool isWhite)` is called with a boolean parameter `isWhite`.
    - The constructor initializes the Bishop object by calling the base class `Piece` constructor with the `isWhite` parameter.
- **Output**:
    - There is no return value as this is a constructor for initializing a Bishop object.
- **See also**: [`Bishop`](bishop.h.driver.md#Bishop)  (Data Structure)


---
#### Bishop::\~Bishop<!-- {{#callable:Bishop::~Bishop}} -->
The destructor for the Bishop class is a default destructor that performs no specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is called when a Bishop object is destroyed.
    - No specific actions or resource deallocations are performed within the destructor.
- **Output**:
    - There is no output or return value from the destructor.
- **See also**: [`Bishop`](bishop.h.driver.md#Bishop)  (Data Structure)


---
#### Bishop::value<!-- {{#callable:Bishop::value}} -->
The `value` function returns the point value of a Bishop piece in a chess game.
- **Inputs**:
    - None
- **Control Flow**:
    - The function is a constant member function of the `Bishop` class, indicating it does not modify the state of the object.
    - It directly returns the integer value `3`, which represents the point value of a Bishop in chess.
- **Output**:
    - The function returns an integer value of `3`, representing the point value of a Bishop piece.
- **See also**: [`Bishop`](bishop.h.driver.md#Bishop)  (Data Structure)


---
#### Bishop::canMoveTo<!-- {{#callable:Bishop::canMoveTo}} -->
The `canMoveTo` function determines if a Bishop can legally move to a specified square by checking if the path is a clear diagonal.
- **Inputs**:
    - `location`: A reference to a `Square` object representing the target location to which the Bishop intends to move.
- **Control Flow**:
    - Initialize a boolean variable `validMove` to `false`.
    - Check if the path from the Bishop's current location to the target `location` is a clear diagonal using `Board::getBoard()->isClearDiagonal`.
    - If the path is clear, set `validMove` to `true`.
    - Return the value of `validMove`.
- **Output**:
    - A boolean value indicating whether the Bishop can legally move to the specified square.
- **See also**: [`Bishop`](bishop.h.driver.md#Bishop)  (Data Structure)


---
#### Bishop::display<!-- {{#callable:Bishop::display}} -->
The `display` function outputs the color and type of the Bishop piece to the console.
- **Inputs**:
    - None
- **Control Flow**:
    - The function uses the `cout` stream to output the Bishop's color followed by the letter 'B'.
- **Output**:
    - The function outputs a string to the console that represents the Bishop piece, consisting of its color and the letter 'B'.
- **See also**: [`Bishop`](bishop.h.driver.md#Bishop)  (Data Structure)



