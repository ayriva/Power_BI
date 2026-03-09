# Steam - Gaming Market Analysis
Power BI project analyzing the PC gaming market using Steam games data from years 2010 - 2025.

[![Awesome](https://raw.githubusercontent.com/ayriva/ayriva.github.io/refs/heads/main/img/steam2.png)](https://github.com/ayriva/Power_BI/blob/main/Steam/steam_games.pdf)

## Project Purpose
This dashboard is designed for exploratory analytics and gaming market insights using Power BI.

It provides a structured analytical view of the Steam gaming ecosystem, supporting:
- Market structure exploration
- Game popularity benchmarking
- Pricing strategy evaluation
- Player sentiment analysis
- Engagement measurement
- Platform distribution comparison
- Developer performance analysis

It allows to explore different market segments filtering by: Release Year, Price, Genre, Estimated Owners, Positive/Negative Rating, Peak CCU, Average/Median Playtime, Platform, Publisher.

## Dataset
CSV database, fields used in the dashboard:
- Name
- Release date
- Estimated owners (range)
- Peak CCU
- Price
- About the game
- User score
- Positive
- Negative
- Average playtime forever
- Median playtime forever
- Windows (TRUE/FALSE)
- Mac (TRUE/FALSE)
- Linux (TRUE/FALSE)
- Publishers
- Genres
- Tags
- Supported languages
- Categories

## DAX
Key Metrics Used:
- **Total Games** → COUNTROWS(games)
- **Avg Price** → AVERAGE(games[Price])
- **Avg User Score:**
`Avg User Score =
VAR Score =
    CALCULATE(
        AVERAGE(games[User score]),
        games[User score] > 0
    )
RETURN
IF(ISBLANK(Score), "0/100", FORMAT(Score, "0") & "/100")`
- Avg Peak CCU → AVERAGE(games[Peak CCU])
- Positive % → Positive / (Positive + Negative)
- Free vs Paid:
`Free Games = CALCULATE(
    COUNTROWS(games),
    games[Price] = 0 || ISBLANK(games[Price])
)`
vs `Paid Games = CALCULATE(
    COUNTROWS(games),
    games[Price] > 0
)`
- **Avg Peak CCU by Platform:** `Avg Peak CCU Windows = CALCULATE(
    AVERAGE(games[Peak CCU]),
    games[Windows] = TRUE()
)`
- **Avg Playtime** → AVERAGE(games[Average playtime forever])


