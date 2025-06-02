# Purpose
The provided code is a C++ source file, likely part of a larger chess application, that defines the implementation of a [`Square`](#Square::Square) class. This class offers narrow functionality, specifically managing the state of a square on a chessboard, including its coordinates and the piece occupying it. The class constructor initializes the square's position and sets the occupying piece to `NULL`, while the destructor is defined but does not perform any specific actions. The class provides methods to set and retrieve the piece occupying the square, check if the square is occupied, and access the square's coordinates. This file is intended to be compiled and linked with other parts of the ChessProject, as it includes headers for dependencies like `piece.h` and `square.h`.
# Imports and Dependencies

---
- `piece.h`
- `square.h`


# Data Structures

---
### Square<!-- {{#data_structure:Square}} -->
- **Description**: [See definition](square.h.driver.md#Square)
- **Member Functions**:
    - [`Square::Square`](#Square::Square)
    - [`Square::~Square`](#Square::~Square)
    - [`Square::setOccupier`](#Square::setOccupier)
    - [`Square::getX`](#Square::getX)
    - [`Square::getY`](#Square::getY)
    - [`Square::occupied`](#Square::occupied)
    - [`Square::occupiedBy`](#Square::occupiedBy)

**Methods**

---
#### Square::Square<!-- {{#callable:Square::Square}} -->
The `Square` constructor initializes a `Square` object with specified x and y coordinates and sets the occupying piece to NULL.
- **Inputs**:
    - `x`: The x-coordinate of the square on the board.
    - `y`: The y-coordinate of the square on the board.
- **Control Flow**:
    - The constructor initializes the private member variable `_x` with the value of the input parameter `x`.
    - The constructor initializes the private member variable `_y` with the value of the input parameter `y`.
    - The constructor sets the private member variable `_piece` to `NULL`, indicating that the square is initially unoccupied.
- **Output**:
    - The function does not return any value as it is a constructor for the `Square` class.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::\~Square<!-- {{#callable:Square::~Square}} -->
The destructor for the Square class, `~Square`, is a default destructor that performs no specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is called when a Square object is destroyed.
    - No specific actions or resource deallocations are performed within the destructor.
- **Output**:
    - There is no output or return value from the destructor.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::setOccupier<!-- {{#callable:Square::setOccupier}} -->
The `setOccupier` function assigns a `Piece` object to a `Square` object, indicating that the square is occupied by that piece.
- **Inputs**:
    - `piece`: A pointer to a `Piece` object that is to be set as the occupier of the square.
- **Control Flow**:
    - The function takes a pointer to a `Piece` object as an argument.
    - It assigns this pointer to the private member variable `_piece` of the `Square` class, effectively setting the piece that occupies the square.
- **Output**:
    - The function does not return any value.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::getX<!-- {{#callable:Square::getX}} -->
The `getX` function returns the x-coordinate of a `Square` object.
- **Inputs**:
    - None
- **Control Flow**:
    - The function accesses the private member variable `_x` of the `Square` class.
    - It returns the value of `_x`.
- **Output**:
    - The function returns an integer representing the x-coordinate of the `Square`.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::getY<!-- {{#callable:Square::getY}} -->
The `getY` function returns the Y-coordinate of a `Square` object.
- **Inputs**:
    - None
- **Control Flow**:
    - The function accesses the private member variable `_y` of the `Square` class.
    - It returns the value of `_y`.
- **Output**:
    - The function returns an integer representing the Y-coordinate of the square.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::occupied<!-- {{#callable:Square::occupied}} -->
The `occupied` function checks if a `Square` object is occupied by a `Piece`.
- **Inputs**:
    - None
- **Control Flow**:
    - The function accesses the private member `_piece` of the `Square` class.
    - It returns the boolean value of `_piece`, which is `true` if `_piece` is not `NULL` (indicating the square is occupied) and `false` if `_piece` is `NULL` (indicating the square is not occupied).
- **Output**:
    - A boolean value indicating whether the square is occupied by a piece.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)


---
#### Square::occupiedBy<!-- {{#callable:Square::occupiedBy}} -->
The `occupiedBy` function returns the `Piece` object that currently occupies the `Square`.
- **Inputs**:
    - None
- **Control Flow**:
    - The function directly returns the private member variable `_piece`, which is a pointer to a `Piece` object.
- **Output**:
    - A pointer to the `Piece` object that occupies the `Square`, or `NULL` if the square is unoccupied.
- **See also**: [`Square`](square.h.driver.md#Square)  (Data Structure)



