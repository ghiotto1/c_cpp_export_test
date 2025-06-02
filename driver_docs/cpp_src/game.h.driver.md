# Purpose
The provided code is a C++ header file named `game.h`, which defines a class `Game` that represents a game of chess. This file is part of a broader chess application, as indicated by its inclusion of other headers such as `board.h`, `piece.h`, and `player.h`. The `Game` class encapsulates the core functionality required to manage a chess game, including initializing the game, determining the next player to move, and identifying the opponent of a given player. The class is designed with both public and private members, where the public interface provides essential methods for game management, and the private section contains attributes that maintain the state of the game, such as the players and the sets of pieces for each side.

The `Game` class is structured to be used as a singleton, as suggested by its static methods and attributes, which implies that only one instance of the game is intended to be active at any time. The static methods `initialize`, `getNextPlayer`, and `opponentOf` provide the primary interface for interacting with the game state, while the private constructor prevents direct instantiation of the class. This design pattern ensures controlled access to the game state and enforces the logic necessary for managing a chess game. The use of static attributes like `player1`, `player2`, `nextPlayer`, and the sets of pieces (`whitePieces` and `blackPieces`) further supports this singleton approach, centralizing the game state within the class itself.
# Imports and Dependencies

---
- `set`
- `iostream`
- `board.h`
- `piece.h`
- `player.h`


# Data Structures

---
### Game<!-- {{#data_structure:Game}} -->
- **Type**: `class`
- **Members**:
    - `player1`: A static pointer to the first player, representing the white player in the game.
    - `player2`: A static pointer to the second player, representing the black player in the game.
    - `nextPlayer`: A static pointer to the player whose turn is next.
    - `whitePieces`: A static set containing pointers to all the white pieces in the game.
    - `blackPieces`: A static set containing pointers to all the black pieces in the game.
- **Description**: The `Game` class represents a game of chess, managing the players and their respective pieces. It includes static methods to initialize the game, determine the next player, and find the opponent of a given player. The class maintains static attributes for the two players, the next player to move, and sets of pieces for both white and black sides. The destructor ensures proper cleanup of dynamically allocated pieces and players.
- **Member Functions**:
    - [`Game::Game`](game.cpp.driver.md#GameGame)
    - [`Game::~Game`](game.cpp.driver.md#GameGame)
    - [`Game::initialize`](game.cpp.driver.md#Gameinitialize)
    - [`Game::getNextPlayer`](game.cpp.driver.md#GamegetNextPlayer)
    - [`Game::opponentOf`](game.cpp.driver.md#GameopponentOf)


