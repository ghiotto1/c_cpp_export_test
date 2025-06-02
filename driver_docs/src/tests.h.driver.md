# Purpose
This C header file is designed for testing various components of a chess game implementation. It declares a series of functions that are used to validate different aspects of the chess program, such as board creation, move generation, and piece movement. The file includes functions for testing specific chess functionalities, including square properties, move creation and conversion, board state management, and special conditions like castling and draw by insufficient material. Additionally, it provides a mechanism to fail tests with an optional message, ensuring that any discrepancies in expected behavior can be identified and addressed. This file is essential for maintaining the integrity and correctness of the chess application by systematically verifying its components.
# Function Declarations (Public API)

---
### failTest<!-- {{#callable_declaration:failTest}} -->
Fails the current test and terminates the program.
- **Description**: Use this function to immediately fail the currently running test and halt the program execution. It is typically used in a testing environment to indicate that a test has encountered a critical failure. The function outputs a failure message to the standard error stream, which includes the name of the current test and an optional custom message. If the `msg` parameter is `NULL`, only the test name is included in the output. This function will terminate the program using `exit(1)`, so it should be used when no further execution is desired after a test failure.
- **Inputs**:
    - `msg`: A pointer to a null-terminated string containing a custom failure message. If `NULL`, no custom message is included in the output. The caller retains ownership of the string, and it must be a valid pointer or `NULL`.
- **Output**: None
- **See also**: [`failTest`](tests.c.driver.md#failTest)  (Implementation)


---
### validateString<!-- {{#callable_declaration:validateString}} -->
Compares two strings and fails the test if they are not equal.
- **Description**: This function is used to compare two strings, `actual` and `expected`, during testing. It is typically called within a test case to ensure that the `actual` string matches the `expected` string. If the strings are not equal, the function constructs a detailed error message and calls `failTest` to fail the current test and halt the program. This function should be used when string equality is a critical condition for the test's success. It is important to note that the function will terminate the program if the strings do not match, so it should be used with caution in test environments.
- **Inputs**:
    - `actual`: A pointer to a null-terminated string representing the actual value obtained during the test. Must not be null.
    - `expected`: A pointer to a null-terminated string representing the expected value to compare against. Must not be null.
- **Output**: None
- **See also**: [`validateString`](tests.c.driver.md#validateString)  (Implementation)


---
### testSqI<!-- {{#callable_declaration:testSqI}} -->
Tests the square indexing function for correctness.
- **Description**: This function is used to verify the correctness of the square indexing function `sqI` by iterating over all possible chessboard squares and checking if the function returns the expected file and rank. It is intended to be used in a testing environment to ensure that the `sqI` function behaves as expected. If a discrepancy is found between the expected and actual values, the test fails and halts the program, providing a message with the details of the failure. This function should be called in a controlled testing setup where such halts are manageable.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testSqI`](tests.c.driver.md#testSqI)  (Implementation)


---
### testSqS<!-- {{#callable_declaration:testSqS}} -->
Tests the conversion of chess square strings to square objects.
- **Description**: This function is used to verify that the conversion from chess square notation strings (e.g., "a1", "h8") to square objects is functioning correctly. It iterates over all possible squares on a standard 8x8 chessboard, converting each square's string representation to a square object and checking if the resulting object's file and rank match the expected values. If any conversion does not match the expected result, the test fails and halts execution with an error message. This function is typically used in a testing environment to ensure the correctness of the square conversion logic.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testSqS`](tests.c.driver.md#testSqS)  (Implementation)


---
### testSqGetStr<!-- {{#callable_declaration:testSqGetStr}} -->
Tests the string representation of chessboard squares.
- **Description**: This function is used to verify that the string representation of each square on a chessboard is correctly generated. It iterates over all possible squares on an 8x8 chessboard, constructs the expected string representation for each square, and validates it against the actual string returned by the `sqGetStr` function. This function is typically used in a testing context to ensure the correctness of the `sqGetStr` function, and it assumes that the `validateString` function will handle any discrepancies by failing the test.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testSqGetStr`](tests.c.driver.md#testSqGetStr)  (Implementation)


---
### testSqIsDark<!-- {{#callable_declaration:testSqIsDark}} -->
Tests if the function correctly identifies dark squares on a chessboard.
- **Description**: This function is used to verify the correctness of the `sqIsDark` function, which determines whether a given square on a chessboard is dark. It iterates over all squares on a standard 8x8 chessboard, checking if the `sqIsDark` function returns the expected result for each square. The test expects the squares to alternate between dark and light, starting with a dark square at a1. If a discrepancy is found between the actual and expected results, the test fails and halts execution, providing a descriptive error message. This function is typically used during development to ensure the `sqIsDark` function behaves as intended.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testSqIsDark`](tests.c.driver.md#testSqIsDark)  (Implementation)


---
### testMoveCreate<!-- {{#callable_declaration:testMoveCreate}} -->
Tests the creation and validation of chess moves.
- **Description**: This function is used to test the creation of chess moves and their validation within a chess implementation. It is intended to ensure that moves are correctly created and validated according to expected parameters. This function is typically used during the development and testing phase to verify that move creation and validation logic is functioning as intended. It does not take any parameters and does not return any values, as it is designed to be a self-contained test that will halt the program if a test fails.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testMoveCreate`](tests.c.driver.md#testMoveCreate)  (Implementation)


---
### testMoveFromUci<!-- {{#callable_declaration:testMoveFromUci}} -->
Tests the conversion of UCI strings to move objects.
- **Description**: This function is used to verify that UCI (Universal Chess Interface) strings are correctly converted into move objects within the chess implementation. It is intended for use in a testing environment to ensure that the conversion process produces the expected results. The function does not take any parameters and does not return a value. It is typically called as part of a suite of tests to validate the correctness of move creation from UCI strings. The function assumes that the necessary chess data structures and functions are available and correctly implemented.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testMoveFromUci`](tests.c.driver.md#testMoveFromUci)  (Implementation)


---
### testMoveGetUci<!-- {{#callable_declaration:testMoveGetUci}} -->
Validates the UCI string representation of chess moves.
- **Description**: This function is used to test the correctness of the UCI (Universal Chess Interface) string representation of chess moves. It is intended for use in a testing environment to ensure that the conversion of move objects to their UCI string format is accurate. The function performs validation by comparing the generated UCI string against expected values. It is typically used during the development and testing of a chess engine to verify that move encoding is functioning as expected. This function should be called in a controlled test environment where the test framework can handle any failures.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testMoveGetUci`](tests.c.driver.md#testMoveGetUci)  (Implementation)


---
### testMoveList<!-- {{#callable_declaration:testMoveList}} -->
Tests the functionality of move list operations.
- **Description**: This function is used to verify the correct behavior of move list operations in a chess implementation. It creates a list of moves, adds several moves to the list, retrieves them, and checks their correctness by comparing their UCI (Universal Chess Interface) string representations against expected values. This function is typically used in a testing environment to ensure that move list creation, addition, retrieval, and UCI conversion are functioning as expected. It is important to call this function in a controlled test environment as it will halt the program if any test fails.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testMoveList`](tests.c.driver.md#testMoveList)  (Implementation)


---
### testBoardCreate<!-- {{#callable_declaration:testBoardCreate}} -->
Tests the creation of a chess board and its initial state.
- **Description**: This function is used to verify that a newly created chess board is initialized correctly with all pieces in their standard starting positions. It checks that the board's initial state matches the expected configuration for a new game, including piece placement, current player, castling rights, en passant target, half-move clock, and move number. This function is typically used in a testing environment to ensure that the board creation logic is functioning as intended. It is important to call this function in a controlled test setup where the program can handle test failures appropriately.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardCreate`](tests.c.driver.md#testBoardCreate)  (Implementation)


---
### testBoardCreateFromFen<!-- {{#callable_declaration:testBoardCreateFromFen}} -->
Tests the creation of a chess board from a FEN string.
- **Description**: This function is used to verify that a chess board can be correctly initialized from a given FEN (Forsyth-Edwards Notation) string. It checks that the board is set up with the correct pieces in their respective positions, the current player to move, castling rights, en passant target square, half-move clock, and full move number. This function is typically used in a testing environment to ensure that the board creation logic is functioning as expected. It is important to call this function in a controlled test environment where the program can be halted if the test fails.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardCreateFromFen`](tests.c.driver.md#testBoardCreateFromFen)  (Implementation)


---
### testBoardEq<!-- {{#callable_declaration:testBoardEq}} -->
Fails the test for board equality.
- **Description**: This function is intended to test the equality of two chess boards, but it is currently not implemented. When called, it will immediately fail the test and halt the program with a message indicating that the functionality is not yet implemented. This function is a placeholder and should be completed to perform actual board equality testing in the future.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardEq`](tests.c.driver.md#testBoardEq)  (Implementation)


---
### testPawnMoves<!-- {{#callable_declaration:testPawnMoves}} -->
Tests the move generation for pawns in various board scenarios.
- **Description**: This function is used to verify the correctness of pawn move generation in a chess game implementation. It sets up different board positions using the Forsyth-Edwards Notation (FEN) and checks the generated moves for pawns in various scenarios, including starting positions, capturing moves, blocked paths, promotion opportunities, and en passant captures. This function is intended for use in a testing environment to ensure that pawn moves are generated accurately according to chess rules. It must be called in a context where the board and move list management functions are available and properly initialized.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testPawnMoves`](tests.c.driver.md#testPawnMoves)  (Implementation)


---
### testKnightMoves<!-- {{#callable_declaration:testKnightMoves}} -->
Tests the generation of legal knight moves on a chessboard.
- **Description**: This function is used to verify the correctness of knight move generation in a chess implementation. It sets up various board positions with knights and checks if the generated moves match the expected legal moves for those positions. This function is typically used in a testing environment to ensure that the knight move generation logic is functioning correctly. It assumes that the board and move list management functions are working as expected and does not handle any errors or invalid inputs explicitly.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testKnightMoves`](tests.c.driver.md#testKnightMoves)  (Implementation)


---
### testBishopMoves<!-- {{#callable_declaration:testBishopMoves}} -->
Tests the move generation for bishops on a chessboard.
- **Description**: This function is used to verify the correctness of bishop move generation in a chess implementation. It sets up specific board positions and checks that the generated list of possible moves for a bishop matches the expected moves. This function is typically used during development to ensure that the bishop's movement logic is correctly implemented and handles various board scenarios, including open boards and boards with blocking pieces. It is intended to be part of a suite of tests and should be run in an environment where the chessboard and move generation functions are properly initialized and available.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBishopMoves`](tests.c.driver.md#testBishopMoves)  (Implementation)


---
### testRookMoves<!-- {{#callable_declaration:testRookMoves}} -->
Tests the move generation for rooks on a chessboard.
- **Description**: This function is used to verify the correctness of rook move generation in a chess implementation. It sets up specific board positions and checks that the generated moves for a rook match the expected legal moves. This function is typically used in a testing context to ensure that the move generation logic for rooks is functioning correctly. It assumes that the board and move generation functions are correctly implemented and available. The function does not return any value but will halt the program if a test fails, indicating an error in the move generation logic.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testRookMoves`](tests.c.driver.md#testRookMoves)  (Implementation)


---
### testQueenMoves<!-- {{#callable_declaration:testQueenMoves}} -->
Tests the move generation for a queen on a chessboard.
- **Description**: This function is used to verify the correctness of move generation for a queen piece on a chessboard. It sets up specific board positions and checks that the generated list of possible moves for a queen matches the expected moves. This function is typically used in a testing environment to ensure that the move generation logic for queens is functioning correctly. It assumes that the board and move list structures are properly initialized and that the move generation functions are correctly implemented. The function does not return any value but will halt the program if a test fails.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testQueenMoves`](tests.c.driver.md#testQueenMoves)  (Implementation)


---
### testKingMoves<!-- {{#callable_declaration:testKingMoves}} -->
Tests the generation of king moves on a chess board.
- **Description**: This function is used to verify the correctness of king move generation in a chess game implementation. It sets up various board positions and checks if the generated moves for the king are as expected. The function does not consider whether the king moves into check, as it focuses solely on the potential moves a king can make from a given position. This function is useful for ensuring that the move generation logic for the king is functioning correctly, especially in edge cases such as when the king is in a corner or surrounded by other pieces.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testKingMoves`](tests.c.driver.md#testKingMoves)  (Implementation)


---
### testIsSquareAttacked<!-- {{#callable_declaration:testIsSquareAttacked}} -->
Tests if squares are correctly identified as attacked in various board scenarios.
- **Description**: This function is used to verify the correctness of the square attack detection logic in a chess board implementation. It sets up different board configurations using the Forsyth-Edwards Notation (FEN) and checks if the function responsible for determining if a square is attacked returns the expected results. This function is typically used during the development and testing phase to ensure that the attack detection logic is functioning as intended. It is important to call this function in a controlled test environment as it will halt the program if any test fails.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testIsSquareAttacked`](tests.c.driver.md#testIsSquareAttacked)  (Implementation)


---
### testIsInCheck<!-- {{#callable_declaration:testIsInCheck}} -->
Tests if a chess board is in check under various scenarios.
- **Description**: This function is used to verify the correctness of check detection logic in a chess board implementation. It sets up different board positions using the FEN notation and checks whether the board is correctly identified as being in check or not. This function is typically used in a testing environment to ensure that the check detection functions, such as `boardIsInCheck` and `boardIsPlayerInCheck`, behave as expected. It is important to call this function in a controlled test environment where the program can be halted if a test fails, as it uses `failTest` to report errors.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testIsInCheck`](tests.c.driver.md#testIsInCheck)  (Implementation)


---
### testBoardPlayMove<!-- {{#callable_declaration:testBoardPlayMove}} -->
Tests the functionality of playing moves on a chess board.
- **Description**: This function is used to verify the correctness of move execution on a chess board within a test suite. It performs a series of predefined chess moves, including standard moves, captures, castling, and en passant, and checks the resulting board state against expected outcomes. This function is intended to be used in a testing environment to ensure that the move execution logic is functioning as expected. It assumes that the board and move functions are correctly implemented and available. The function does not return any value but will halt the program if a test fails, indicating an error in the move execution logic.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardPlayMove`](tests.c.driver.md#testBoardPlayMove)  (Implementation)


---
### testBoardGenerateMoves<!-- {{#callable_declaration:testBoardGenerateMoves}} -->
Tests the move generation functionality of a chess board.
- **Description**: This function is used to verify the correctness of move generation on a chess board in various scenarios, including the initial board setup, boards with some moves played, and special cases like pinned pieces and checks. It is intended for use in a testing environment to ensure that the move generation logic produces the expected results. The function does not take any parameters and does not return a value, as it is designed to validate the internal logic of the chess implementation by asserting expected outcomes. It is crucial to run this function in a controlled test environment where failures can be appropriately handled.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardGenerateMoves`](tests.c.driver.md#testBoardGenerateMoves)  (Implementation)


---
### testBoardGenerateMovesCastling<!-- {{#callable_declaration:testBoardGenerateMovesCastling}} -->
Tests castling move generation on a chess board.
- **Description**: This function is used to verify the correct generation of castling moves in various board states during a chess game. It should be called as part of a test suite to ensure that castling is correctly handled under different conditions, such as when the king or rook has moved, when the king is in check, or when squares between the king and rook are attacked. The function does not take any parameters and does not return a value, as it is intended solely for testing purposes. It assumes that the board and move generation functions are correctly implemented and available.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardGenerateMovesCastling`](tests.c.driver.md#testBoardGenerateMovesCastling)  (Implementation)


---
### testBoardGetFen<!-- {{#callable_declaration:testBoardGetFen}} -->
Tests the FEN string generation functionality of the chess board.
- **Description**: This function is used to verify that the chess board's FEN (Forsyth-Edwards Notation) string generation is functioning correctly. It is intended to be used in a testing environment where the correctness of FEN strings is critical for board state representation. The function does not take any parameters and does not return a value. It is expected to be called in a context where the board state can be validated against known FEN strings, ensuring that the board's FEN output matches expected values for various chess positions.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardGetFen`](tests.c.driver.md#testBoardGetFen)  (Implementation)


---
### testBoardIsInsufficientMaterial<!-- {{#callable_declaration:testBoardIsInsufficientMaterial}} -->
Tests the board state for insufficient material draw conditions.
- **Description**: This function is used to verify that a chess board correctly identifies draw conditions due to insufficient material. It should be called during testing to ensure that the board's logic for detecting insufficient material is functioning as expected. The function sets up various board states and checks if they are correctly identified as insufficient material scenarios, which are situations where neither player can checkmate the other with the available pieces. This function is part of a suite of tests and should be used in a controlled testing environment.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardIsInsufficientMaterial`](tests.c.driver.md#testBoardIsInsufficientMaterial)  (Implementation)


---
### testBoardList<!-- {{#callable_declaration:testBoardList}} -->
Tests the functionality of board list operations.
- **Description**: This function is used to verify the correct behavior of board list operations in a chess implementation. It creates a series of chess board states, adds them to a board list, and checks if they can be retrieved correctly. This function is typically used in a testing environment to ensure that the board list operations such as creation, addition, retrieval, and freeing of resources are functioning as expected. It is important to call this function in a controlled test environment as it will halt the program if any test fails.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testBoardList`](tests.c.driver.md#testBoardList)  (Implementation)


---
### testSqSetSet<!-- {{#callable_declaration:testSqSetSet}} -->
Tests the functionality of setting squares in a square set.
- **Description**: This function is used to verify that the `sqSetSet` function correctly sets specific squares in a square set represented by a 64-bit integer. It is intended for use in a testing environment to ensure that the `sqSetSet` function behaves as expected when setting various squares on a chessboard. The function will halt the program and report an error if any of the test cases fail, indicating that the square setting functionality is not working correctly. This function should be used in a controlled testing environment where the program can be safely halted for debugging purposes.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testSqSetSet`](tests.c.driver.md#testSqSetSet)  (Implementation)


---
### testSqSetGet<!-- {{#callable_declaration:testSqSetGet}} -->
Tests the functionality of square set operations.
- **Description**: This function is used to verify the correctness of square set operations in a chess implementation. It checks whether specific squares on a chessboard are correctly identified as being part of a set, based on predefined patterns. This function is typically used during the development and testing phase to ensure that the square set operations behave as expected. It is important to call this function in a controlled test environment, as it will halt the program if any discrepancies are found between expected and actual results.
- **Inputs**:
    - None
- **Output**: None
- **See also**: [`testSqSetGet`](tests.c.driver.md#testSqSetGet)  (Implementation)


