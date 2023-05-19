
## OO Design

### Symbol

Each chess piece has a specific symbol, sometimes the symbol is the same, so we build the architecture around the symbol.
There is a configuration file `symbol.json` to describe the player corresponding to the `Symbol`, as well as its action logic, etc.

### SymbolMap

The class `SymbolMap` is used to manage all `Symbol`s and establish a mapping from characters to `Symbol`s.

### Movement

It is assumed that the action logic of a `Symbol` is composed of multiple `Movement`s.
For example, the following is the `Amazon` part in the configuration file.
```json
{
    "Black": "A",
    "White": "a",
    "Piece": "Amazon",
    "Value": 12.0,
    "Sprites": "amazon",
    "Movement": [
        "knight",  // <---
        "bishop",  // <---
        "rook"     // <---
    ]
}
```
This means that `Amazon`'s movement is a combination of `KnightMovement`, `BishopMovement`, and `RookMovement`.
Obviously all of them are subclasses of `Movement`.

The class `Movement` will reveal squares which are movable, capturable and controlled.
This behavior of stripping out the action logic makes it easier for the `App` to focus on its core business.

### App

The method `App.updateBackground` calculates the color of the background uniformly after each action, so that the method `App.draw` can focus on rendering.

### UML

![UML](UML.png)

## Marking Criteria

### Final Code Submission and Demo (10%)

- [x] Window launches and shows checkerboard pattern.
- [ ] Configuration file is correctly read in – timers display correctly
- [x] Map loads and pieces are displayed in correct positions
- [x] Piece colour for player and computer is correct
- [x] Pieces are controlled by mouse clicks
    - [x] A piece can be selected – green highlight appears
    - [x] Potential moves show in blue highlights, or red for potential captures
    - [x] Clicking on a highlighted blue/red cell cause the selected piece to move to that location
    - [x] Captured pieces are deleted properly
- [x] Pieces move correctly according to the table of their movement
- [ ] Piece movement – is smooth and correct speed
- [ ] If a move causes the opponent’s king to come under attack, display “Check!” and highlight the
king’s tile in dark red.
- [ ] While the king is in check, only moves to save the king are allowed:
    - [ ] Capture the attacking piece
    - [ ] Move a piece to block
    - [ ] Move the king to a safe square
- [ ] A move that causes your own king to be in check is not allowed:
    - [x] Moving the king to a square that is under attack
    - [ ] Moving a pinned piece that was blocking an attack on the king
- [ ] Special moves: Pawn can move two squares initially, Castling, Pawn promotion to queen on the 8th rank (ie. when passing the halfway point)
- [ ] Computer AI moves automatically after the player makes their move
- [ ] Computer AI only makes legal moves
- [ ] Game ends if either player runs out of time – message is displayed correctly
- [ ] Game ends if either player is checkmated – message is displayed correctly
- [ ] Pieces contributing to checkmate have their tiles highlighted in red
- [ ] Player can resign if they want to by pressing ‘escape’
- [ ] Timer counts down and increments according to config after a move is made
- [x] Ensure that your application does not repeat large sections of logic
- [x] Ensure that your application is bug-free

### Testcases (3%)

### Design, Report, UML and Javadoc (3%)

- [x] Report, UML and OO design: 2%
- [x] Javadoc, comments, style and readability: 1%
