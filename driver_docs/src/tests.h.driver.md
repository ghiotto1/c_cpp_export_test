# Purpose
This C header file defines a series of function prototypes for testing various components of a chess game implementation. It is designed to facilitate unit testing by providing declarations for functions that test different aspects of the chess program, such as board creation, move generation, and piece movement. The file includes functions for testing specific chess functionalities, including square properties, move creation and validation, board state management, and special conditions like castling and insufficient material for a draw. The [`failTest`](#failTest) function is particularly notable as it is intended to halt the program when a test fails, optionally providing a message. Overall, this file serves as a blueprint for implementing comprehensive tests to ensure the correctness and reliability of a chess game coded in C.
# Function Declarations (Public API)

---
### failTest<!-- {{#callable_declaration:failTest}} -->
Fails the current test and terminates the program.
- **Description**: This function is used to indicate a failure in the currently running test by printing a failure message to the standard error stream and then terminating the program. It should be called when a test condition fails and the test cannot continue. The function can optionally include a custom message to provide additional context about the failure. It is important to note that this function will halt the entire program, so it should be used judiciously within a testing framework.
- **Inputs**:
    - `msg`: A pointer to a null-terminated string containing a custom failure message. If this parameter is NULL, no additional message is printed beyond the default failure notification. The caller retains ownership of the string, and it must be a valid pointer or NULL.
- **Output**: None
- **See also**: [`failTest`](tests.c.driver.md#failTest)  (Implementation)


---
### validateString<!-- {{#callable_declaration:validateString}} -->
Compares two strings and fails the test if they are not equal.
- **Description**: Use this function to verify that two strings are identical during a test. It is intended for use in a testing environment where the program should halt if the strings do not match. The function compares the provided strings and, if they differ, it constructs a detailed error message and calls `failTest` to terminate the test. This function should be used when exact string matching is critical for the test's success.
- **Inputs**:
    - `actual`: A pointer to the actual string to be compared. Must not be null, as passing a null pointer will result in undefined behavior.
    - `expected`: A pointer to the expected string to be compared against. Must not be null, as passing a null pointer will result in undefined behavior.
- **Output**: None
- **See also**: [`validateString`](tests.c.driver.md#validateString)  (Implementation)


---
### testSqI<!-- {{#callable_declaration:testSqI}} -->
Tests the square indexing function for correctness.
- **Description**: This function is used to verify the correctness of the square indexing function `sqI` by iterating over all possible chessboard squares and checking if the function returns the expected file and rank. It is intended to be used in a testing environment to ensure that the `sqI` function behaves as expected for all valid chessboard positions. The function will call `failTest` with an appropriate message if any discrepancy is found, halting the test execution. This function should be used when validating the implementation of square indexing in a chess program.
- **Inputs**: None
- **Output**: None
- **See also**: [`testSqI`](tests.c.driver.md#testSqI)  (Implementation)


---
### testSqS<!-- {{#callable_declaration:testSqS}} -->
Tests the conversion of chess square strings to square objects.
- **Description**: This function is used to verify that the conversion from chess square notation strings (e.g., "a1", "h8") to square objects is functioning correctly. It iterates over all possible squares on a chessboard, converts each square's string representation to a square object, and checks if the resulting object's file and rank match the expected values. If any conversion does not match the expected result, the test fails and halts execution with an error message. This function is typically used during development to ensure the correctness of the square conversion logic.
- **Inputs**: None
- **Output**: None
- **See also**: [`testSqS`](tests.c.driver.md#testSqS)  (Implementation)


---
### testSqGetStr<!-- {{#callable_declaration:testSqGetStr}} -->
Tests the string representation of chessboard squares.
- **Description**: This function is used to verify that the string representation of each square on a chessboard is correctly generated. It iterates over all possible squares on an 8x8 chessboard, constructs the expected string representation for each square, and validates it against the actual string returned by the `sqGetStr` function. This function is typically used in a testing context to ensure the correctness of the `sqGetStr` function, and it assumes that the chessboard is indexed from 1 to 8 for both ranks and files.
- **Inputs**: None
- **Output**: None
- **See also**: [`testSqGetStr`](tests.c.driver.md#testSqGetStr)  (Implementation)


---
### testSqIsDark<!-- {{#callable_declaration:testSqIsDark}} -->
Tests if the function correctly identifies dark squares on a chessboard.
- **Description**: This function is used to verify the correctness of the `sqIsDark` function, which determines if a given square on a chessboard is dark. It iterates over all squares on a standard 8x8 chessboard, checking if each square is correctly identified as dark or light. The function expects the `sqIsDark` function to return 1 for dark squares and 0 for light squares, starting with a1 as dark. If a discrepancy is found, it calls `failTest` with a descriptive message. This function is typically used in a testing environment to ensure the accuracy of the chessboard square color identification logic.
- **Inputs**: None
- **Output**: None
- **See also**: [`testSqIsDark`](tests.c.driver.md#testSqIsDark)  (Implementation)


---
### testMoveCreate<!-- {{#callable_declaration:testMoveCreate}} -->
Tests the creation of chess moves.
- **Description**: This function is used to verify the correct creation of chess moves within the testing framework. It should be called to ensure that moves are generated accurately according to the expected parameters. This function is part of a suite of tests for a chess implementation and is intended to validate the move creation logic by comparing the generated moves against expected values. It is typically used during development to catch errors in move generation logic.
- **Inputs**: None
- **Output**: None
- **See also**: [`testMoveCreate`](tests.c.driver.md#testMoveCreate)  (Implementation)


---
### testMoveFromUci<!-- {{#callable_declaration:testMoveFromUci}} -->
Test the conversion of UCI strings to move objects.
- **Description**: This function is used to verify that UCI (Universal Chess Interface) strings are correctly converted into move objects within the chess implementation. It should be called during the testing phase to ensure that the move conversion logic is functioning as expected. The function does not take any parameters and does not return a value. It is intended to be used as part of a suite of tests to validate the chess engine's move handling capabilities.
- **Inputs**: None
- **Output**: None
- **See also**: [`testMoveFromUci`](tests.c.driver.md#testMoveFromUci)  (Implementation)


---
### testMoveGetUci<!-- {{#callable_declaration:testMoveGetUci}} -->
Tests the conversion of chess moves to UCI notation.
- **Description**: This function is used to verify that the conversion of chess moves to UCI (Universal Chess Interface) notation is performed correctly. It is a part of a suite of tests for a chess implementation in C. The function checks specific move scenarios, including normal moves and promotion moves, to ensure that the UCI strings generated match the expected values. This function is intended for use in a testing environment and should be called when validating the correctness of move-to-UCI conversion functionality.
- **Inputs**: None
- **Output**: None
- **See also**: [`testMoveGetUci`](tests.c.driver.md#testMoveGetUci)  (Implementation)


---
### testMoveList<!-- {{#callable_declaration:testMoveList}} -->
Tests the functionality of move list operations.
- **Description**: This function is designed to test the creation, addition, retrieval, and validation of moves within a move list in a chess implementation. It creates a move list, adds several moves to it, retrieves them, and checks their correctness by comparing their UCI (Universal Chess Interface) string representations against expected values. This function is useful for ensuring that the move list operations are functioning correctly and that moves are stored and retrieved accurately. It should be used in a testing environment where the correctness of move handling is critical. The function will halt the program if any discrepancies are found, indicating a failure in the move list operations.
- **Inputs**: None
- **Output**: None
- **See also**: [`testMoveList`](tests.c.driver.md#testMoveList)  (Implementation)


---
### testBoardCreate<!-- {{#callable_declaration:testBoardCreate}} -->
Validates the initial state of a newly created chess board.
- **Description**: This function is used to verify that a newly created chess board is initialized correctly according to standard chess rules. It checks that all pieces are in their correct starting positions, the current player is set to white, all castling rights are enabled, the en passant target square is invalid, the half-move clock is set to zero, and the move number is set to one. This function is typically used in a testing context to ensure that the board creation logic is functioning as expected. It will halt the program if any of these conditions are not met.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardCreate`](tests.c.driver.md#testBoardCreate)  (Implementation)


---
### testBoardCreateFromFen<!-- {{#callable_declaration:testBoardCreateFromFen}} -->
Tests the creation of a chess board from a FEN string.
- **Description**: This function is used to verify that a chess board can be correctly initialized from a given FEN (Forsyth-Edwards Notation) string. It checks that the board's pieces, current player, castling rights, en passant target square, half-move clock, and full move number are set as expected. This function is typically used in a testing context to ensure that the board creation logic is functioning correctly. It is important to note that this function will halt the program if the board is not created correctly or if any of the assertions fail.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardCreateFromFen`](tests.c.driver.md#testBoardCreateFromFen)  (Implementation)


---
### testBoardEq<!-- {{#callable_declaration:testBoardEq}} -->
Fails the test for board equality.
- **Description**: This function is intended to test the equality of two chess boards, but it currently fails the test and halts the program with a message indicating that it is not yet implemented. It is a placeholder for future implementation and should not be used in its current state for any testing purposes.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardEq`](tests.c.driver.md#testBoardEq)  (Implementation)


---
### testPawnMoves<!-- {{#callable_declaration:testPawnMoves}} -->
Tests the functionality of pawn move generation in various board scenarios.
- **Description**: This function is used to verify the correctness of pawn move generation in a chess game implementation. It sets up different board scenarios using the Forsyth-Edwards Notation (FEN) and checks the generated pawn moves against expected results. The function covers scenarios such as pawns on their starting rank, pawns with capture opportunities, blocked pawns, promotion possibilities, and en passant captures. It is intended to be used in a testing environment to ensure that the pawn move generation logic is functioning as expected. The function does not return any value and is expected to halt the program if any test fails.
- **Inputs**: None
- **Output**: None
- **See also**: [`testPawnMoves`](tests.c.driver.md#testPawnMoves)  (Implementation)


---
### testKnightMoves<!-- {{#callable_declaration:testKnightMoves}} -->
Tests the generation of legal knight moves on a chessboard.
- **Description**: This function is used to verify the correctness of knight move generation in a chess implementation. It sets up various board positions with knights and checks if the generated moves match the expected legal moves for those positions. This function is typically used in a testing environment to ensure that the knight move generation logic is functioning correctly. It assumes that the board and move list management functions are working as expected and does not return any value or modify any input parameters.
- **Inputs**: None
- **Output**: None
- **See also**: [`testKnightMoves`](tests.c.driver.md#testKnightMoves)  (Implementation)


---
### testBishopMoves<!-- {{#callable_declaration:testBishopMoves}} -->
Tests the move generation for bishops on a chessboard.
- **Description**: This function is used to verify the correctness of bishop move generation in a chess implementation. It sets up specific board positions and checks that the generated moves for a bishop match the expected set of moves. This function is typically used during development to ensure that the bishop move generation logic is functioning correctly. It is expected to be called in a testing environment where the program can be halted if the test fails. The function does not return any value or modify any input parameters.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBishopMoves`](tests.c.driver.md#testBishopMoves)  (Implementation)


---
### testRookMoves<!-- {{#callable_declaration:testRookMoves}} -->
Tests the move generation for rooks on a chessboard.
- **Description**: This function is used to verify the correctness of rook move generation in a chess implementation. It sets up specific board positions and checks that the generated moves for a rook match the expected legal moves. This function is typically used during development to ensure that the move generation logic for rooks is functioning correctly. It is not intended for use in production code, but rather as part of a test suite to validate the chess engine's behavior.
- **Inputs**: None
- **Output**: None
- **See also**: [`testRookMoves`](tests.c.driver.md#testRookMoves)  (Implementation)


---
### testQueenMoves<!-- {{#callable_declaration:testQueenMoves}} -->
Tests the move generation for a queen on a chessboard.
- **Description**: This function is used to verify the correctness of move generation for a queen piece on a chessboard. It sets up specific board positions and checks that the generated moves for a queen match the expected set of moves. This function is typically used in a testing context to ensure that the move generation logic for queens is functioning correctly. It assumes that the board and move generation functions are correctly implemented and available. The function does not return any value but will halt the program if the test conditions are not met.
- **Inputs**: None
- **Output**: None
- **See also**: [`testQueenMoves`](tests.c.driver.md#testQueenMoves)  (Implementation)


---
### testKingMoves<!-- {{#callable_declaration:testKingMoves}} -->
Tests the generation of king moves on a chess board.
- **Description**: This function is used to verify the correctness of king move generation in a chess game implementation. It sets up various board positions and checks if the generated moves for the king are as expected. This function is useful for ensuring that the move generation logic for the king is functioning correctly, including edge cases such as the king being in a corner or surrounded by other pieces. It is important to note that the function does not consider whether the king's moves place it in check, as the underlying move generation function does not account for move legality in terms of check.
- **Inputs**: None
- **Output**: None
- **See also**: [`testKingMoves`](tests.c.driver.md#testKingMoves)  (Implementation)


---
### testIsSquareAttacked<!-- {{#callable_declaration:testIsSquareAttacked}} -->
Tests if squares on a chess board are correctly identified as attacked.
- **Description**: This function is used to verify the correctness of the boardIsSquareAttacked function by setting up specific board positions and checking if the function correctly identifies attacked squares. It is intended for use in a testing environment to ensure that the logic for determining attacked squares is functioning as expected. The function sets up various board scenarios using the Forsyth-Edwards Notation (FEN) and compares the actual results of boardIsSquareAttacked against expected outcomes. It is crucial for validating the accuracy of attack detection in a chess engine.
- **Inputs**: None
- **Output**: None
- **See also**: [`testIsSquareAttacked`](tests.c.driver.md#testIsSquareAttacked)  (Implementation)


---
### testIsInCheck<!-- {{#callable_declaration:testIsInCheck}} -->
Tests if a chess board is correctly identified as being in check.
- **Description**: This function is used to verify the correctness of check detection logic in a chess board implementation. It sets up various board states using the Forsyth-Edwards Notation (FEN) and checks if the board is correctly identified as being in check or not. This function is intended for use in a testing environment to ensure that the check detection functions, such as `boardIsInCheck` and `boardIsPlayerInCheck`, behave as expected under different scenarios. It is crucial for validating the integrity of the chess engine's check detection capabilities.
- **Inputs**: None
- **Output**: None
- **See also**: [`testIsInCheck`](tests.c.driver.md#testIsInCheck)  (Implementation)


---
### testBoardPlayMove<!-- {{#callable_declaration:testBoardPlayMove}} -->
Tests the functionality of playing moves on a chess board.
- **Description**: This function is used to verify the correctness of move execution on a chess board by simulating various chess scenarios, including standard moves, captures, castling, and en passant. It ensures that the board state after each move matches the expected state, as represented by FEN strings. This function is typically called during the testing phase to validate the move execution logic of a chess engine. It is important to ensure that the board is correctly initialized and that the move logic is implemented accurately before using this function.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardPlayMove`](tests.c.driver.md#testBoardPlayMove)  (Implementation)


---
### testBoardGenerateMoves<!-- {{#callable_declaration:testBoardGenerateMoves}} -->
Tests the move generation functionality of a chess board.
- **Description**: This function is used to verify the correctness of move generation in a chess board implementation. It performs a series of tests on different board states to ensure that the generated moves match expected results. This function is typically used during development to validate that the move generation logic is functioning correctly. It is important to run this test after any changes to the move generation code to ensure no regressions have been introduced. The function does not take any parameters and does not return a value, as it is intended solely for testing purposes.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardGenerateMoves`](tests.c.driver.md#testBoardGenerateMoves)  (Implementation)


---
### testBoardGenerateMovesCastling<!-- {{#callable_declaration:testBoardGenerateMovesCastling}} -->
Tests castling move generation in various board scenarios.
- **Description**: This function is used to verify the correct generation of castling moves under different board conditions in a chess game. It should be called to ensure that the move generation logic correctly handles castling rights, checks, and other constraints that affect castling. The function simulates various board states and checks if the expected castling moves are present or absent in the generated move list. It is intended for use in a testing environment to validate the chess engine's handling of castling rules.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardGenerateMovesCastling`](tests.c.driver.md#testBoardGenerateMovesCastling)  (Implementation)


---
### testBoardGetFen<!-- {{#callable_declaration:testBoardGetFen}} -->
Tests the FEN string generation functionality of the chess board.
- **Description**: This function is used to verify that the chess board's FEN (Forsyth-Edwards Notation) string generation is functioning correctly. It is intended for use in a testing environment to ensure that the board can accurately represent its state in FEN format. The function does not take any parameters and does not return a value. It is expected to be called within a test suite where the board's FEN generation is being validated against known FEN strings. The function will halt the program if the FEN generation does not match the expected values, indicating a failure in the test.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardGetFen`](tests.c.driver.md#testBoardGetFen)  (Implementation)


---
### testBoardIsInsufficientMaterial<!-- {{#callable_declaration:testBoardIsInsufficientMaterial}} -->
Tests the board state for draw conditions due to insufficient material.
- **Description**: This function is used to verify that a chess board state is correctly identified as a draw due to insufficient material. It sets up various board configurations and checks if the function responsible for detecting insufficient material correctly identifies these scenarios. This function is typically used in a testing environment to ensure the accuracy of the insufficient material detection logic. It should be called when validating the draw detection capabilities of a chess engine or application.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardIsInsufficientMaterial`](tests.c.driver.md#testBoardIsInsufficientMaterial)  (Implementation)


---
### testBoardList<!-- {{#callable_declaration:testBoardList}} -->
Tests the functionality of board list operations.
- **Description**: This function is used to verify the correct behavior of board list operations, including creation, addition, retrieval, and freeing of board objects within a list. It ensures that boards can be added to a list and retrieved in the correct order, and that the list and its contents are properly freed. This function is typically used in a testing environment to validate the integrity of board list management in a chess application.
- **Inputs**: None
- **Output**: None
- **See also**: [`testBoardList`](tests.c.driver.md#testBoardList)  (Implementation)


---
### testSqSetSet<!-- {{#callable_declaration:testSqSetSet}} -->
Tests the functionality of setting squares in a square set.
- **Description**: This function is used to verify that the `sqSetSet` function correctly sets specific squares in a square set represented by a 64-bit integer. It is intended for use in a testing environment to ensure that the `sqSetSet` function behaves as expected when setting various squares. The function checks multiple scenarios by setting different squares and comparing the resulting square set against expected values. If any of the checks fail, the function calls `failTest` to indicate a failure in the test.
- **Inputs**: None
- **Output**: None
- **See also**: [`testSqSetSet`](tests.c.driver.md#testSqSetSet)  (Implementation)


---
### testSqSetGet<!-- {{#callable_declaration:testSqSetGet}} -->
Tests the functionality of retrieving square set values.
- **Description**: This function is used to verify the correctness of the square set retrieval logic in a chess implementation. It checks whether specific squares on a chessboard, represented by a bitboard, are correctly identified as being set or not. The function is intended to be used in a testing context to ensure that the square set retrieval function, `sqSetGet`, behaves as expected for various board configurations. It is important to call this function in a controlled test environment where the results can be validated and any discrepancies can be addressed.
- **Inputs**: None
- **Output**: None
- **See also**: [`testSqSetGet`](tests.c.driver.md#testSqSetGet)  (Implementation)


