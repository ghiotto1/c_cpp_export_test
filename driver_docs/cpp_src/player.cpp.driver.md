# Purpose
The `player.cpp` file is part of a Chess game project and implements the functionality related to a player in the game. This file defines the [`Player`](#PlayerPlayer) class, which encapsulates the attributes and behaviors of a chess player, such as their name, the color they are playing (white or black), their pieces, and their king. The class provides methods for making moves, checking if the player is in check, capturing opponent pieces, and calculating the player's score based on captured pieces. The [`makeMove`](#PlayermakeMove) method is particularly important as it handles player input for moves, validates the input, and executes the move on the board if valid. The [`inCheck`](#PlayerinCheck) method determines if the player's king is under threat from any of the opponent's pieces, which is a critical aspect of chess gameplay.

This file is a C++ source file that likely works in conjunction with other components of the Chess project, such as `board.h` and `game.h`, which are included at the beginning of the file. The [`Player`](#PlayerPlayer) class interacts with these components to manage the state of the game, such as the board's configuration and the pieces' positions. The file does not define a public API or external interface but rather provides the internal logic necessary for player-related operations within the game. The use of standard input/output functions indicates that this file may be part of a console-based application where players input their moves directly.
# Imports and Dependencies

---
- `iostream`
- `player.h`
- `board.h`
- `game.h`


# Data Structures

---
### Player<!-- {{#data_structure:Player}} -->
- **Description**: [See definition](player.h.driver.md#Player)
- **Member Functions**:
    - [`Player::Player`](#PlayerPlayer)
    - [`Player::~Player`](#PlayerPlayer)
    - [`Player::makeMove`](#PlayermakeMove)
    - [`Player::inCheck`](#PlayerinCheck)
    - [`Player::capture`](#Playercapture)
    - [`Player::getName`](#PlayergetName)
    - [`Player::isWhite`](#PlayerisWhite)
    - [`Player::score`](#Playerscore)
    - [`Player::myPieces`](#PlayermyPieces)
    - [`Player::myKing`](#PlayermyKing)

**Methods**

---
#### Player::Player<!-- {{#callable:Player::Player}} -->
The `Player` constructor initializes a `Player` object with a name, color, a reference to their king, and a set of their pieces.
- **Inputs**:
    - `name`: A string representing the player's name.
    - `isWhite`: A boolean indicating whether the player is playing with the white pieces.
    - `myKing`: A reference to the `King` object that belongs to the player.
    - `myPieces`: A reference to a set of pointers to `Piece` objects representing the player's pieces.
- **Control Flow**:
    - The constructor initializes the `_name` member variable with the provided `name` argument.
    - The `_isWhite` member variable is initialized with the `isWhite` argument to indicate the player's color.
    - The `_myPieces` member variable is initialized with the reference to the set of pieces provided by `myPieces`.
    - The `_myKing` member variable is initialized with the reference to the `King` object provided by `myKing`.
- **Output**: The constructor does not return any value as it is used to initialize a `Player` object.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::\~Player<!-- {{#callable:Player::~Player}} -->
The `Player::~Player()` function is the default destructor for the `Player` class, which currently does not perform any specific operations upon object destruction.
- **Inputs**: None
- **Control Flow**:
    - The destructor is defined but contains no code, indicating it does not perform any specific actions when a `Player` object is destroyed.
- **Output**: There is no output or return value from this destructor, as it is a default destructor with no operations.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::makeMove<!-- {{#callable:Player::makeMove}} -->
The `makeMove` function allows a player to input and execute a move on the chessboard, ensuring the move is valid and in algebraic notation.
- **Inputs**:
    - `None`: The function does not take any parameters; it relies on user input for the move.
- **Control Flow**:
    - Check if the player is in check and announce it if true.
    - Prompt the player to enter a move in algebraic notation (e.g., 'a2 a4').
    - Validate the input to ensure it is in the correct format and the starting square is occupied.
    - If the input is invalid, prompt the player again until a valid move is entered.
    - Translate the algebraic notation into board coordinates.
    - Move the piece from the starting square to the destination square using the `moveTo` method.
- **Output**: Returns a boolean indicating whether the move was successfully executed.
- **Functions called**:
    - [`Player::inCheck`](#PlayerinCheck)
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::inCheck<!-- {{#callable:Player::inCheck}} -->
The `inCheck` function determines if the current player's king is in check by checking if any opponent's piece can move to the king's location.
- **Inputs**: None
- **Control Flow**:
    - Initialize a boolean variable `check` to false.
    - Iterate over each piece in the opponent's set of pieces.
    - For each piece, check if it is located on the board and can move to the current player's king's location.
    - If such a piece is found, set `check` to true.
    - Return the value of `check`.
- **Output**: A boolean value indicating whether the player's king is in check (true if in check, false otherwise).
- **Functions called**:
    - [`Player::myKing`](#PlayermyKing)
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::capture<!-- {{#callable:Player::capture}} -->
The `capture` function removes a piece from the board and adds it to the player's set of captured pieces.
- **Inputs**:
    - `aPiece`: A pointer to the `Piece` object that is to be captured.
- **Control Flow**:
    - The function first sets the location of the piece `aPiece` to `NULL`, effectively removing it from the board.
    - Then, it inserts the piece into the player's `_capturedPieces` set, which keeps track of all pieces captured by the player.
- **Output**: The function does not return any value.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::getName<!-- {{#callable:Player::getName}} -->
The `getName` function returns the name of the player.
- **Inputs**: None
- **Control Flow**:
    - The function accesses the private member variable `_name` of the `Player` class.
    - It returns the value of `_name`.
- **Output**: A string representing the player's name.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::isWhite<!-- {{#callable:Player::isWhite}} -->
The `isWhite` function checks if the player is the white player in a chess game.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the value of the private member variable `_isWhite`.
- **Output**: A boolean value indicating whether the player is the white player (`true`) or not (`false`).
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::score<!-- {{#callable:Player::score}} -->
The `score` function calculates and returns the total score of all pieces captured by the player.
- **Inputs**: None
- **Control Flow**:
    - Initialize a local variable `score` to 0.
    - Iterate over each piece in the player's `_capturedPieces` set.
    - For each piece, add its value (obtained by calling the `value()` method on the piece) to the `score`.
    - Return the accumulated `score`.
- **Output**: The function returns an integer representing the total score of the captured pieces.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::myPieces<!-- {{#callable:Player::myPieces}} -->
The `myPieces` function returns a pointer to the set of pieces owned by the player.
- **Inputs**: None
- **Control Flow**:
    - The function simply returns the address of the `_myPieces` member variable, which is a reference to a set of `Piece*`.
- **Output**: A pointer to a `set<Piece*>` representing the player's pieces.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::myKing<!-- {{#callable:Player::myKing}} -->
The `myKing` function returns a pointer to the `King` object associated with the `Player` instance.
- **Inputs**: None
- **Control Flow**:
    - The function directly returns the address of the `_myKing` member variable, which is a reference to a `King` object.
- **Output**: A pointer to the `King` object associated with the `Player` instance.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)



