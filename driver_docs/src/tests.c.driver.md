# Purpose
This C source code file is a comprehensive test suite for a chess implementation. It is designed to validate the functionality of various components of a chess library, including squares, moves, move lists, boards, piece movements, and more. The file includes a [`main`](#main) function that sequentially runs a series of test functions, each of which is responsible for testing specific aspects of the chess library. The tests cover a wide range of scenarios, such as move creation, board setup from FEN strings, move generation, castling, en passant, and draw conditions due to insufficient material.

The file imports several headers from the chess library, indicating that it is intended to be used in conjunction with these components to ensure their correctness. The test functions utilize helper functions like [`failTest`](#failTest) and [`validateString`](#validateString) to assert expected outcomes and halt execution if a test fails. This file is not intended to be a reusable library or a public API; rather, it serves as an internal testing mechanism to verify the integrity and correctness of the chess library's functionality. The tests are thorough and cover both basic and complex chess scenarios, ensuring that the library behaves as expected under various conditions.
# Imports and Dependencies

---
- `stdio.h`
- `stdlib.h`
- `string.h`
- `tests.h`
- `chesslib/squareset.h`
- `chesslib/movelist.h`
- `chesslib/board.h`
- `chesslib/piecemoves.h`
- `chesslib/boardlist.h`


# Global Variables

---
### currTest
- **Type**: `const char*`
- **Description**: `currTest` is a global variable of type `const char*` that holds the name of the currently running test as a string. It is used to track which test is being executed at any given time during the test suite execution.
- **Use**: This variable is used to store the name of the test currently being executed, allowing for error messages to specify which test failed.


# Functions

---
### main<!-- {{#callable:main}} -->
The `main` function runs a series of predefined tests for a chess implementation and reports success if all tests pass.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of strings representing the command-line arguments passed to the program.
- **Control Flow**:
    - The function begins by running a series of test functions using the `RUN_TEST` macro, which sets the current test name and executes the test function.
    - Tests are grouped by functionality, such as square tests, move tests, board tests, piece move tests, attacked square tests, move generation tests, FEN generation tests, draw condition tests, board list tests, and square set tests.
    - Each test function is executed sequentially, and if any test fails, the program will terminate with an error message indicating the failed test.
    - If all tests pass, a success message is printed to the console.
    - The function returns 0 to indicate successful execution.
- **Output**:
    - The function returns an integer value of 0, indicating successful execution if all tests pass.


---
### failTest<!-- {{#callable:failTest}} -->
The `failTest` function logs a failure message for the current test and terminates the program.
- **Inputs**:
    - `msg`: A constant character pointer to a message string that provides additional context for the test failure; it can be NULL if no additional message is needed.
- **Control Flow**:
    - Check if the input message `msg` is NULL.
    - If `msg` is NULL, print a failure message to the standard error stream with the current test name.
    - If `msg` is not NULL, print a failure message to the standard error stream with the current test name and the provided message.
    - Terminate the program with an exit status of 1.
- **Output**:
    - The function does not return any value as it terminates the program execution.


---
### validateString<!-- {{#callable:validateString}} -->
The `validateString` function compares two strings and triggers a test failure if they are not identical.
- **Inputs**:
    - `actual`: A pointer to the actual string that needs to be validated.
    - `expected`: A pointer to the expected string that the actual string is compared against.
- **Control Flow**:
    - The function begins by comparing the `actual` and `expected` strings using `strcmp`.
    - If the strings are not equal, it calculates the lengths of both strings using `strlen`.
    - It allocates memory for a new string that will hold the error message, which includes both the actual and expected strings.
    - The error message is formatted and stored in the allocated memory using `sprintf`.
    - The [`failTest`](#failTest) function is called with the error message, which causes the program to exit.
    - The `free` function is called to deallocate the memory for the error message, although this line is not executed because [`failTest`](#failTest) exits the program.
- **Output**:
    - The function does not return a value; it exits the program if the strings do not match.
- **Functions called**:
    - [`failTest`](#failTest)


---
### testSqI<!-- {{#callable:testSqI}} -->
The `testSqI` function tests the [`sqI`](chesslib/square.c.driver.md#sqI) function to ensure it correctly maps file and rank inputs to a square structure with matching file and rank values.
- **Inputs**:
    - None
- **Control Flow**:
    - Iterates over ranks from 1 to 8.
    - For each rank, iterates over files from 1 to 8.
    - Calls [`sqI`](chesslib/square.c.driver.md#sqI) with the current file and rank to get a square `s`.
    - Checks if the file and rank of `s` match the current file and rank.
    - If they do not match, constructs an error message and calls [`failTest`](#failTest) with the message.
- **Output**:
    - The function does not return a value; it will exit the program with an error message if a test fails.
- **Functions called**:
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`failTest`](#failTest)


---
### testSqS<!-- {{#callable:testSqS}} -->
The `testSqS` function verifies that the [`sqS`](chesslib/square.c.driver.md#sqS) function correctly converts chess square strings to their corresponding `sq` structure representation.
- **Inputs**:
    - None
- **Control Flow**:
    - Iterates over all possible ranks (1 to 8) and files (1 to 8) of a chessboard.
    - For each rank and file, constructs a string representation of the square (e.g., 'a1', 'b2').
    - Calls the [`sqS`](chesslib/square.c.driver.md#sqS) function to convert the string to an `sq` structure.
    - Checks if the `sq` structure's file and rank match the expected file and rank.
    - If there is a mismatch, constructs an error message and calls [`failTest`](#failTest) to halt the test.
- **Output**:
    - The function does not return a value; it halts the program with an error message if a test fails.
- **Functions called**:
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`failTest`](#failTest)


---
### testSqGetStr<!-- {{#callable:testSqGetStr}} -->
The `testSqGetStr` function tests the conversion of chessboard square coordinates to their string representation and validates the output against expected values.
- **Inputs**:
    - None
- **Control Flow**:
    - Iterates over ranks from 1 to 8.
    - For each rank, iterates over files from 1 to 8.
    - For each file and rank combination, creates a square using `sqI(file, rank)`.
    - Generates a string representation of the square using the file and rank values.
    - Validates the string representation obtained from `sqGetStr(s)` against the expected string using [`validateString`](#validateString).
- **Output**:
    - The function does not return a value; it validates the correctness of the [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr) function by comparing its output to expected string representations of chessboard squares.
- **Functions called**:
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`validateString`](#validateString)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)


---
### testSqIsDark<!-- {{#callable:testSqIsDark}} -->
The `testSqIsDark` function verifies that each square on a chessboard is correctly identified as dark or light according to the expected pattern.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize `expectedIsDark` to 1, indicating that the first square (a1) is expected to be dark.
    - Iterate over each rank from 1 to 8.
    - For each rank, iterate over each file from 1 to 8.
    - For each square, create a square object `s` using `sqI(file, rank)`.
    - Determine if the square `s` is dark using `sqIsDark(s)` and store the result in `actualIsDark`.
    - If `actualIsDark` does not match `expectedIsDark`, construct an error message and call [`failTest`](#failTest) with this message to indicate a test failure.
    - Toggle `expectedIsDark` after each file iteration to alternate the expected color for the next square.
    - Toggle `expectedIsDark` after each rank iteration to maintain the checkerboard pattern.
- **Output**:
    - The function does not return a value but will terminate the program with an error message if a square's darkness does not match the expected pattern.
- **Functions called**:
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`sqIsDark`](chesslib/square.c.driver.md#sqIsDark)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


---
### validateMove<!-- {{#callable:validateMove}} -->
The `validateMove` function checks if a given move matches expected parameters and fails the test if it does not.
- **Inputs**:
    - `m`: The move to be validated, containing the starting square, ending square, and promotion type.
    - `expectedFrom`: The expected starting square of the move.
    - `expectedTo`: The expected ending square of the move.
    - `expectedPromotion`: The expected promotion type of the move.
- **Control Flow**:
    - Check if the starting square of the move `m` is not equal to `expectedFrom` using [`sqEq`](chesslib/square.c.driver.md#sqEq) function.
    - Check if the ending square of the move `m` is not equal to `expectedTo` using [`sqEq`](chesslib/square.c.driver.md#sqEq) function.
    - Check if the promotion type of the move `m` is not equal to `expectedPromotion`.
    - If any of the above checks fail, format a message with the actual and expected move details using `sprintf`.
    - Call [`failTest`](#failTest) with the formatted message to indicate the test failure.
- **Output**:
    - The function does not return a value; it either passes silently or calls [`failTest`](#failTest) to indicate a test failure.
- **Functions called**:
    - [`sqEq`](chesslib/square.c.driver.md#sqEq)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


---
### testMoveCreate<!-- {{#callable:testMoveCreate}} -->
The `testMoveCreate` function tests the creation and validation of chess moves, including normal and promotion moves.
- **Inputs**:
    - None
- **Control Flow**:
    - Create a move `m` using [`moveSq`](chesslib/move.c.driver.md#moveSq) from square (5, 8) to square (5, 7).
    - Validate the move `m` using [`validateMove`](#validateMove) to ensure it matches the expected from and to squares and has no promotion.
    - Create a move `m` using [`movePromote`](chesslib/move.c.driver.md#movePromote) from square (3, 2) to square (2, 1) with a promotion to a queen.
    - Validate the move `m` using [`validateMove`](#validateMove) to ensure it matches the expected from and to squares and has the correct promotion to a queen.
- **Output**:
    - The function does not return any output; it performs validation checks and may halt execution if a test fails.
- **Functions called**:
    - [`moveSq`](chesslib/move.c.driver.md#moveSq)
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`validateMove`](#validateMove)
    - [`movePromote`](chesslib/move.c.driver.md#movePromote)


---
### testMoveGetUci<!-- {{#callable:testMoveGetUci}} -->
The `testMoveGetUci` function tests the conversion of chess moves to UCI (Universal Chess Interface) format strings.
- **Inputs**:
    - None
- **Control Flow**:
    - A move `m` is created from square e8 to e7 using [`moveSq`](chesslib/move.c.driver.md#moveSq) and its UCI string is validated against "e8e7" using [`validateString`](#validateString).
    - Another move `m` is created from square c2 to b1 with a promotion to a queen using [`movePromote`](chesslib/move.c.driver.md#movePromote), and its UCI string is validated against "c2b1q" using [`validateString`](#validateString).
- **Output**:
    - The function does not return any value; it validates the correctness of UCI string conversion for specific moves.
- **Functions called**:
    - [`moveSq`](chesslib/move.c.driver.md#moveSq)
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`validateString`](#validateString)
    - [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci)
    - [`movePromote`](chesslib/move.c.driver.md#movePromote)


---
### testMoveFromUci<!-- {{#callable:testMoveFromUci}} -->
The `testMoveFromUci` function tests the conversion of UCI (Universal Chess Interface) strings into move objects and validates their correctness.
- **Inputs**:
    - None
- **Control Flow**:
    - The function begins by creating a move object `m` from the UCI string "e8e7" using the [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci) function.
    - It then validates this move by checking if it correctly represents a move from square e8 to e7 with no promotion using the [`validateMove`](#validateMove) function.
    - Next, it creates another move object `m` from the UCI string "c2b1q", which includes a promotion to a queen.
    - It validates this move by checking if it correctly represents a move from square c2 to b1 with a promotion to a queen using the [`validateMove`](#validateMove) function.
- **Output**:
    - The function does not return any value; it performs validation checks and may halt execution if a test fails.
- **Functions called**:
    - [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci)
    - [`validateMove`](#validateMove)
    - [`sqI`](chesslib/square.c.driver.md#sqI)


---
### testMoveList<!-- {{#callable:testMoveList}} -->
The `testMoveList` function tests the functionality of creating, adding, retrieving, and validating moves in a move list for a chess game.
- **Inputs**:
    - None
- **Control Flow**:
    - Create three moves using [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci) with UCI strings 'e2e4', 'e7e5', and 'e1e2'.
    - Create a new move list using [`moveListCreate`](chesslib/movelist.c.driver.md#moveListCreate).
    - Add the three moves to the move list using [`moveListAdd`](chesslib/movelist.c.driver.md#moveListAdd).
    - Retrieve the moves from the list using [`moveListGet`](chesslib/movelist.c.driver.md#moveListGet) at indices 0, 1, and 2.
    - Convert each retrieved move to its UCI string using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci) and compare it to the expected UCI string using `strcmp`.
    - If the UCI string does not match the expected string, call [`failTest`](#failTest) with a formatted error message.
    - Free the UCI string memory after each comparison.
    - Free the move list using [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree).
- **Output**:
    - The function does not return any value but will terminate the program with an error message if any test fails.
- **Functions called**:
    - [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci)
    - [`moveListCreate`](chesslib/movelist.c.driver.md#moveListCreate)
    - [`moveListAdd`](chesslib/movelist.c.driver.md#moveListAdd)
    - [`moveListGet`](chesslib/movelist.c.driver.md#moveListGet)
    - [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci)
    - [`failTest`](#failTest)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### assertPiece<!-- {{#callable:assertPiece}} -->
The `assertPiece` function checks if two chess pieces are equal and reports an error if they are not.
- **Inputs**:
    - `actual`: The actual piece to be compared.
    - `expected`: The expected piece to be compared against.
- **Control Flow**:
    - The function compares the `actual` piece with the `expected` piece using the `!=` operator.
    - If the pieces are not equal, it retrieves the letter representation of both pieces using [`pieceGetLetter`](chesslib/piece.c.driver.md#pieceGetLetter).
    - It formats a message indicating the mismatch using `sprintf`.
    - The function then calls [`failTest`](#failTest) with the formatted message to report the error and halt the program.
- **Output**:
    - The function does not return a value; it halts the program if the pieces do not match.
- **Functions called**:
    - [`pieceGetLetter`](chesslib/piece.c.driver.md#pieceGetLetter)
    - [`failTest`](#failTest)


---
### testBoardCreate<!-- {{#callable:testBoardCreate}} -->
The `testBoardCreate` function tests the creation of a chess board and verifies its initial setup and state.
- **Inputs**:
    - None
- **Control Flow**:
    - Create a new board using `boardCreate()` and store it in `b`.
    - Check if the board `b` is `NULL` and fail the test if it is.
    - Verify the initial positions of white pieces (rooks, knights, bishops, queen, king, and pawns) on the board using [`assertPiece`](#assertPiece).
    - Verify that the squares from index 16 to 47 are empty using [`assertPiece`](#assertPiece).
    - Verify the initial positions of black pieces (pawns, rooks, knights, bishops, queen, king) on the board using [`assertPiece`](#assertPiece).
    - Check if the current player is set to white (`pcWhite`) and fail the test if not.
    - Check if all castling flags are enabled (`0b1111`) and fail the test if not.
    - Verify that the en passant target square is `SQ_INVALID` and fail the test if not.
    - Check if the half-move clock is set to 0 and fail the test if not.
    - Check if the move number is set to 1 and fail the test if not.
    - Free the allocated memory for the board `b`.
- **Output**:
    - The function does not return any value; it performs assertions to validate the board's initial state and fails the test if any condition is not met.
- **Functions called**:
    - [`boardCreate`](chesslib/board.c.driver.md#boardCreate)
    - [`failTest`](#failTest)
    - [`assertPiece`](#assertPiece)
    - [`sqEq`](chesslib/square.c.driver.md#sqEq)


---
### testBoardCreateFromFen<!-- {{#callable:testBoardCreateFromFen}} -->
The function `testBoardCreateFromFen` tests the creation of a chess board from a FEN string and verifies the board's state against expected values.
- **Inputs**:
    - None
- **Control Flow**:
    - Call [`boardCreateFromFen`](chesslib/board.c.driver.md#boardCreateFromFen) with a specific FEN string to create a board.
    - Check if the board is NULL and fail the test if it is.
    - Iterate over all 64 squares of the board, skipping specific indices where pieces are expected, and assert that the remaining squares are empty.
    - Assert that specific squares contain the expected pieces (queens, pawns, kings).
    - Verify that the current player is black, failing the test if not.
    - Check that all castling flags are disabled, failing the test if not.
    - Verify the en passant target square is correct, failing the test if not.
    - Check that the half-move clock is zero, failing the test if not.
    - Verify the full move number is 46, failing the test if not.
    - Free the allocated board memory.
- **Output**:
    - The function does not return a value but will terminate the program with an error message if any test condition fails.
- **Functions called**:
    - [`boardCreateFromFen`](chesslib/board.c.driver.md#boardCreateFromFen)
    - [`failTest`](#failTest)
    - [`assertPiece`](#assertPiece)
    - [`sqEq`](chesslib/square.c.driver.md#sqEq)
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)


---
### testBoardEq<!-- {{#callable:testBoardEq}} -->
The `testBoardEq` function is a placeholder for a test that checks if two chess boards are equal, but it is not yet implemented.
- **Inputs**:
    - None
- **Control Flow**:
    - The function calls [`failTest`](#failTest) with the message 'Not yet implemented', which causes the test to fail and the program to exit.
    - There is a commented-out section indicating a future plan to create a board from a FEN string for comparison.
- **Output**:
    - The function does not return any value as it is intended to fail the test and exit the program.
- **Functions called**:
    - [`failTest`](#failTest)


---
### validateUciIsInMovelist<!-- {{#callable:validateUciIsInMovelist}} -->
The `validateUciIsInMovelist` function checks if a given UCI move string is present in a move list and fails the test if it is not found.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure representing the list of moves to be searched.
    - `expectedUci`: A string representing the expected UCI move that should be present in the move list.
- **Control Flow**:
    - Iterate over each node in the move list starting from the head.
    - For each node, retrieve the UCI string of the move using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci).
    - Compare the retrieved UCI string with the expected UCI string using `strcmp`.
    - If a match is found (comparison result is 0), return from the function, indicating the move is present.
    - If the loop completes without finding a match, format an error message indicating the expected UCI was absent.
    - Call [`failTest`](#failTest) with the error message to halt the test execution.
- **Output**:
    - The function does not return a value; it either returns normally if the UCI is found or calls [`failTest`](#failTest) to halt execution if the UCI is not found.
- **Functions called**:
    - [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci)
    - [`failTest`](#failTest)


---
### validateListSize<!-- {{#callable:validateListSize}} -->
The `validateListSize` function checks if a move list's size matches an expected size and triggers a test failure if they do not match.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure, which contains a list of chess moves and its current size.
    - `expectedSize`: A `size_t` value representing the expected number of elements in the move list.
- **Control Flow**:
    - The function checks if the `size` attribute of the `list` does not equal `expectedSize`.
    - If the sizes do not match, it formats an error message indicating the actual and expected sizes.
    - The function then calls [`failTest`](#failTest) with the formatted message to indicate a test failure and halt execution.
- **Output**:
    - The function does not return a value; it either completes silently if the sizes match or halts the program with an error message if they do not.
- **Functions called**:
    - [`failTest`](#failTest)


---
### testPawnMoves<!-- {{#callable:testPawnMoves}} -->
The `testPawnMoves` function tests various scenarios of pawn movements on a chessboard, including normal moves, captures, promotions, and en passant captures, using a series of assertions to validate the correctness of the move generation logic.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a board with a lone white pawn on its starting rank and generate its possible moves, validating that it can move one or two squares forward.
    - Set up a board where a pawn can capture enemy pieces diagonally and validate the possible capture moves.
    - Test a scenario where a pawn is blocked by another piece and validate that no moves are possible.
    - Place a pawn not on its starting rank and validate that it can only move one square forward.
    - Set up a board where a white pawn is about to promote and validate all possible promotion moves.
    - Test a black pawn on its starting rank and validate its possible moves, including moving two squares forward.
    - Set up a scenario where a pawn is blocked with one free spot and validate the single possible move.
    - Test a black pawn about to promote with capturing ability and validate all possible promotion and capture moves.
    - Set up a board where a white pawn can capture en passant and validate the en passant capture move.
    - Test a black pawn with an en passant capture opportunity and validate the en passant capture move.
    - Free the allocated memory for the board and move lists after each test case.
- **Output**:
    - The function does not return any value; it uses assertions to validate the correctness of pawn move generation logic in various scenarios.
- **Functions called**:
    - [`boardCreateFromFen`](chesslib/board.c.driver.md#boardCreateFromFen)
    - [`pmGetPawnMoves`](chesslib/piecemoves.c.driver.md#pmGetPawnMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)


---
### testKnightMoves<!-- {{#callable:testKnightMoves}} -->
The `testKnightMoves` function tests the generation of legal moves for a knight in various board positions.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board with a lone knight at c3 and generate its moves.
    - Validate that the move list contains 8 moves and specific expected moves from c3.
    - Free the move list.
    - Initialize a chess board with a knight near the edge at h7 and generate its moves.
    - Validate that the move list contains 3 moves and specific expected moves from h7.
    - Free the move list.
    - Initialize a chess board with a knight at f6 surrounded by other pieces and generate its moves.
    - Validate that the move list contains 6 moves and specific expected moves from f6.
    - Free the move list.
- **Output**:
    - The function does not return any value; it validates the correctness of knight move generation through assertions.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetKnightMoves`](chesslib/piecemoves.c.driver.md#pmGetKnightMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testBishopMoves<!-- {{#callable:testBishopMoves}} -->
The `testBishopMoves` function tests the move generation for bishops on a chessboard in different scenarios.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board with a lone bishop on e7 using FEN notation.
    - Generate all possible moves for the bishop on e7 and store them in a move list.
    - Validate that the move list contains exactly 9 moves and includes specific expected moves.
    - Free the move list to release memory.
    - Reinitialize the chess board with a bishop on c3 and other pieces blocking some paths using FEN notation.
    - Generate all possible moves for the bishop on c3 and store them in a move list.
    - Validate that the move list contains exactly 5 moves and includes specific expected moves.
    - Free the move list to release memory.
- **Output**:
    - The function does not return any value; it validates the correctness of bishop move generation through assertions.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetBishopMoves`](chesslib/piecemoves.c.driver.md#pmGetBishopMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testRookMoves<!-- {{#callable:testRookMoves}} -->
The `testRookMoves` function tests the move generation for rooks on a chessboard in different scenarios.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board `b` and a move list pointer `list`.
    - Set up a board with a lone rook on d7 using FEN notation and generate its possible moves.
    - Validate that the move list contains 14 moves and specific moves like 'd7d8', 'd7e7', etc.
    - Free the move list after validation.
    - Set up a more complex board with a rook on e5 surrounded by other pieces and generate its possible moves.
    - Validate that the move list contains 9 moves and specific moves like 'e5e6', 'e5e7', etc.
    - Free the move list after validation.
- **Output**:
    - The function does not return any value; it validates the correctness of rook move generation through assertions.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetRookMoves`](chesslib/piecemoves.c.driver.md#pmGetRookMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testQueenMoves<!-- {{#callable:testQueenMoves}} -->
The `testQueenMoves` function tests the move generation for a queen piece on a chessboard in different scenarios.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board with a lone queen at position b2 using FEN notation.
    - Generate all possible moves for the queen at b2 and store them in a move list.
    - Validate that the move list contains 23 moves and specific expected moves like b2b3, b2b4, etc.
    - Free the move list to release memory.
    - Initialize another chess board with a queen surrounded by other pieces at position d5 using FEN notation.
    - Generate all possible moves for the queen at d5 and store them in a move list.
    - Validate that the move list contains 11 moves and specific expected moves like d5e6, d5f7, etc.
    - Free the move list to release memory.
- **Output**:
    - The function does not return any value; it performs assertions to validate the correctness of queen move generation.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetQueenMoves`](chesslib/piecemoves.c.driver.md#pmGetQueenMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testKingMoves<!-- {{#callable:testKingMoves}} -->
The `testKingMoves` function tests the movement generation of a king piece on a chessboard in various scenarios without considering check conditions.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board with a lone king at position c7 and generate possible king moves using [`pmGetKingMoves`](chesslib/piecemoves.c.driver.md#pmGetKingMoves).
    - Validate that the generated move list contains 8 moves corresponding to all possible king moves from c7.
    - Free the move list memory.
    - Initialize a chess board with a king in the corner at position a1 and generate possible king moves.
    - Validate that the generated move list contains 3 moves corresponding to all possible king moves from a1.
    - Free the move list memory.
    - Initialize a chess board with a king surrounded by other pieces at position d5 and generate possible king moves.
    - Validate that the generated move list contains 5 moves corresponding to all possible king moves from d5.
    - Free the move list memory.
- **Output**:
    - The function does not return any value; it validates the correctness of king move generation by asserting expected move lists.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetKingMoves`](chesslib/piecemoves.c.driver.md#pmGetKingMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testIsSquareAttacked<!-- {{#callable:testIsSquareAttacked}} -->
The `testIsSquareAttacked` function tests the [`boardIsSquareAttacked`](chesslib/board.c.driver.md#boardIsSquareAttacked) function by setting up various chess board scenarios and verifying if the function correctly identifies attacked squares.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board with a knight and a pawn using FEN notation and iterate over all 64 squares to check if the expected attacked squares match the actual attacked squares as determined by [`boardIsSquareAttacked`](chesslib/board.c.driver.md#boardIsSquareAttacked).
    - Reinitialize the board with a lone rook and repeat the process of checking attacked squares for all 64 squares, comparing expected and actual results.
    - Set up a board with a rook and potential blocking or capturing pieces, and again verify the attacked status of each square against expected results.
- **Output**:
    - The function does not return a value but will call [`failTest`](#failTest) and terminate the program if any test case fails, indicating a discrepancy between expected and actual results.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`sqIndex`](chesslib/square.c.driver.md#sqIndex)
    - [`sqEq`](chesslib/square.c.driver.md#sqEq)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`boardIsSquareAttacked`](chesslib/board.c.driver.md#boardIsSquareAttacked)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


---
### testIsInCheck<!-- {{#callable:testIsInCheck}} -->
The `testIsInCheck` function tests the functionality of checking if a chess board is in check using various board configurations.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board `b` using [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace) with a FEN string representing a board where the white king is in check by a black rook.
    - Check if the board is in check using [`boardIsInCheck`](chesslib/board.c.driver.md#boardIsInCheck) and fail the test if it is not.
    - Check if the black player is in check using [`boardIsPlayerInCheck`](chesslib/board.c.driver.md#boardIsPlayerInCheck) and fail the test if it is.
    - Initialize the board `b` with a FEN string representing the Scholar's mate position and repeat the check tests for the white player.
    - Initialize the board `b` with a FEN string where checks are blocked by knights and ensure the board is not in check for both players.
- **Output**:
    - The function does not return any value but will terminate the program with an error message if any of the checks fail.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`boardIsInCheck`](chesslib/board.c.driver.md#boardIsInCheck)
    - [`failTest`](#failTest)
    - [`boardIsPlayerInCheck`](chesslib/board.c.driver.md#boardIsPlayerInCheck)


---
### validateBoardEq<!-- {{#callable:validateBoardEq}} -->
The `validateBoardEq` function checks if two chess boards are identical and fails the test with a message if they are not.
- **Inputs**:
    - `name`: A string representing the name or description of the test being performed.
    - `b1`: A pointer to the first board structure to be compared.
    - `b2`: A pointer to the second board structure to be compared.
- **Control Flow**:
    - The function calls [`boardEq`](chesslib/board.c.driver.md#boardEq) to compare the two board structures `b1` and `b2` for equality.
    - If [`boardEq`](chesslib/board.c.driver.md#boardEq) returns false, indicating the boards are not equal, a message is formatted using `sprintf` to include the provided `name` and a description of the failure.
    - The [`failTest`](#failTest) function is then called with the formatted message to indicate the test failure and halt the program.
- **Output**:
    - The function does not return a value; it either completes without issue if the boards are equal or calls [`failTest`](#failTest) to terminate the program if they are not.
- **Functions called**:
    - [`boardEq`](chesslib/board.c.driver.md#boardEq)
    - [`failTest`](#failTest)


---
### testBoardPlayMove<!-- {{#callable:testBoardPlayMove}} -->
The `testBoardPlayMove` function tests various chess move scenarios on a board to ensure correct move execution and board state validation.
- **Inputs**:
    - None
- **Control Flow**:
    - Create a new chess board `b` using `boardCreate()`.
    - Play the move 1. e4 on board `b` and create a board `bCheck` from a FEN string to represent the expected board state after the move.
    - Validate that the board `b` matches `bCheck` using [`validateBoardEq`](#validateBoardEq).
    - Check for fuzziness by comparing `b` with `bCheckFuzzy` and ensure they are not exactly equal but contextually the same.
    - Play the move 1... Nf6 on board `b` and update `bCheck` to the expected state after the move.
    - Validate the board state again using [`validateBoardEq`](#validateBoardEq).
    - Test capturing moves by setting up specific board states and playing moves like Rook captures Rook and Bishop captures Pawn.
    - Validate each board state after the move using [`validateBoardEq`](#validateBoardEq).
    - Test special moves like castling (O-O, O-O-O) and en passant captures by setting up specific board states and playing the moves.
    - Validate each board state after the move using [`validateBoardEq`](#validateBoardEq).
    - Free the memory allocated for the boards `b` and `bCheck`.
- **Output**:
    - The function does not return any value; it performs assertions to validate board states and fails the test if any validation fails.
- **Functions called**:
    - [`boardCreate`](chesslib/board.c.driver.md#boardCreate)
    - [`boardPlayMoveInPlace`](chesslib/board.c.driver.md#boardPlayMoveInPlace)
    - [`moveSq`](chesslib/move.c.driver.md#moveSq)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`boardCreateFromFen`](chesslib/board.c.driver.md#boardCreateFromFen)
    - [`validateBoardEq`](#validateBoardEq)
    - [`boardEq`](chesslib/board.c.driver.md#boardEq)
    - [`failTest`](#failTest)
    - [`boardEqContext`](chesslib/board.c.driver.md#boardEqContext)
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci)


---
### validateUciIsNotInMovelist<!-- {{#callable:validateUciIsNotInMovelist}} -->
The function `validateUciIsNotInMovelist` checks if a given UCI string is absent from a move list and fails the test if it is present.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure representing the list of moves to be checked.
    - `expectedUci`: A string representing the UCI (Universal Chess Interface) notation of the move expected to be absent from the move list.
- **Control Flow**:
    - Iterate through each node in the move list starting from the head.
    - For each node, retrieve the UCI string of the move using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci).
    - Compare the retrieved UCI string with the `expectedUci` using `strcmp`.
    - If the strings match, construct an error message indicating the presence of the move and call [`failTest`](#failTest) with this message to halt the test.
    - If the loop completes without finding a match, the function ends successfully, indicating the move is absent.
- **Output**:
    - The function does not return a value; it either completes successfully if the move is absent or calls [`failTest`](#failTest) to halt the program if the move is present.
- **Functions called**:
    - [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci)
    - [`failTest`](#failTest)


---
### testBoardGenerateMoves<!-- {{#callable:testBoardGenerateMoves}} -->
The `testBoardGenerateMoves` function tests the move generation functionality of a chess board implementation by validating the generated moves against expected moves for various board states.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board to the starting position and generate all possible moves.
    - Validate that the generated move list contains exactly 20 moves, including all possible pawn and knight moves from the initial position.
    - Free the move list to release memory.
    - Set up a board with a specific FEN string representing a mid-game position and generate all possible moves.
    - Validate the size of the move list and check for the presence of specific pawn, knight, bishop, queen, and king moves.
    - Free the move list to release memory.
    - Set up a board with fewer pieces and generate all possible moves.
    - Validate the size of the move list and check for the presence of specific knight and king moves.
    - Free the move list to release memory.
    - Set up a board with a pinned knight and generate all possible moves.
    - Validate that only king moves are present in the move list and the pinned knight cannot move.
    - Free the move list to release memory.
    - Set up a board where the king is in check and generate all possible moves.
    - Validate that the move list contains only moves that block the check or move the king out of check.
    - Free the move list to release memory.
- **Output**:
    - The function does not return any output; it performs assertions to validate the correctness of move generation and will halt execution if any test fails.
- **Functions called**:
    - [`boardInitInPlace`](chesslib/board.c.driver.md#boardInitInPlace)
    - [`boardGenerateMoves`](chesslib/board.c.driver.md#boardGenerateMoves)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`validateUciIsNotInMovelist`](#validateUciIsNotInMovelist)


---
### testBoardGenerateMovesCastling<!-- {{#callable:testBoardGenerateMovesCastling}} -->
The function `testBoardGenerateMovesCastling` tests the generation of castling moves in a chess game under various board conditions.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board with a specific FEN string and generate possible moves.
    - Validate that the castling move 'e1g1' is in the move list for White's kingside castling.
    - Remove the castling flag for White's kingside castling and validate that 'e1g1' is not in the move list.
    - Switch to Black's turn and validate that the castling move 'e8g8' is in the move list for Black's kingside castling.
    - Initialize the board for White's queenside castling and validate 'e1c1' is in the move list.
    - Switch to Black's turn and validate 'e8c8' is in the move list for Black's queenside castling.
    - Test scenarios where the king is in check or squares are attacked, ensuring castling is not allowed when it shouldn't be.
    - Free the move list after each test case to prevent memory leaks.
- **Output**:
    - The function does not return any value; it validates the presence or absence of castling moves in the generated move list and fails the test if the validation does not meet expectations.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`boardGenerateMoves`](chesslib/board.c.driver.md#boardGenerateMoves)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)
    - [`validateUciIsNotInMovelist`](#validateUciIsNotInMovelist)


---
### validateBoardFen<!-- {{#callable:validateBoardFen}} -->
The `validateBoardFen` function checks if a given FEN string correctly represents a chess board state by comparing it to the FEN string generated from the board initialized with the given FEN.
- **Inputs**:
    - `fen`: A string representing the Forsyth-Edwards Notation (FEN) of a chess board state.
- **Control Flow**:
    - Initialize a `board` structure `b`.
    - Call [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace) to set up the board `b` using the provided FEN string.
    - Generate the FEN string from the board `b` using [`boardGetFen`](chesslib/board.c.driver.md#boardGetFen).
    - Call [`validateString`](#validateString) to compare the generated FEN string with the input FEN string.
    - Free the memory allocated for the generated FEN string.
- **Output**:
    - The function does not return a value; it validates the FEN string and may terminate the program if the validation fails.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`boardGetFen`](chesslib/board.c.driver.md#boardGetFen)
    - [`validateString`](#validateString)


---
### testBoardGetFen<!-- {{#callable:testBoardGetFen}} -->
The `testBoardGetFen` function validates the correctness of FEN (Forsyth-Edwards Notation) string generation for various chess board states.
- **Inputs**:
    - None
- **Control Flow**:
    - The function calls [`validateBoardFen`](#validateBoardFen) with the initial FEN string and several other FEN strings representing different chess positions.
    - Each call to [`validateBoardFen`](#validateBoardFen) checks if the FEN string generated from a board matches the expected FEN string.
- **Output**:
    - The function does not return any value; it performs validation checks and may halt execution if a test fails.
- **Functions called**:
    - [`validateBoardFen`](#validateBoardFen)


---
### validateBoardIsInsufficientMaterial<!-- {{#callable:validateBoardIsInsufficientMaterial}} -->
The function `validateBoardIsInsufficientMaterial` checks if a chess board has insufficient material to continue the game and compares the result with an expected value, failing the test if they do not match.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess board.
    - `expected`: A `uint8_t` value representing the expected result of whether the board is a draw by insufficient material (1 for true, 0 for false).
- **Control Flow**:
    - Call the function [`boardIsInsufficientMaterial`](chesslib/board.c.driver.md#boardIsInsufficientMaterial) with the board `b` to determine if the board is a draw by insufficient material, storing the result in `actual`.
    - Compare `actual` with `expected`.
    - If `actual` does not equal `expected`, format a message indicating the discrepancy and call [`failTest`](#failTest) with this message to halt the test.
- **Output**:
    - The function does not return a value; it either completes successfully or calls [`failTest`](#failTest) to indicate a test failure.
- **Functions called**:
    - [`boardIsInsufficientMaterial`](chesslib/board.c.driver.md#boardIsInsufficientMaterial)
    - [`failTest`](#failTest)


---
### testBoardIsInsufficientMaterial<!-- {{#callable:testBoardIsInsufficientMaterial}} -->
The function `testBoardIsInsufficientMaterial` tests various chess board configurations to determine if they result in a draw due to insufficient material.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a chess board `b` using [`boardInitInPlace`](chesslib/board.c.driver.md#boardInitInPlace) and check if it is insufficient material using [`validateBoardIsInsufficientMaterial`](#validateBoardIsInsufficientMaterial) with expected result `0`.
    - Set up a board with only kings using [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace) and validate it as insufficient material with expected result `1`.
    - Set up a board with a king versus a king and knight, validate it as insufficient material with expected result `1`.
    - Set up a board with a king versus a king and two knights, validate it as not insufficient material with expected result `0`.
    - Set up a board with a king and bishop versus a king and bishop on different colors, validate it as not insufficient material with expected result `0`.
    - Set up a board with a king and bishop versus a king and bishop on the same color, validate it as insufficient material with expected result `1`.
    - Set up a board with multiple bishops on the same color versus a king and bishops, validate it as insufficient material with expected result `1`.
- **Output**:
    - The function does not return a value; it uses assertions to validate the expected outcomes of the tests.
- **Functions called**:
    - [`boardInitInPlace`](chesslib/board.c.driver.md#boardInitInPlace)
    - [`validateBoardIsInsufficientMaterial`](#validateBoardIsInsufficientMaterial)
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)


---
### testBoardList<!-- {{#callable:testBoardList}} -->
The `testBoardList` function tests the functionality of creating, adding to, retrieving from, and freeing a list of chess boards.
- **Inputs**:
    - None
- **Control Flow**:
    - Create a new board `b1` using `boardCreate()`.
    - Create a new board `b2` by playing a move on `b1` using `boardPlayMove(b1, moveFromUci("e2e4"))`.
    - Create a new board `b3` by playing a different move on `b1` using `boardPlayMove(b1, moveFromUci("c7c5"))`.
    - Create a new board list `l` using `boardListCreate()`.
    - Add `b1`, `b2`, and `b3` to the board list `l` using `boardListAdd()`.
    - Check if the first board in the list `l` is `b1` using `boardListGet(l, 0)` and call `failTest()` if not.
    - Check if the second board in the list `l` is `b2` using `boardListGet(l, 1)` and call `failTest()` if not.
    - Check if the third board in the list `l` is `b3` using `boardListGet(l, 2)` and call `failTest()` if not.
    - Free the board list `l` using `boardListFree(l)`, which also frees all boards in the list.
- **Output**:
    - The function does not return any value, but it will terminate the program with an error message if any of the tests fail.
- **Functions called**:
    - [`boardCreate`](chesslib/board.c.driver.md#boardCreate)
    - [`boardPlayMove`](chesslib/board.c.driver.md#boardPlayMove)
    - [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci)
    - [`boardListCreate`](chesslib/boardlist.c.driver.md#boardListCreate)
    - [`boardListAdd`](chesslib/boardlist.c.driver.md#boardListAdd)
    - [`boardListGet`](chesslib/boardlist.c.driver.md#boardListGet)
    - [`failTest`](#failTest)
    - [`boardListFree`](chesslib/boardlist.c.driver.md#boardListFree)


---
### testSqSetSet<!-- {{#callable:testSqSetSet}} -->
The `testSqSetSet` function tests the [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) function by setting specific squares on a bitboard and verifying the expected bitboard state.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a 64-bit integer `ss` to 0, representing an empty bitboard.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the square 'e4' on the bitboard `ss` to 1.
    - Check if `ss` equals `0x0000000010000000` and call [`failTest`](#failTest) if not.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the square 'd5' on the bitboard `ss` to 1.
    - Check if `ss` equals `0x0000000810000000` and call [`failTest`](#failTest) if not.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the square 'a1' on the bitboard `ss` to 1.
    - Check if `ss` equals `0x0000000810000001` and call [`failTest`](#failTest) if not.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the square 'h8' on the bitboard `ss` to 1.
    - Check if `ss` equals `0x8000000810000001` and call [`failTest`](#failTest) if not.
- **Output**:
    - The function does not return a value; it uses [`failTest`](#failTest) to indicate test failures.
- **Functions called**:
    - [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`failTest`](#failTest)


---
### testSqSetGet<!-- {{#callable:testSqSetGet}} -->
The `testSqSetGet` function tests the [`sqSetGet`](chesslib/squareset.c.driver.md#sqSetGet) function by verifying the correctness of square set retrieval for specific bit patterns representing chessboard squares.
- **Inputs**:
    - None
- **Control Flow**:
    - Initialize a 64-bit integer `ss` to represent a diagonal from a1 to h8 with the bit pattern `0x8040201008040201`.
    - Iterate over each square index from 0 to 63, converting each index to a square `s` using `sqIndex(i)`.
    - For each square, calculate the expected value as 1 if the square's file equals its rank, otherwise 0.
    - Retrieve the actual value from the square set using `sqSetGet(&ss, s)`.
    - If the expected value does not match the actual value, format an error message and call [`failTest`](#failTest) to indicate a test failure.
    - Reinitialize `ss` to represent the entire c file, f file, 3 rank, and 6 rank with the bit pattern `0x2424FF2424FF2424`.
    - Repeat the iteration and validation process for the new bit pattern, checking if the square's file or rank matches 3 or 6.
- **Output**:
    - The function does not return a value; it uses [`failTest`](#failTest) to halt execution if any test fails, indicating a mismatch between expected and actual values.
- **Functions called**:
    - [`sqIndex`](chesslib/square.c.driver.md#sqIndex)
    - [`sqSetGet`](chesslib/squareset.c.driver.md#sqSetGet)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


