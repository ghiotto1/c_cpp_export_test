# Purpose
This C header file defines enumerations and function prototypes related to chess pieces, serving as a foundational component for a chess program. It includes three enumerations: `pieceType`, which categorizes the types of chess pieces (e.g., pawn, knight, bishop); `piece`, which represents specific pieces with color differentiation (e.g., white pawn, black knight); and `pieceColor`, which specifies the color of a piece (white or black). The file also declares several functions that operate on these enumerations, such as [`pieceGetType`](#pieceGetType) and [`pieceGetColor`](#pieceGetColor), which extract the type and color from a `piece`, and [`pieceMake`](#pieceMake), which constructs a `piece` from a given type and color. This header file is essential for managing and manipulating chess pieces within a larger chess application.
# Data Structures

---
### pieceType
- **Type**: `enum`
- **Members**:
    - `ptEmpty`: Represents an empty square or no piece.
    - `ptPawn`: Represents a pawn piece.
    - `ptKnight`: Represents a knight piece.
    - `ptBishop`: Represents a bishop piece.
    - `ptRook`: Represents a rook piece.
    - `ptQueen`: Represents a queen piece.
    - `ptKing`: Represents a king piece.
- **Description**: The `pieceType` enumeration defines the different types of chess pieces that can exist on a chessboard, including an empty square. Each enumerator corresponds to a specific type of piece, such as a pawn, knight, bishop, rook, queen, or king, allowing for easy identification and manipulation of chess pieces within a program.


---
### piece
- **Type**: `enum`
- **Members**:
    - `pEmpty`: Represents an empty square on the chessboard.
    - `pWPawn`: Represents a white pawn piece.
    - `pWKnight`: Represents a white knight piece.
    - `pWBishop`: Represents a white bishop piece.
    - `pWRook`: Represents a white rook piece.
    - `pWQueen`: Represents a white queen piece.
    - `pWKing`: Represents a white king piece.
    - `pBPawn`: Represents a black pawn piece.
    - `pBKnight`: Represents a black knight piece.
    - `pBBishop`: Represents a black bishop piece.
    - `pBRook`: Represents a black rook piece.
    - `pBQueen`: Represents a black queen piece.
    - `pBKing`: Represents a black king piece.
- **Description**: The `piece` enum defines constants for each type of chess piece, including both white and black pieces, as well as an empty square. It is used to represent the state of a chessboard in a program, allowing for easy identification and manipulation of chess pieces based on their type and color.


---
### pieceColor
- **Type**: `enum`
- **Members**:
    - `pcNoColor`: Represents a piece with no color.
    - `pcWhite`: Represents a white-colored piece.
    - `pcBlack`: Represents a black-colored piece.
- **Description**: The `pieceColor` enum is used to define the color of a chess piece, with possible values indicating no color, white, or black. This enumeration is part of a chess program and helps in distinguishing between different colored pieces on the board.


# Function Declarations (Public API)

---
### pieceGetType<!-- {{#callable_declaration:pieceGetType}} -->
Returns the type of a given chess piece.
- **Description**: This function determines the type of a chess piece based on its enumeration value. It is useful for identifying the kind of piece (e.g., pawn, knight) from a given piece enumeration, which includes both white and black pieces. The function expects a valid piece enumeration value as input, and it correctly maps black pieces to their corresponding type by adjusting their enumeration value. It should be used when the specific type of a piece is needed, regardless of its color.
- **Inputs**:
    - `p`: An enumeration value of type `piece` representing a chess piece. It must be a valid value from the `piece` enum, including both white and black pieces. Invalid values may lead to undefined behavior.
- **Output**: The function returns a `pieceType` enumeration value corresponding to the type of the input piece, such as `ptPawn`, `ptKnight`, etc.
- **See also**: [`pieceGetType`](../../src/chesslib/piece.c.driver.md#pieceGetType)  (Implementation)


---
### pieceGetColor<!-- {{#callable_declaration:pieceGetColor}} -->
Returns the color of a given chess piece.
- **Description**: Use this function to determine the color of a specified chess piece. It is useful when you need to differentiate between white and black pieces in a chess game. The function expects a valid piece enumeration value as input and returns the corresponding color. If the piece is not recognized as either white or black, the function returns a value indicating no color. This function is typically used in chess game logic to handle piece-specific operations based on color.
- **Inputs**:
    - `p`: A value of type `piece` representing a chess piece. It must be a valid enumeration value within the defined range of pieces. If the value does not correspond to a recognized piece, the function will return `pcNoColor`.
- **Output**: Returns a `pieceColor` value indicating the color of the piece: `pcWhite` for white pieces, `pcBlack` for black pieces, and `pcNoColor` if the piece does not have a recognized color.
- **See also**: [`pieceGetColor`](../../src/chesslib/piece.c.driver.md#pieceGetColor)  (Implementation)


---
### pieceTypeGetLetter<!-- {{#callable_declaration:pieceTypeGetLetter}} -->
Returns the character representation of a chess piece type.
- **Description**: This function provides a character representation for a given chess piece type, which can be useful for displaying or logging purposes. It maps each piece type to a specific character: 'P' for pawn, 'N' for knight, 'B' for bishop, 'R' for rook, 'Q' for queen, 'K' for king, and a space character for an empty piece type. If the input does not match any defined piece type, the function returns a null character. This function should be used when a textual representation of a piece type is needed, and it assumes that the input is a valid `pieceType` enumeration value.
- **Inputs**:
    - `pe`: The chess piece type to be converted to a character. It must be a valid `pieceType` enumeration value. If the value is not recognized, the function returns a null character.
- **Output**: Returns a character corresponding to the given piece type, or a null character if the piece type is not recognized.
- **See also**: [`pieceTypeGetLetter`](../../src/chesslib/piece.c.driver.md#pieceTypeGetLetter)  (Implementation)


---
### pieceGetLetter<!-- {{#callable_declaration:pieceGetLetter}} -->
Returns the character representation of a chess piece.
- **Description**: This function provides the character representation of a given chess piece, which is useful for displaying the piece in a user interface or for debugging purposes. The character returned corresponds to the type of the piece, with uppercase letters representing white pieces and lowercase letters representing black pieces. The function assumes that the input is a valid piece enumeration value. It should be used in contexts where the piece's type and color need to be represented as a single character.
- **Inputs**:
    - `p`: A piece enumeration value representing a chess piece. It must be a valid value from the 'piece' enum, and the function does not handle invalid values.
- **Output**: A character representing the piece, with uppercase for white pieces and lowercase for black pieces.
- **See also**: [`pieceGetLetter`](../../src/chesslib/piece.c.driver.md#pieceGetLetter)  (Implementation)


---
### pieceMake<!-- {{#callable_declaration:pieceMake}} -->
Create a chess piece of a specified type and color.
- **Description**: This function constructs a chess piece based on the specified type and color. It is used to initialize or create a piece for a chess game, ensuring that the piece is valid by checking the color and type. If the color is not valid (neither white nor black), or if the type is not recognized, the function returns an empty piece. This function is useful for setting up a chessboard or managing game state where specific pieces need to be instantiated.
- **Inputs**:
    - `type`: Specifies the type of the chess piece to create. Must be one of the defined pieceType values (e.g., ptPawn, ptKnight). If an unrecognized type is provided, the function returns an empty piece.
    - `color`: Specifies the color of the chess piece. Must be either pcWhite or pcBlack. If an invalid color is provided, the function returns an empty piece.
- **Output**: Returns a piece of the specified type and color, or pEmpty if the inputs are invalid.
- **See also**: [`pieceMake`](../../src/chesslib/piece.c.driver.md#pieceMake)  (Implementation)


