# Purpose
This C source code file provides functionality for handling chess pieces within a chess library. It defines several functions that operate on a custom data type, `piece`, which likely represents a chess piece with both type and color attributes. The file includes functions to determine the type and color of a piece ([`pieceGetType`](#pieceGetType) and [`pieceGetColor`](#pieceGetColor)), convert a piece type to its corresponding letter representation ([`pieceTypeGetLetter`](#pieceTypeGetLetter)), and obtain the letter representation of a piece considering its color ([`pieceGetLetter`](#pieceGetLetter)). Additionally, it includes a function to create a piece given its type and color ([`pieceMake`](#pieceMake)). The code is structured to handle both white and black pieces, and it uses enumerations or constants such as `pWPawn`, `pBPawn`, `ptPawn`, `pcWhite`, and `pcBlack` to represent different piece types and colors.

The file is part of a broader chess library, as indicated by the inclusion of "chesslib/piece.h", suggesting that it is intended to be used as a component within a larger chess application. The functions defined here provide a narrow but essential functionality focused on the representation and manipulation of chess pieces, which is a fundamental aspect of any chess-related software. The code does not define public APIs or external interfaces directly but rather implements the logic that would be used by other parts of the chess library or application to manage chess pieces effectively.
# Imports and Dependencies

---
- `ctype.h`
- `chesslib/piece.h`


# Functions

---
### pieceGetType<!-- {{#callable:pieceGetType}} -->
The function `pieceGetType` determines the type of a chess piece from its encoded value.
- **Inputs**:
    - `p`: An encoded value representing a chess piece, which includes both type and color information.
- **Control Flow**:
    - Check if the piece `p` is greater than or equal to `pBPawn`, indicating it is a black piece.
    - If true, adjust `p` by subtracting `pBPawn` and adding 1 to normalize it to a type value.
    - Cast the adjusted or original `p` to `pieceType` and return it.
- **Output**:
    - The function returns a `pieceType`, which is an enumeration representing the type of the chess piece (e.g., pawn, knight, bishop, etc.).


---
### pieceGetColor<!-- {{#callable:pieceGetColor}} -->
The function `pieceGetColor` determines the color of a chess piece based on its enumeration value.
- **Inputs**:
    - `p`: An enumeration value representing a chess piece, which can be a white or black piece, or an invalid piece.
- **Control Flow**:
    - Check if the piece `p` is within the range of white pieces (`pWPawn` to `pWKing`); if true, return `pcWhite`.
    - Check if the piece `p` is within the range of black pieces (`pBPawn` to `pBKing`); if true, return `pcBlack`.
    - If neither condition is met, return `pcNoColor` indicating the piece has no valid color.
- **Output**:
    - The function returns a `pieceColor` enumeration value, which can be `pcWhite`, `pcBlack`, or `pcNoColor`.


---
### pieceTypeGetLetter<!-- {{#callable:pieceTypeGetLetter}} -->
The function `pieceTypeGetLetter` returns the corresponding character representation of a chess piece type.
- **Inputs**:
    - `pe`: A `pieceType` enumeration value representing the type of a chess piece.
- **Control Flow**:
    - The function uses a switch statement to determine the character representation based on the `pieceType` value `pe`.
    - If `pe` is `ptPawn`, it returns 'P'.
    - If `pe` is `ptKnight`, it returns 'N'.
    - If `pe` is `ptBishop`, it returns 'B'.
    - If `pe` is `ptRook`, it returns 'R'.
    - If `pe` is `ptQueen`, it returns 'Q'.
    - If `pe` is `ptKing`, it returns 'K'.
    - If `pe` is `ptEmpty`, it returns a space character ' '.
    - For any other value of `pe`, it returns 0.
- **Output**:
    - The function returns a `char` representing the letter associated with the given `pieceType`, or 0 if the type is unrecognized.


---
### pieceGetLetter<!-- {{#callable:pieceGetLetter}} -->
The function `pieceGetLetter` returns the character representation of a chess piece, adjusting for color by converting to lowercase if the piece is black.
- **Inputs**:
    - `p`: A `piece` type representing a chess piece, which includes both type and color information.
- **Control Flow**:
    - Call `pieceGetType(p)` to determine the type of the piece `p`.
    - Call `pieceTypeGetLetter()` with the result from `pieceGetType(p)` to get the character representation of the piece type.
    - Check the color of the piece using `pieceGetColor(p)`.
    - If the piece color is `pcBlack`, convert the character to lowercase using `tolower()`.
    - Return the character representation of the piece.
- **Output**:
    - The function returns a `char` representing the piece type, in uppercase for white pieces and lowercase for black pieces.
- **Functions called**:
    - [`pieceTypeGetLetter`](#pieceTypeGetLetter)
    - [`pieceGetType`](#pieceGetType)
    - [`pieceGetColor`](#pieceGetColor)


---
### pieceMake<!-- {{#callable:pieceMake}} -->
The `pieceMake` function creates a chess piece based on the specified type and color, returning an empty piece if the color is invalid or the type is unrecognized.
- **Inputs**:
    - `type`: The type of the chess piece, represented by the `pieceType` enum, such as ptKing, ptQueen, etc.
    - `color`: The color of the chess piece, represented by the `pieceColor` enum, such as pcWhite or pcBlack.
- **Control Flow**:
    - Check if the color is neither pcWhite nor pcBlack; if so, return pEmpty.
    - Use a switch statement to determine the piece type.
    - For each case in the switch statement (ptKing, ptQueen, ptRook, ptBishop, ptKnight, ptPawn), return the corresponding piece for the given color (white or black).
    - If the type does not match any case, return pEmpty.
- **Output**:
    - The function returns a `piece` which is a specific chess piece corresponding to the given type and color, or pEmpty if the color is invalid or the type is unrecognized.


