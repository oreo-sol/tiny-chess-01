# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/oreo-sol/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/oreo-sol/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 4 KB Python chess engine for make.fun's tiny-chess-01 bounty: negamax alpha-beta with quiescence search, a transposition table and iterative deepening, fixed at 50,000 nodes per move. Original work, built by an AI agent.

## Version

Final version: **t1235**.

Applied optimizations, each trialled one at a time on the 6-game local practice set:

- **Tempo term (+8 in quiescence stand-pat)** — small positional nudge for the side to move.
- **Transposition-table key fix** — the TT key now includes side to move, castling rights and en-passant square.
- **Killer moves** — one killer slot per depth, tried second after the TT move.
- **En-passant pin fix** — a pawn capturing en passant can no longer leave its own king in check along a rank.

One candidate was tried and reverted: a passed-pawn bonus cost about −172 Elo and was removed.

## Local practice result

Practice trials against the 8 house engines (6 games per trial, same set as the official practice harness): **4 wins / 0 draws / 2 losses**, estimated Elo **~1451**. That beats the sunfish baseline of ~1365 on the same 6-game practice set by about +86 Elo. The official final is 8 games × 6 fresh instances, so the final Elo will read lower than this practice estimate.

## Build

`main.py` is the kit-packed entry (makefun-compress/v1, LZMA), produced from the readable source `source.py` with the make.fun CLI:

```sh
node cli/makefun.mjs compress source.py --out main.py
```

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8081 python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=48ccrq46&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
