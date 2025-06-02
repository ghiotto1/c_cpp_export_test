# Purpose
The `player.cpp` file is part of a Chess game project and implements the [`Player`](#PlayerPlayer) class, which encapsulates the behavior and attributes of a chess player. This file provides functionality specific to managing a player's actions and state within a game, such as making moves, checking if the player is in check, capturing pieces, and calculating the player's score based on captured pieces. The class constructor initializes a player with a name, color, a reference to their king, and a set of pieces they control. The [`makeMove`](#PlayermakeMove) function handles player input for moves, ensuring they are valid and in algebraic notation, and then executes the move on the board. The [`inCheck`](#PlayerinCheck) function determines if the player's king is under threat from any of the opponent's pieces, while the [`capture`](#Playercapture) function updates the state of a captured piece and adds it to the player's collection of captured pieces.

The file includes several key components such as the [`makeMove`](#PlayermakeMove), [`inCheck`](#PlayerinCheck), [`capture`](#Playercapture), and [`score`](#Playerscore) methods, which are central to the player's interaction with the game. The [`makeMove`](#PlayermakeMove) method is particularly important as it interfaces with the board to execute moves, while [`inCheck`](#PlayerinCheck) and [`capture`](#Playercapture) manage game state and player strategy. The file also defines accessors like [`getName`](#PlayergetName), [`isWhite`](#PlayerisWhite), [`myPieces`](#PlayermyPieces), and [`myKing`](#PlayermyKing), which provide information about the player's identity and current game status. This file is a C++ source file that is likely part of a larger application, interacting with other components such as `board.h`, `game.h`, and `player.h`, and does not define a standalone executable. Instead, it contributes to the broader functionality of the Chess game by managing player-specific logic and interactions.
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
The Player constructor initializes a Player object with a name, color, a reference to their King, and a set of their pieces.
- **Inputs**:
    - `name`: A string representing the player's name.
    - `isWhite`: A boolean indicating whether the player is playing with the white pieces.
    - `myKing`: A reference to the player's King object.
    - `myPieces`: A reference to a set of pointers to the player's Piece objects.
- **Control Flow**:
    - The constructor initializes the private member variables _name, _isWhite, _myPieces, and _myKing with the provided arguments.
- **Output**:
    - The function does not return any value as it is a constructor.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::\~Player<!-- {{#callable:Player::~Player}} -->
The `~Player` function is the default destructor for the `Player` class, responsible for cleaning up resources when a `Player` object is destroyed.
- **Inputs**:
    - None
- **Control Flow**:
    - The destructor is defined but does not contain any specific logic or resource deallocation code.
    - It is implicitly called when a `Player` object goes out of scope or is explicitly deleted.
- **Output**:
    - The destructor does not return any value or perform any specific actions, as it is currently empty.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::makeMove<!-- {{#callable:Player::makeMove}} -->
The `makeMove` function allows a player to input and execute a move in a chess game, ensuring the move is valid and in the correct format.
- **Inputs**:
    - `none`: The function does not take any parameters; it relies on user input for the move.
- **Control Flow**:
    - Check if the player is currently in check and announce it if true.
    - Prompt the player to enter a move in algebraic notation (e.g., 'a2 a4').
    - Validate the input to ensure it is in the correct format and the starting square is occupied.
    - If the input is invalid, prompt the player to enter a move again until a valid move is provided.
    - Translate the valid input from algebraic notation to board coordinates.
    - Execute the move by moving the piece from the starting square to the destination square.
- **Output**:
    - Returns a boolean indicating whether the move was successfully executed.
- **Functions called**:
    - [`Player::inCheck`](#PlayerinCheck)
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::inCheck<!-- {{#callable:Player::inCheck}} -->
The `inCheck` function determines if the current player's king is in check by checking if any opponent's piece can move to the king's location.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a boolean variable `check` to `false`.
    - Iterate over each piece in the opponent's set of pieces.
    - For each piece, check if it is located on the board and can move to the current player's king's location.
    - If such a piece is found, set `check` to `true`.
    - Return the value of `check`.
- **Output**:
    - A boolean value indicating whether the player's king is in check (true if in check, false otherwise).
- **Functions called**:
    - [`Player::myKing`](#PlayermyKing)
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::capture<!-- {{#callable:Player::capture}} -->
The `capture` function removes a piece from the board and adds it to the player's set of captured pieces.
- **Inputs**:
    - `aPiece`: A pointer to the Piece object that is to be captured.
- **Control Flow**:
    - The function first calls `setLocation(NULL)` on the `aPiece` to unset its location on the board, effectively removing it from play.
    - The function then inserts `aPiece` into the player's `_capturedPieces` set, indicating that the piece has been captured by this player.
- **Output**:
    - The function does not return any value.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::getName<!-- {{#callable:Player::getName}} -->
The `getName` function returns the name of the player.
- **Inputs**:
    - None
- **Control Flow**:
    - The function accesses the private member variable `_name` of the `Player` class.
    - It returns the value of `_name`.
- **Output**:
    - The function returns a `string` representing the player's name.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::isWhite<!-- {{#callable:Player::isWhite}} -->
The `isWhite` function checks if the player is the white player in a chess game.
- **Inputs**:
    - None
- **Control Flow**:
    - The function directly returns the value of the private member variable `_isWhite`.
- **Output**:
    - A boolean value indicating whether the player is the white player (`true` if white, `false` otherwise).
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::score<!-- {{#callable:Player::score}} -->
The `score` function calculates the total score of a player's captured pieces by summing their values.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a local variable `score` to 0 to hold the total score.
    - Iterate over each piece in the `_capturedPieces` set using an iterator.
    - For each piece, retrieve its value using the `value()` method and add it to the `score`.
    - Return the total `score` after iterating through all captured pieces.
- **Output**:
    - The function returns an integer representing the total score of the player's captured pieces.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::myPieces<!-- {{#callable:Player::myPieces}} -->
The `myPieces` function returns a pointer to the set of pieces owned by the player.
- **Inputs**:
    - None
- **Control Flow**:
    - The function simply returns the address of the `_myPieces` member variable, which is a reference to a set of `Piece` pointers.
- **Output**:
    - A pointer to a `set<Piece*>` representing the player's pieces.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)


---
#### Player::myKing<!-- {{#callable:Player::myKing}} -->
The `myKing` function returns a pointer to the `King` object associated with the `Player` instance.
- **Inputs**:
    - None
- **Control Flow**:
    - The function simply returns the address of the `_myKing` member variable, which is a reference to a `King` object.
- **Output**:
    - A pointer to the `King` object associated with the `Player` instance.
- **See also**: [`Player`](player.h.driver.md#Player)  (Data Structure)



