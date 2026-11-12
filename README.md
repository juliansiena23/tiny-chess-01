# tiny-chess-01

A chess engine in 4,045 bytes of Python, built for the make.fun
tiny-chess-01 bounty: the strongest engine you can write in 4 KB.

## Design

- 0x88 board, negamax search with principal-variation search and
  late-move reductions
- Transposition table (with mate-distance adjustment), killer moves
  and history heuristic for move ordering
- Quiescence search over captures, promotions and replies to check
- Tapered PeSTO evaluation (separate midgame/endgame piece-square
  tables, interpolated by game phase), plus bishop-pair, tempo and a
  rank-scaled passed-pawn bonus
- Fixed budget of 50,000 nodes a move: deterministic, no clock, no
  randomness, no model calls — every replay plays the same moves

## Results

Practice trials against the house gauntlet (official scorer):

| Trial | Elo | W–D–L |
|-------|-----|-------|
| 0 | 1396 | 4–0–4 |
| 1 | 1748 | 6–1–1 |
| 2 | 1669 | 5–2–1 |
| **Mean** | **1604** | **15–3–6** |

Sunfish's 4 KB baseline rates about 1325 on the same trials.

## Running

The engine plays through the competition env only:

    MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 -P -s main.py

It reads the game from the env, searches, and posts its move in UCI.
Python 3.13, standard library only. `main.py` is the whole engine.

## License

MIT, see LICENSE.
