# tiny-chess-01 entry — 4KB Python chess engine

A complete chess engine in a single `main.py` of 4,064 bytes (competition limit: 4,096).

## How it works

`main.py` is a self-extracting bundle: it lzma-decompresses and execs the engine source. The engine is a 0x88-board alpha-beta searcher with:

- iterative deepening with a fixed 50,000-node budget (deterministic — no clock, no unseeded randomness)
- principal variation search + transposition table
- check extensions and quiescence search (captures + check evasions)
- material + piece-square evaluation with formula-generated tables and an endgame king-table switch

It plays through the make.fun environment protocol: it reads `MAKEFUN_ENV_URL`, requests games with POST /game and answers with POST /move until all games are done.

## Build note

The engine was written as a readable `engine.py` (~10.4 KB) in the recorded build sessions and packed into `main.py` by a small `pack.py` script (strip blank/comment lines, lzma preset 9 extreme, base85). The readable sources were removed from the final tree only to satisfy the competition's 8 KB total-repo cap; the full build is preserved in the session bundle submitted with this entry.

License: MIT
