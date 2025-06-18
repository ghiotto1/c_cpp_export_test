# Purpose
This C source code file is a comprehensive test suite for a chess implementation. It is designed to validate the functionality of various components of a chess library, including squares, moves, move lists, boards, piece movements, and more. The file includes a [`main`](#main) function that sequentially runs a series of test functions, each of which is responsible for testing specific aspects of the chess library. The tests cover a wide range of scenarios, such as move creation, board setup from FEN strings, move generation, castling, en passant, and draw conditions due to insufficient material.

The file imports several headers from the chess library, indicating that it is intended to be used as a standalone executable to verify the correctness of the library's functionality. The test functions utilize helper functions like [`failTest`](#failTest) and [`validateString`](#validateString) to assert expected outcomes and halt execution upon failure. The code is structured to ensure that each component of the chess library behaves as expected, providing a robust framework for regression testing and quality assurance of the chess implementation.
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
The `main` function runs a series of predefined tests for various components of a chess implementation and reports success if all tests pass.
- **Inputs**:
    - `argc`: The number of command-line arguments passed to the program.
    - `argv`: An array of strings representing the command-line arguments.
- **Control Flow**:
    - The function begins by running a series of test functions related to chess squares using the `RUN_TEST` macro.
    - It continues by running test functions related to chess moves, move lists, and board creation and manipulation.
    - The function then tests piece-specific move generation for pawns, knights, bishops, rooks, queens, and kings.
    - It proceeds to test functions related to checking if squares are attacked and if a player is in check.
    - The function tests the ability to play moves on the board, including special moves like castling and en passant.
    - It generates and verifies moves for the board, including castling conditions.
    - The function tests the generation of FEN strings from board states and checks for draw conditions due to insufficient material.
    - It tests the functionality of board lists and square sets.
    - Finally, if all tests pass, it prints a success message and returns 0.
- **Output**: The function returns an integer, 0, indicating successful execution if all tests pass.


---
### failTest<!-- {{#callable:failTest}} -->
The `failTest` function logs a failure message for the current test and terminates the program.
- **Inputs**:
    - `msg`: A constant character pointer to a message string that provides additional information about the test failure; it can be NULL if no additional message is needed.
- **Control Flow**:
    - Check if the input message `msg` is NULL.
    - If `msg` is NULL, print a failure message to the standard error stream with the current test name.
    - If `msg` is not NULL, print a failure message to the standard error stream with the current test name and the provided message.
    - Terminate the program with an exit status of 1.
- **Output**: The function does not return a value; it exits the program with a status code of 1.


---
### validateString<!-- {{#callable:validateString}} -->
The `validateString` function compares two strings and triggers a test failure if they are not identical.
- **Inputs**:
    - `actual`: A pointer to the actual string that needs to be validated.
    - `expected`: A pointer to the expected string that the actual string is compared against.
- **Control Flow**:
    - The function begins by comparing the `actual` and `expected` strings using `strcmp`.
    - If the strings are not equal, it calculates the lengths of both strings using `strlen`.
    - It allocates memory for a new string that will hold a formatted error message.
    - The error message is created using `sprintf`, indicating the mismatch between the actual and expected strings.
    - The [`failTest`](#failTest) function is called with the error message, which exits the program, so the subsequent `free` call is not executed.
- **Output**: The function does not return a value; it exits the program if the strings do not match.
- **Functions called**:
    - [`failTest`](#failTest)


---
### testSqI<!-- {{#callable:testSqI}} -->
The `testSqI` function verifies that the [`sqI`](chesslib/square.c.driver.md#sqI) function correctly maps file and rank inputs to a square structure with matching file and rank values.
- **Inputs**: None
- **Control Flow**:
    - Iterates over ranks from 1 to 8.
    - For each rank, iterates over files from 1 to 8.
    - Calls [`sqI`](chesslib/square.c.driver.md#sqI) with the current file and rank to get a square `s`.
    - Checks if the file and rank of `s` match the current file and rank.
    - If they do not match, constructs an error message and calls [`failTest`](#failTest) with this message.
- **Output**: The function does not return a value; it either completes successfully or calls [`failTest`](#failTest) to indicate a failure.
- **Functions called**:
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`failTest`](#failTest)


---
### testSqS<!-- {{#callable:testSqS}} -->
The `testSqS` function tests the conversion of chess square strings to square structures and verifies their correctness.
- **Inputs**: None
- **Control Flow**:
    - Iterates over ranks from 1 to 8.
    - For each rank, iterates over files from 1 to 8.
    - Constructs a string representation of the square using the file and rank.
    - Calls the [`sqS`](chesslib/square.c.driver.md#sqS) function to convert the string to a square structure.
    - Checks if the converted square's file and rank match the expected values.
    - If there is a mismatch, constructs an error message and calls [`failTest`](#failTest) to halt the test.
- **Output**: The function does not return a value; it halts the program if a test fails.
- **Functions called**:
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`failTest`](#failTest)


---
### testSqGetStr<!-- {{#callable:testSqGetStr}} -->
The `testSqGetStr` function tests the conversion of chessboard square coordinates to their string representation and validates the output against expected values.
- **Inputs**: None
- **Control Flow**:
    - Iterates over all possible ranks (1 to 8) and files (1 to 8) on a chessboard.
    - For each combination of rank and file, it creates a square using the [`sqI`](chesslib/square.c.driver.md#sqI) function.
    - Generates the expected string representation of the square using the file and rank values.
    - Calls [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr) to get the actual string representation of the square.
    - Validates the actual string against the expected string using [`validateString`](#validateString).
- **Output**: The function does not return any value; it validates the correctness of the [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr) function by comparing its output to expected values.
- **Functions called**:
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`validateString`](#validateString)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)


---
### testSqIsDark<!-- {{#callable:testSqIsDark}} -->
The `testSqIsDark` function verifies that each square on a chessboard is correctly identified as dark or light by the [`sqIsDark`](chesslib/square.c.driver.md#sqIsDark) function.
- **Inputs**: None
- **Control Flow**:
    - Initialize `expectedIsDark` to 1, assuming the square a1 is dark.
    - Iterate over each rank from 1 to 8.
    - For each rank, iterate over each file from 1 to 8.
    - For each square, create a square object `s` using `sqI(file, rank)`.
    - Determine if the square `s` is dark using `sqIsDark(s)` and store the result in `actualIsDark`.
    - If `actualIsDark` does not match `expectedIsDark`, construct an error message and call [`failTest`](#failTest) with this message.
    - Toggle `expectedIsDark` after each file iteration to alternate between dark and light squares.
    - Toggle `expectedIsDark` after each rank iteration to maintain the checkerboard pattern.
- **Output**: The function does not return a value but will terminate the program with an error message if a test fails.
- **Functions called**:
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`sqIsDark`](chesslib/square.c.driver.md#sqIsDark)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


---
### validateMove<!-- {{#callable:validateMove}} -->
The `validateMove` function checks if a given chess move matches expected parameters and triggers a test failure if it does not.
- **Inputs**:
    - `m`: A `move` structure representing the actual move to be validated.
    - `expectedFrom`: A `sq` structure representing the expected starting square of the move.
    - `expectedTo`: A `sq` structure representing the expected ending square of the move.
    - `expectedPromotion`: A `pieceType` representing the expected promotion piece type, if any.
- **Control Flow**:
    - The function checks if the actual move's starting square, ending square, and promotion type match the expected values using logical OR to combine the conditions.
    - If any of these conditions are not met, a message is formatted with the actual and expected values using `sprintf`.
    - The [`failTest`](#failTest) function is called with the formatted message, which halts the program and indicates a test failure.
- **Output**: The function does not return a value; it either completes silently if the move is valid or halts the program with an error message if the move is invalid.
- **Functions called**:
    - [`sqEq`](chesslib/square.c.driver.md#sqEq)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


---
### testMoveCreate<!-- {{#callable:testMoveCreate}} -->
The `testMoveCreate` function tests the creation and validation of chess moves, including normal and promotion moves.
- **Inputs**: None
- **Control Flow**:
    - A move `m` is created using [`moveSq`](chesslib/move.c.driver.md#moveSq) from square (5, 8) to square (5, 7).
    - The move `m` is validated using [`validateMove`](#validateMove) to ensure it matches the expected from and to squares and has no promotion.
    - A promotion move `m` is created using [`movePromote`](chesslib/move.c.driver.md#movePromote) from square (3, 2) to square (2, 1) with a promotion to a queen.
    - The promotion move `m` is validated using [`validateMove`](#validateMove) to ensure it matches the expected from and to squares and the promotion to a queen.
- **Output**: The function does not return any output; it performs validation checks and may halt execution if a test fails.
- **Functions called**:
    - [`moveSq`](chesslib/move.c.driver.md#moveSq)
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`validateMove`](#validateMove)
    - [`movePromote`](chesslib/move.c.driver.md#movePromote)


---
### testMoveGetUci<!-- {{#callable:testMoveGetUci}} -->
The `testMoveGetUci` function tests the conversion of chess moves to UCI (Universal Chess Interface) format strings and validates the output against expected results.
- **Inputs**: None
- **Control Flow**:
    - A move `m` is created from square e8 to e7 using [`moveSq`](chesslib/move.c.driver.md#moveSq) and converted to UCI format using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci), then validated against the expected string "e8e7" using [`validateString`](#validateString).
    - Another move `m` is created from square c2 to b1 with a promotion to a queen using [`movePromote`](chesslib/move.c.driver.md#movePromote), converted to UCI format, and validated against the expected string "c2b1q".
- **Output**: The function does not return any value; it validates the correctness of UCI string conversion for specific chess moves.
- **Functions called**:
    - [`moveSq`](chesslib/move.c.driver.md#moveSq)
    - [`sqI`](chesslib/square.c.driver.md#sqI)
    - [`validateString`](#validateString)
    - [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci)
    - [`movePromote`](chesslib/move.c.driver.md#movePromote)


---
### testMoveFromUci<!-- {{#callable:testMoveFromUci}} -->
The `testMoveFromUci` function tests the conversion of UCI (Universal Chess Interface) strings into move objects and validates their correctness.
- **Inputs**: None
- **Control Flow**:
    - The function begins by calling [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci) with the string "e8e7" to create a move object `m`.
    - It then calls [`validateMove`](#validateMove) to check if the move `m` corresponds to moving from square e8 to e7 with no promotion (indicated by `ptEmpty`).
    - Next, it calls [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci) with the string "c2b1q" to create another move object `m`.
    - It calls [`validateMove`](#validateMove) again to check if this move `m` corresponds to moving from square c2 to b1 with a promotion to a queen (indicated by `ptQueen`).
- **Output**: The function does not return any value; it performs validation checks and may halt the program if a test fails.
- **Functions called**:
    - [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci)
    - [`validateMove`](#validateMove)
    - [`sqI`](chesslib/square.c.driver.md#sqI)


---
### testMoveList<!-- {{#callable:testMoveList}} -->
The `testMoveList` function tests the functionality of creating, adding, retrieving, and validating moves in a move list for a chess game.
- **Inputs**: None
- **Control Flow**:
    - Create three moves using [`moveFromUci`](chesslib/move.c.driver.md#moveFromUci) with UCI strings 'e2e4', 'e7e5', and 'e1e2'.
    - Create a new move list using [`moveListCreate`](chesslib/movelist.c.driver.md#moveListCreate).
    - Add the three moves to the move list using [`moveListAdd`](chesslib/movelist.c.driver.md#moveListAdd).
    - Retrieve the moves from the move list using [`moveListGet`](chesslib/movelist.c.driver.md#moveListGet) at indices 0, 1, and 2.
    - Convert each retrieved move to its UCI string using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci).
    - Compare each UCI string with the expected string ('e2e4', 'e7e5', 'e1e2') using `strcmp`.
    - If any comparison fails, call [`failTest`](#failTest) with a formatted error message.
    - Free the UCI strings after comparison.
    - Free the move list using [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree).
- **Output**: The function does not return any value; it performs assertions to validate the correctness of move list operations and may terminate the program if a test fails.
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
- **Output**: The function does not return a value; it exits the program if the pieces do not match.
- **Functions called**:
    - [`pieceGetLetter`](chesslib/piece.c.driver.md#pieceGetLetter)
    - [`failTest`](#failTest)


---
### testBoardCreate<!-- {{#callable:testBoardCreate}} -->
The `testBoardCreate` function verifies the correct initialization of a chess board by checking the placement of pieces, the current player, castling rights, en passant target, half-move clock, and move number.
- **Inputs**: None
- **Control Flow**:
    - Create a new board using `boardCreate()` and store it in `b`.
    - Check if the board `b` is `NULL` and fail the test if it is.
    - Verify the initial positions of white pieces on the board using [`assertPiece`](#assertPiece).
    - Verify the initial positions of white pawns on the board using a loop and [`assertPiece`](#assertPiece).
    - Verify that the middle squares are empty using a loop and [`assertPiece`](#assertPiece).
    - Verify the initial positions of black pawns on the board using a loop and [`assertPiece`](#assertPiece).
    - Verify the initial positions of black pieces on the board using [`assertPiece`](#assertPiece).
    - Check if the current player is white and fail the test if it is not.
    - Check if all castling rights are enabled and fail the test if they are not.
    - Check if the en passant target square is `SQ_INVALID` and fail the test if it is not.
    - Check if the half-move clock is 0 and fail the test if it is not, providing a detailed message.
    - Check if the move number is 1 and fail the test if it is not, providing a detailed message.
    - Free the allocated memory for the board `b`.
- **Output**: The function does not return any value; it performs assertions and may terminate the program if any test fails.
- **Functions called**:
    - [`boardCreate`](chesslib/board.c.driver.md#boardCreate)
    - [`failTest`](#failTest)
    - [`assertPiece`](#assertPiece)
    - [`sqEq`](chesslib/square.c.driver.md#sqEq)


---
### testBoardCreateFromFen<!-- {{#callable:testBoardCreateFromFen}} -->
The function `testBoardCreateFromFen` tests the creation of a chess board from a FEN string and verifies the board's state against expected values.
- **Inputs**: None
- **Control Flow**:
    - Create a board using [`boardCreateFromFen`](chesslib/board.c.driver.md#boardCreateFromFen) with a specific FEN string.
    - Check if the board creation returned a NULL pointer and fail the test if it did.
    - Iterate over all 64 squares of the board, asserting that only specific squares contain pieces, while others are empty.
    - Assert the presence of specific pieces at designated squares based on the FEN string.
    - Verify that the current player is set to black as expected.
    - Check that all castling flags are disabled.
    - Validate that the en passant target square is correctly set to e3.
    - Ensure the half-move clock is set to 0.
    - Confirm the full move number is set to 46.
    - Free the allocated board memory.
- **Output**: The function does not return any value; it performs assertions to validate the board state and fails the test if any assertion is incorrect.
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
- **Inputs**: None
- **Control Flow**:
    - The function calls [`failTest`](#failTest) with the message 'Not yet implemented', which causes the test to fail and the program to exit.
    - There is a commented-out section indicating a plan to create a board from a FEN string, but it is not executed.
- **Output**: The function does not return any value as it is a void function, and it currently only causes the program to exit with a failure message.
- **Functions called**:
    - [`failTest`](#failTest)


---
### validateUciIsInMovelist<!-- {{#callable:validateUciIsInMovelist}} -->
The `validateUciIsInMovelist` function checks if a given UCI move string is present in a move list and fails the test if it is not found.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure representing the list of moves to be checked.
    - `expectedUci`: A string representing the expected UCI move that should be present in the move list.
- **Control Flow**:
    - Iterate over each node in the move list starting from the head.
    - For each node, retrieve the UCI string of the move using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci).
    - Compare the retrieved UCI string with the expected UCI string using `strcmp`.
    - If a match is found (comparison result is 0), return from the function, indicating the move is present.
    - If the loop completes without finding a match, format an error message indicating the expected UCI was absent.
    - Call [`failTest`](#failTest) with the error message to fail the test.
- **Output**: The function does not return a value; it either returns normally if the UCI is found or calls [`failTest`](#failTest) to terminate the program if the UCI is not found.
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
    - The function compares the `size` attribute of the `list` with `expectedSize`.
    - If the sizes do not match, it formats an error message indicating the actual and expected sizes.
    - The function then calls [`failTest`](#failTest) with the formatted message to indicate a test failure and halt execution.
- **Output**: The function does not return a value; it either completes without issue or halts the program if the list size does not match the expected size.
- **Functions called**:
    - [`failTest`](#failTest)


---
### testPawnMoves<!-- {{#callable:testPawnMoves}} -->
The `testPawnMoves` function tests various scenarios of pawn movements on a chessboard, including normal moves, captures, promotions, and special moves like en passant, using a series of assertions to validate the correctness of the move generation logic.
- **Inputs**: None
- **Control Flow**:
    - Initialize a board with a lone white pawn on its starting rank and generate its possible moves, validating that it can move one or two squares forward.
    - Set up a board where a pawn can capture enemy pieces and validate that the move list includes both forward moves and captures.
    - Test a scenario where a pawn is blocked by another piece, ensuring no moves are generated.
    - Check a pawn not on its starting rank, validating it can only move one square forward.
    - Test a white pawn about to promote, ensuring all promotion options are included in the move list.
    - Set up a black pawn on its starting rank and validate it can move one or two squares forward.
    - Test a scenario where a pawn is blocked with one free spot, ensuring only the free move is generated.
    - Check a black pawn about to promote with capturing ability, validating all promotion and capture options are included.
    - Test en passant capture opportunities for both white and black pawns, ensuring the special capture move is included.
    - Free the move list and board resources after each test case.
- **Output**: The function does not return any value; it uses assertions to validate the correctness of pawn move generation logic.
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
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a lone knight at c3 and generate its moves.
    - Validate that the move list contains 8 moves and specific expected moves like 'c3d5', 'c3e4', etc.
    - Free the move list memory.
    - Initialize a chess board with a knight near the edge at h7 and generate its moves.
    - Validate that the move list contains 3 moves and specific expected moves like 'h7g5', 'h7f6', etc.
    - Free the move list memory.
    - Initialize a chess board with a knight at f6 surrounded by other pieces and generate its moves.
    - Validate that the move list contains 6 moves and specific expected moves like 'f6g8', 'f6h5', etc.
    - Free the move list memory.
- **Output**: The function does not return any value; it validates the correctness of knight move generation through assertions.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetKnightMoves`](chesslib/piecemoves.c.driver.md#pmGetKnightMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testBishopMoves<!-- {{#callable:testBishopMoves}} -->
The `testBishopMoves` function tests the move generation for a bishop in different board scenarios to ensure correctness.
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a lone bishop on e7 using FEN notation.
    - Generate all possible moves for the bishop on e7 and store them in a move list.
    - Validate that the move list contains exactly 9 moves and includes specific expected moves.
    - Free the move list to release memory.
    - Initialize a new board position with a bishop on c3 and some blocking pieces using FEN notation.
    - Generate all possible moves for the bishop on c3 and store them in a move list.
    - Validate that the move list contains exactly 5 moves and includes specific expected moves.
    - Free the move list to release memory.
- **Output**: The function does not return any value; it performs assertions to validate the correctness of bishop move generation.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetBishopMoves`](chesslib/piecemoves.c.driver.md#pmGetBishopMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testRookMoves<!-- {{#callable:testRookMoves}} -->
The `testRookMoves` function tests the generation and validation of legal moves for a rook in different board scenarios.
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a lone rook on d7 using FEN notation.
    - Generate all possible moves for the rook on d7 and store them in a move list.
    - Validate that the move list contains exactly 14 moves and includes specific expected moves like 'd7d8', 'd7e7', etc.
    - Free the move list to release memory.
    - Reinitialize the board with a more complex setup including a rook on e5 surrounded by other pieces.
    - Generate all possible moves for the rook on e5 and store them in a move list.
    - Validate that the move list contains exactly 9 moves and includes specific expected moves like 'e5e6', 'e5e7', etc.
    - Free the move list to release memory.
- **Output**: The function does not return any value; it performs assertions to validate the correctness of rook move generation and will halt execution if any test fails.
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
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a lone queen at position b2 using FEN notation.
    - Generate all possible moves for the queen at b2 and store them in a move list.
    - Validate that the move list contains exactly 23 moves and specific expected moves like b2b3, b2b4, etc.
    - Free the move list to release memory.
    - Initialize another chess board with a queen at d5 surrounded by other pieces using FEN notation.
    - Generate all possible moves for the queen at d5 and store them in a move list.
    - Validate that the move list contains exactly 11 moves and specific expected moves like d5e6, d5f7, etc.
    - Free the move list to release memory.
- **Output**: The function does not return any value; it validates the correctness of queen move generation through assertions.
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
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a lone king at position c7 and generate possible king moves using [`pmGetKingMoves`](chesslib/piecemoves.c.driver.md#pmGetKingMoves).
    - Validate that the generated move list contains 8 moves and includes specific moves like c7c8, c7d8, etc.
    - Free the move list memory after validation.
    - Initialize a chess board with a king in the corner at position a1 and generate possible king moves.
    - Validate that the generated move list contains 3 moves and includes specific moves like a1a2, a1b2, etc.
    - Free the move list memory after validation.
    - Initialize a chess board with a king surrounded by other pieces at position d5 and generate possible king moves.
    - Validate that the generated move list contains 5 moves and includes specific moves like d5e5, d5d4, etc.
    - Free the move list memory after validation.
- **Output**: The function does not return any value; it performs assertions to validate the correctness of king move generation.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`pmGetKingMoves`](chesslib/piecemoves.c.driver.md#pmGetKingMoves)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`validateListSize`](#validateListSize)
    - [`validateUciIsInMovelist`](#validateUciIsInMovelist)
    - [`moveListFree`](chesslib/movelist.c.driver.md#moveListFree)


---
### testIsSquareAttacked<!-- {{#callable:testIsSquareAttacked}} -->
The `testIsSquareAttacked` function tests whether specific squares on a chess board are correctly identified as being attacked by certain pieces.
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a knight and a pawn using FEN notation and iterate over all 64 squares to check if they are attacked by white pieces, comparing expected and actual results.
    - Initialize a chess board with a lone rook using FEN notation and iterate over all 64 squares to check if they are attacked by black pieces, comparing expected and actual results.
    - Initialize a chess board with a rook and blocking pieces using FEN notation and iterate over all 64 squares to check if they are attacked by black pieces, comparing expected and actual results.
    - If any square's expected attacked status does not match the actual attacked status, a failure message is generated and the test is failed.
- **Output**: The function does not return any value but will halt execution and print an error message if any test fails.
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
The `testIsInCheck` function tests various chess board configurations to verify if the [`boardIsInCheck`](chesslib/board.c.driver.md#boardIsInCheck) and [`boardIsPlayerInCheck`](chesslib/board.c.driver.md#boardIsPlayerInCheck) functions correctly identify when a king is in check.
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board `b` using [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace) with a FEN string representing a board where the white king is in check by a black rook.
    - Check if [`boardIsInCheck`](chesslib/board.c.driver.md#boardIsInCheck) returns true for the board `b`; if not, call [`failTest`](#failTest) with an error message.
    - Check if [`boardIsPlayerInCheck`](chesslib/board.c.driver.md#boardIsPlayerInCheck) returns false for the black player; if not, call [`failTest`](#failTest) with an error message.
    - Initialize the board `b` with a FEN string representing the Scholar's mate position where the black king is in check.
    - Check if [`boardIsInCheck`](chesslib/board.c.driver.md#boardIsInCheck) returns true for the board `b`; if not, call [`failTest`](#failTest) with an error message.
    - Check if [`boardIsPlayerInCheck`](chesslib/board.c.driver.md#boardIsPlayerInCheck) returns false for the white player; if not, call [`failTest`](#failTest) with an error message.
    - Initialize the board `b` with a FEN string where checks are blocked by knights, ensuring no king is in check.
    - Check if [`boardIsInCheck`](chesslib/board.c.driver.md#boardIsInCheck) returns false for the board `b`; if not, call [`failTest`](#failTest) with an error message.
    - Check if [`boardIsPlayerInCheck`](chesslib/board.c.driver.md#boardIsPlayerInCheck) returns false for the black player; if not, call [`failTest`](#failTest) with an error message.
- **Output**: The function does not return any value; it uses [`failTest`](#failTest) to halt execution if any test fails.
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
    - The function calls [`boardEq`](chesslib/board.c.driver.md#boardEq) to compare the two boards `b1` and `b2` for equality.
    - If the boards are not equal, it formats a message indicating the test name and that the boards were not the same.
    - The function then calls [`failTest`](#failTest) with the formatted message to indicate the test failure and halt execution.
- **Output**: The function does not return a value; it either continues execution if the boards are equal or halts the program with a failure message if they are not.
- **Functions called**:
    - [`boardEq`](chesslib/board.c.driver.md#boardEq)
    - [`failTest`](#failTest)


---
### testBoardPlayMove<!-- {{#callable:testBoardPlayMove}} -->
The `testBoardPlayMove` function tests various chess move scenarios on a board to ensure the [`boardPlayMoveInPlace`](chesslib/board.c.driver.md#boardPlayMoveInPlace) function correctly updates the board state.
- **Inputs**: None
- **Control Flow**:
    - Create a new chess board `b` using [`boardCreate`](chesslib/board.c.driver.md#boardCreate) and a check board `bCheck`.
    - Play the move 1. e4 on `b` and create a board `bCheck` from the FEN string representing the expected board state after the move.
    - Validate that `b` and `bCheck` are equal using [`validateBoardEq`](#validateBoardEq).
    - Check for fuzziness by comparing `b` with a slightly different board `bCheckFuzzy` and ensure they are not exactly equal but contextually the same.
    - Play the move 1... Nf6 on `b` and update `bCheck` to the expected state after the move, then validate equality.
    - Test capturing by setting up a board where a rook captures another rook, play the move, and validate the board state.
    - Test a bishop capturing a pawn in the opening, play the move, and validate the board state.
    - Test a series of moves leading to a draw, play each move, and validate the board state after each move.
    - Test castling moves (White O-O, Black O-O, White O-O-O, Black O-O-O), play each move, and validate the board state after each move.
    - Test en passant captures for both White and Black, play each move, and validate the board state after each move.
    - Free the memory allocated for `b` and `bCheck`.
- **Output**: The function does not return any value; it performs assertions to validate board states and will terminate the program with an error message if any test fails.
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
The function `validateUciIsNotInMovelist` checks if a given UCI string is absent from a list of moves and fails the test if it is present.
- **Inputs**:
    - `list`: A pointer to a `moveList` structure representing the list of moves to be checked.
    - `expectedUci`: A character pointer to the UCI string that is expected to be absent from the move list.
- **Control Flow**:
    - Iterate over each node in the move list starting from the head.
    - For each node, retrieve the UCI string of the move using [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci).
    - Compare the retrieved UCI string with the expected UCI string using `strcmp`.
    - Free the memory allocated for the retrieved UCI string.
    - If the strings match (comparison result is 0), construct an error message indicating the UCI string was found in the list.
    - Call [`failTest`](#failTest) with the constructed message to indicate the test failure and exit the function.
    - If the loop completes without finding a match, the function ends without any action, indicating the UCI string is not in the list.
- **Output**: The function does not return a value; it either completes silently if the UCI string is not found or calls [`failTest`](#failTest) to terminate the program if the UCI string is found.
- **Functions called**:
    - [`moveGetUci`](chesslib/move.c.driver.md#moveGetUci)
    - [`failTest`](#failTest)


---
### testBoardGenerateMoves<!-- {{#callable:testBoardGenerateMoves}} -->
The `testBoardGenerateMoves` function tests the move generation functionality of a chess board implementation by validating the generated moves against expected moves for various board states.
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board to the starting position and generate all possible moves.
    - Validate that the generated move list contains 20 moves, including all possible pawn and knight moves from the initial position.
    - Free the move list memory after validation.
    - Set up a board with a specific FEN string and generate moves, validating the expected number of moves and specific pawn, knight, bishop, queen, and king moves.
    - Free the move list memory after validation.
    - Set up a board with fewer pieces and generate moves, validating the expected number of moves and specific knight and king moves.
    - Free the move list memory after validation.
    - Set up a board with a pinned knight and generate moves, validating that only king moves are possible and the knight cannot move.
    - Free the move list memory after validation.
    - Set up a board where the king is in check and generate moves, validating that only moves that block the check are possible.
    - Free the move list memory after validation.
- **Output**: The function does not return any value; it performs assertions to validate the correctness of move generation and will terminate the program if any test fails.
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
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board with a specific FEN string and generate possible moves.
    - Validate that the expected castling move (e.g., 'e1g1' for white king-side castling) is present in the generated move list.
    - Modify the board state to remove castling rights and regenerate moves, then validate that the castling move is absent.
    - Repeat the process for black king-side castling, white queen-side castling, and black queen-side castling.
    - Test scenarios where castling is not allowed due to the king being in check or squares being attacked.
    - Free the move list after each test case to prevent memory leaks.
- **Output**: The function does not return any value; it validates the presence or absence of castling moves in the generated move list and fails the test if the validation does not meet expectations.
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
    - Generate a FEN string `actualFen` from the board `b` using [`boardGetFen`](chesslib/board.c.driver.md#boardGetFen).
    - Call [`validateString`](#validateString) to compare `actualFen` with the input `fen` to ensure they match.
    - Free the memory allocated for `actualFen`.
- **Output**: The function does not return a value; it validates the FEN string and may terminate the program if the validation fails.
- **Functions called**:
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)
    - [`boardGetFen`](chesslib/board.c.driver.md#boardGetFen)
    - [`validateString`](#validateString)


---
### testBoardGetFen<!-- {{#callable:testBoardGetFen}} -->
The function `testBoardGetFen` validates the correctness of FEN (Forsyth-Edwards Notation) string generation for various chess board states.
- **Inputs**: None
- **Control Flow**:
    - The function calls [`validateBoardFen`](#validateBoardFen) with the initial FEN string and several other FEN strings representing different chess positions.
    - Each call to [`validateBoardFen`](#validateBoardFen) checks if the FEN string generated from a board matches the expected FEN string.
- **Output**: The function does not return any value; it performs validation checks and may halt the program if a test fails.
- **Functions called**:
    - [`validateBoardFen`](#validateBoardFen)


---
### validateBoardIsInsufficientMaterial<!-- {{#callable:validateBoardIsInsufficientMaterial}} -->
The function `validateBoardIsInsufficientMaterial` checks if a chess board has insufficient material for a draw and compares the result with an expected value, failing the test if they do not match.
- **Inputs**:
    - `b`: A pointer to a `board` structure representing the current state of the chess board.
    - `expected`: A `uint8_t` value representing the expected result of whether the board is a draw by insufficient material (1 for true, 0 for false).
- **Control Flow**:
    - Call the function [`boardIsInsufficientMaterial`](chesslib/board.c.driver.md#boardIsInsufficientMaterial) with the board `b` to determine if the board is a draw by insufficient material, storing the result in `actual`.
    - Compare `actual` with `expected`.
    - If `actual` does not equal `expected`, format a message indicating the discrepancy and call [`failTest`](#failTest) with this message to halt the test.
- **Output**: The function does not return a value; it either completes successfully or calls [`failTest`](#failTest) to indicate a test failure.
- **Functions called**:
    - [`boardIsInsufficientMaterial`](chesslib/board.c.driver.md#boardIsInsufficientMaterial)
    - [`failTest`](#failTest)


---
### testBoardIsInsufficientMaterial<!-- {{#callable:testBoardIsInsufficientMaterial}} -->
The function `testBoardIsInsufficientMaterial` tests various chess board configurations to determine if they result in a draw due to insufficient material.
- **Inputs**: None
- **Control Flow**:
    - Initialize a chess board `b` using [`boardInitInPlace`](chesslib/board.c.driver.md#boardInitInPlace) and validate it is not insufficient material using [`validateBoardIsInsufficientMaterial`](#validateBoardIsInsufficientMaterial).
    - Set up a board with only kings using [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace) and validate it is insufficient material.
    - Set up a board with a king versus a king and knight, and validate it is insufficient material.
    - Set up a board with a king versus a king and two knights, and validate it is not insufficient material.
    - Set up a board with a king and bishop versus a king and bishop on different colors, and validate it is not insufficient material.
    - Set up a board with a king and bishop versus a king and bishop on the same color, and validate it is insufficient material.
    - Set up a board with multiple bishops on the same color versus a king and bishops, and validate it is insufficient material.
- **Output**: The function does not return a value; it uses assertions to validate the test cases.
- **Functions called**:
    - [`boardInitInPlace`](chesslib/board.c.driver.md#boardInitInPlace)
    - [`validateBoardIsInsufficientMaterial`](#validateBoardIsInsufficientMaterial)
    - [`boardInitFromFenInPlace`](chesslib/board.c.driver.md#boardInitFromFenInPlace)


---
### testBoardList<!-- {{#callable:testBoardList}} -->
The `testBoardList` function tests the functionality of creating, adding to, retrieving from, and freeing a list of chess boards.
- **Inputs**: None
- **Control Flow**:
    - Create a new chess board `b1` using `boardCreate()`.
    - Create a new board `b2` by playing a move on `b1` using `boardPlayMove()` with the move 'e2e4'.
    - Create another board `b3` by playing a different move on `b1` using `boardPlayMove()` with the move 'c7c5'.
    - Create a new board list `l` using `boardListCreate()`.
    - Add boards `b1`, `b2`, and `b3` to the list `l` using `boardListAdd()`.
    - Check if the first board in the list `l` is `b1` using `boardListGet()`, and call `failTest()` if it is not.
    - Check if the second board in the list `l` is `b2` using `boardListGet()`, and call `failTest()` if it is not.
    - Check if the third board in the list `l` is `b3` using `boardListGet()`, and call `failTest()` if it is not.
    - Free the board list `l` using `boardListFree()`, which also frees all boards in the list.
- **Output**: The function does not return any value; it performs assertions to ensure the board list operations are correct and calls `failTest()` if any assertion fails.
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
The function `testSqSetSet` tests the functionality of setting specific squares in a bitboard representation of a chessboard using the [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) function.
- **Inputs**: None
- **Control Flow**:
    - Initialize a 64-bit unsigned integer `ss` to 0, representing an empty bitboard.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the bit corresponding to square 'e4' in `ss` to 1, and check if `ss` equals `0x0000000010000000`; if not, call [`failTest`](#failTest) with an error message.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the bit corresponding to square 'd5' in `ss` to 1, and check if `ss` equals `0x0000000810000000`; if not, call [`failTest`](#failTest) with an error message.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the bit corresponding to square 'a1' in `ss` to 1, and check if `ss` equals `0x0000000810000001`; if not, call [`failTest`](#failTest) with an error message.
    - Call [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet) to set the bit corresponding to square 'h8' in `ss` to 1, and check if `ss` equals `0x8000000810000001`; if not, call [`failTest`](#failTest) with an error message.
- **Output**: The function does not return any value; it either completes successfully or calls [`failTest`](#failTest) to indicate a failure in setting the expected bits.
- **Functions called**:
    - [`sqSetSet`](chesslib/squareset.c.driver.md#sqSetSet)
    - [`sqS`](chesslib/square.c.driver.md#sqS)
    - [`failTest`](#failTest)


---
### testSqSetGet<!-- {{#callable:testSqSetGet}} -->
The `testSqSetGet` function tests the correctness of the [`sqSetGet`](chesslib/squareset.c.driver.md#sqSetGet) function by verifying if specific squares in a bitboard are set as expected.
- **Inputs**: None
- **Control Flow**:
    - Initialize a bitboard `ss` with a diagonal pattern from a1 to h8.
    - Iterate over all 64 squares on the board.
    - For each square, calculate the expected value based on whether the square is on the diagonal (file equals rank).
    - Retrieve the actual value from the bitboard using [`sqSetGet`](chesslib/squareset.c.driver.md#sqSetGet).
    - If the expected and actual values differ, construct an error message and call [`failTest`](#failTest) to indicate a test failure.
    - Reinitialize the bitboard `ss` to represent specific files and ranks (c file, f file, 3 rank, and 6 rank).
    - Repeat the iteration and comparison process for the new bitboard configuration.
- **Output**: The function does not return a value; it calls [`failTest`](#failTest) if any discrepancies are found between expected and actual values, which halts the program.
- **Functions called**:
    - [`sqIndex`](chesslib/square.c.driver.md#sqIndex)
    - [`sqSetGet`](chesslib/squareset.c.driver.md#sqSetGet)
    - [`sqGetStr`](chesslib/square.c.driver.md#sqGetStr)
    - [`failTest`](#failTest)


