# ChessArena Rwanda: Tournament Pairing, Elo Rating and Fair-Play Monitor

- **Student:** Abdelgafar Faisal Abdelgafar
- **Student ID:** 28874
- **Course:** INSY 8311 – Database Development with PL/SQL (Final Exam, Capstone Project)
- **Instructor:** Eric Maniraguha
- **Academic year:** 2026–2027 (Semester I)

## Problem Statement
Organizers of small chess tournaments in Rwanda (clubs, schools, universities) often pair players and update ratings by hand, in notebooks or spreadsheets. This leads to repeated pairings, wrong results, inconsistent ratings and disputes between players. There is no central record that enforces the tournament rules.

## Proposed Solution
ChessArena is an Oracle database with PL/SQL that registers players and tournaments, generates Swiss-system pairings for each round, records game results and recalculates Elo ratings automatically. Business rules are enforced inside the database by procedures and triggers, and every rejected action is written to an audit log.

## Objectives
**Main objective:** Build an Oracle PL/SQL database that automates pairing, result recording and Elo rating for chess tournaments while enforcing fair-play rules.

**Specific objectives:**
1. Store players, tournaments, rounds and games in a normalized (3NF) schema.
2. Generate Swiss-system pairings per round without repeating opponents.
3. Calculate and update Elo ratings automatically after every recorded result.
4. Block rule violations (repeat pairings, editing a closed round) and record them in an audit log.
5. Provide a simple interface where organizers record results and view the leaderboard.

## Data Source
Lichess standard chess games (Hugging Face), open game data used as the real dataset:
https://huggingface.co/datasets/Lichess/standard-chess-games

- A sample of several thousand games will be used (not the full dataset).
- Player usernames will be replaced by anonymous player IDs.
- Licence to be confirmed on the dataset card before loading.

## Innovation
**Option:** User interface.
**Tool:** Streamlit (Python), connected live to the Oracle database through python-oracledb. The app calls PL/SQL procedures (for example `record_result` and `generate_pairings`) and shows the live leaderboard. Business rules stay in PL/SQL; the app only displays data and calls procedures.

## Planned Tables
| Table | Purpose |
|---|---|
| PLAYERS | Registered players and their current Elo rating |
| TOURNAMENTS | Tournament name, dates, number of rounds, status |
| ENTRIES | Players registered in a tournament and their points |
| ROUNDS | Rounds of a tournament and whether each is open or closed |
| GAMES | Pairings and results (white, black, result) |
| RATING_HISTORY | Rating before and after each game |
| AUDIT_LOG | Every blocked or changed action, with user and time |

## Planned PL/SQL Features
| Feature | Where it is used |
|---|---|
| Function `calc_new_rating` | Computes the new Elo rating after a game |
| Procedure `generate_pairings` (with cursor) | Pairs players with similar points in each round |
| Procedure `record_result` | Saves a result and updates ratings and points |
| Trigger | Blocks pairing two players who already played each other in the tournament |
| Trigger | Blocks changing a result in a closed round and logs the attempt |
| Exception handling | Rejects invalid results and unregistered players |
| Package `chess_pkg` | Groups the functions and procedures above |

## References
Lichess. (n.d.). *Standard chess games* [Data set]. Hugging Face. https://huggingface.co/datasets/Lichess/standard-chess-games

Glickman, M. E., & Jones, A. C. (1999). Rating the chess rating system. *Chance*, *12*, 21–28.

*Full source list with key findings: see `docs/research/research_log.md`.*

## References

Führlich, P., Cseh, Á., & Lenzner, P. (2021). *Improving ranking quality and fairness in Swiss-system chess tournaments* (arXiv:2112.10522). arXiv. https://arxiv.org/pdf/2112.10522v1

Glickman, M. E., & Jones, A. C. (1999). Rating the chess rating system. *Chance, 12*, 21–28. https://www.glicko.net/research/chance.pdf

Herzog, H. (n.d.). *Swiss-Manager* [Computer software]. German Chess Federation. https://www.schachbund.de/bundles/contaolinkscollection/go.php?id=2227

Lichess. (n.d.). *Standard chess games* [Data set]. Hugging Face. https://huggingface.co/datasets/Lichess/standard-chess-games

Oracle. (n.d.). *Trigger restrictions*. In *Oracle Database PL/SQL language reference* (19c). https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/trigger-restrictions.html

Rwanda Chess Confederation. (2020). *Appendix C – Key performance indicators: National Chess Federation Rwanda, period 2019* [Report]. FIDE. https://pdc.fide.com/wp-content/uploads/2020/02/Rwanda_final.pdf

Full source list with key findings and gaps: see [`docs/research/research_log.md`](docs/research/research_log.md).
