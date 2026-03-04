# Steam - Gaming Market Analysis
Power BI project analyzing the PC gaming market using Steam games data from years 2010 - 2025.

## Overview
The dashboard focuses on game releases, popularity, pricing models, player engagement, user sentiment, playtime behavior, platforms, and publisher performance.

It allows filtering by Release Year, Price, Genre, Estimated Owners, Positive/Negative Rating, Peak CCU, Average/Median Playtime, Platform, Publisher to explore different market segments.

## Dataset
Fields used in the dashboard:
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

## DAX - Key Metrics Used

- Total Games → COUNTROWS(games)
- Avg Price → AVERAGE(games[Price])
- Avg User Score:
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
- Avg Playtime → AVERAGE(games[Average playtime forever])
