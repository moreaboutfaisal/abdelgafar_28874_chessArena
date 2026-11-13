| # | Source (APA) | Type | Link | Key finding | Gap it shows |
|---|--------------|------|------|-------------|--------------|

| 1 | Lichess. (n.d.). Standard chess games [Data set]. Hugging Face. https://huggingface.co/datasets/Lichess/standard-chess-games | Dataset | https://huggingface.co/datasets/Lichess/standard-chess-games | Open game records with player ratings, results and dates; licence CC0 (public domain); about 7.14 billion games | Raw game data only: no tournament rules, pairing, or rule enforcement; usernames are public handles, so they need anonymising |

| 2 | Glickman, M. E., & Jones, A. C. (1999). Rating the chess rating system. Chance, 12, 21–28. | Research paper | https://www.glicko.net/research/chance.pdf | Elo predicts game results from the rating difference and updates ratings with a factor K, but tests on 225,621 games show it overestimates the higher-rated player | The paper analyses the rating system statistically; it does not implement it in a database that enforces tournament rules and logs changes |
