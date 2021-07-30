![Unit tests and puzzles](https://github.com/healeycodes/andoma/workflows/Unit%20tests%20and%20puzzles/badge.svg)

# ♟ Enisa

<br>

A chess engine which implements:
- [Alpha-beta pruning](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) for move searching
- [Move ordering](https://www.chessprogramming.org/Move_Ordering) based off heuristics like captures and promotions
- Tomasz Michniewski's [Simplified Evaluation Function](https://www.chessprogramming.org/Simplified_Evaluation_Function) for board evaluation and piece-square tables
- A slice of the Universal Chess Interface (UCI) to allow challenges via lichess.org
- A command-line user interface

It uses Python 3.8 with type hints as well as unit + integration tests. Mypy checks type hints as part of the GitHub Actions CI pipeline.

<br>

## Install

`pip install -r requirements.txt`

<br>

## Use it via command-line

Start the engine with:

`python ui.py`

```bash
Start as [w]hite or [b]lack:
w

  8 ♖ ♘ ♗ ♕ ♔ ♗ ♘ ♖
  7 ♙ ♙ ♙ ♙ ♙ ♙ ♙ ♙
  6 · · · · · · · ·
  5 · · · · · · · ·
  4 · · · · · · · ·
  3 · · · · · · · ·
  2 ♟ ♟ ♟ ♟ ♟ ♟ ♟ ♟
  1 ♜ ♞ ♝ ♛ ♚ ♝ ♞ ♜
    a b c d e f g h

Enter a move like g1h3:
```

<br>

## Use it as a UCI engine

Start the engine with:

`python main.py`

An example interaction with the engine (responses have `#`):

```bash
uci
# id name Enisa
# id author Enisalmis
# uciok
position startpos moves e2e4
go
# bestmove g8f6
```

Also accepts a FEN string:

`position fen rnbqk1nr/p1ppppbp/1p4p1/8/2P5/2Q5/PP1PPPPP/RNB1KBNR b KQkq - 0 1`

<br>

See the [UCI interface doc](https://github.com/healeycodes/andoma/blob/main/uci-interface.md) for more information on communicating with the engine.

Debug information (the number of positions searched, the time taken) is sent to stderr. The engine's response is sent to stdout.

<br>

## Lichess.org

The UCI protocol slice that's implemented by this engine means you can play it via lichess.org by using [ShailChoksi/lichess-bot](https://github.com/ShailChoksi/lichess-bot) (a bridge between Lichess API and chess engines) and a BOT account.

The engine file required by `lichess-bot` may be generated using [pyinstaller](https://www.pyinstaller.org/).

<br>

## Tests

There are unit tests for the engine, UI, and evaluation modules. Mate-in-two/mate-in-three puzzles are being added.

`python -m unittest discover test/`

Type hints:

`pip install -r requirements-dev.txt`

`mypy .`
