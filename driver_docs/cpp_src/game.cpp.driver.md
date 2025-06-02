# Purpose
The `game.cpp` file is a core component of a chess application, specifically responsible for managing the overall game state and the interactions between players and pieces on the board. This file defines the [`Game`](#Game::Game) class, which encapsulates the initialization and management of chess pieces and players. The [`Game`](#Game::Game) class constructor and destructor handle the creation and cleanup of game resources, such as dynamically allocated chess pieces and player objects. The [`initialize`](#Game::initialize) method sets up the chessboard by placing all pieces in their starting positions and associating them with their respective players, ensuring that the game is ready to begin.

The file includes several headers for different chess piece types, such as `queen.h`, `bishop.h`, `knight.h`, `rook.h`, `pawn.h`, and `king.h`, indicating that it relies on these classes to represent the various chess pieces. The [`Game`](#Game::Game) class also manages the turn-based logic of the game through methods like [`getNextPlayer`](#Game::getNextPlayer) and [`opponentOf`](#Game::opponentOf), which determine the current and opposing players. The use of static member variables for players and piece collections suggests that the [`Game`](#Game::Game) class maintains a single instance of the game state, which is shared across the application. Overall, this file provides a focused implementation of the chess game's core mechanics, serving as a central point for game initialization and player management.
# Imports and Dependencies

---
- `game.h`
- `queen.h`
- `bishop.h`
- `knight.h`
- `rook.h`
- `pawn.h`
- `king.h`
- `square.h`


# Global Variables

---
### player1
- **Type**: `Player*`
- **Description**: `player1` is a global pointer variable of type `Player*` that is part of the `Game` class. It is used to represent the first player in the chess game, typically the player controlling the white pieces.
- **Use**: `player1` is initialized in the `initialize` method to point to a new `Player` object representing the white player, and it is used to determine the current player and their opponent during the game.


---
### player2
- **Type**: `Player*`
- **Description**: The `player2` variable is a global pointer to a `Player` object representing the second player in the game, typically the player controlling the black pieces in a chess game. It is initialized to `NULL` and later assigned a `Player` object in the `initialize` method of the `Game` class.
- **Use**: `player2` is used to store and manage the state and actions of the second player in the chess game.


---
### nextPlayer
- **Type**: `Player*`
- **Description**: The `nextPlayer` variable is a pointer to a `Player` object, which represents the player who is to make the next move in the game. It is initialized to `NULL` and later set to point to one of the two players in the game, either `player1` or `player2`. The variable is used to keep track of whose turn it is to play.
- **Use**: This variable is used to determine and update the current player whose turn it is to make a move in the chess game.


# Data Structures

---
### Game<!-- {{#data_structure:Game}} -->
- **Description**: [See definition](game.h.driver.md#Game)
- **Member Functions**:
    - [`Game::Game`](#Game::Game)
    - [`Game::~Game`](#Game::~Game)
    - [`Game::initialize`](#Game::initialize)
    - [`Game::getNextPlayer`](#Game::getNextPlayer)
    - [`Game::opponentOf`](#Game::opponentOf)

**Methods**

---
#### Game::Game<!-- {{#callable:Game::Game}} -->
The `Game` constructor initializes a new instance of the `Game` class without performing any specific actions.
- **Inputs**:
    - None
- **Control Flow**:
    - The constructor is defined but does not contain any code or logic, indicating it performs no operations when a `Game` object is instantiated.
- **Output**:
    - There is no output or return value from this constructor as it is a default constructor with an empty body.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::\~Game<!-- {{#callable:Game::~Game}} -->
The destructor `~Game` cleans up dynamically allocated memory for chess pieces and players when a `Game` object is destroyed.
- **Inputs**:
    - None
- **Control Flow**:
    - Iterates over the `whitePieces` set, deleting each `Piece` pointer and then clears the set.
    - Iterates over the `blackPieces` set, deleting each `Piece` pointer and then clears the set.
    - Deletes the `player1` and `player2` objects.
- **Output**:
    - This function does not return any value as it is a destructor.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::initialize<!-- {{#callable:Game::initialize}} -->
The `initialize` function sets up a new chess game by creating and positioning all pieces on the board, assigning them to players, and determining the starting player.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize two sets to hold white and black pieces.
    - Create and position a white Queen at (3, 0) and a black Queen at (3, 7), then add them to their respective sets.
    - Create and position two white Bishops at (2, 0) and (5, 0) and two black Bishops at (2, 7) and (5, 7), then add them to their respective sets.
    - Create and position two white Knights at (1, 0) and (6, 0) and two black Knights at (1, 7) and (6, 7), then add them to their respective sets.
    - Create and position two white Rooks at (0, 0) and (7, 0) and two black Rooks at (0, 7) and (7, 7), then add them to their respective sets.
    - Create and position eight white Pawns on row 1 and eight black Pawns on row 6, then add them to their respective sets.
    - Create and position a white King at (4, 0) and a black King at (4, 7), then add them to their respective sets.
    - Create a white player with the white King and white pieces, and a black player with the black King and black pieces.
    - Set the next player to be the black player.
- **Output**:
    - The function does not return any value; it initializes the game state by setting up the board and players.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::getNextPlayer<!-- {{#callable:Game::getNextPlayer}} -->
The `getNextPlayer` function updates and returns the player whose turn is next in the game.
- **Inputs**:
    - None
- **Control Flow**:
    - The function calls [`opponentOf`](#Game::opponentOf) with the current `nextPlayer` to determine the opponent player.
    - The `nextPlayer` is updated to the opponent player returned by [`opponentOf`](#Game::opponentOf).
    - The updated `nextPlayer` is returned.
- **Output**:
    - The function returns a pointer to the `Player` object representing the next player whose turn it is.
- **Functions called**:
    - [`Game::opponentOf`](#Game::opponentOf)
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)


---
#### Game::opponentOf<!-- {{#callable:Game::opponentOf}} -->
The `opponentOf` function returns the opponent player of the given player in a chess game.
- **Inputs**:
    - `player`: A reference to a Player object for whom the opponent is to be determined.
- **Control Flow**:
    - Declare a pointer to Player named `opponent`.
    - Check if the name of the input player matches the name of `player1`.
    - If the names match, set `opponent` to `player2`.
    - If the names do not match, set `opponent` to `player1`.
    - Return the `opponent` pointer.
- **Output**:
    - A pointer to the Player object representing the opponent of the given player.
- **See also**: [`Game`](game.h.driver.md#Game)  (Data Structure)



