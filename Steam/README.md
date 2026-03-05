[![Awesome](https://raw.githubusercontent.com/ayriva/ayriva.github.io/refs/heads/main/img/steam2.png)](https://github.com/ayriva/Power_BI/blob/main/Steam/steam_games.pdf)

# Steam - Gaming Market Analysis
Power BI project analyzing the PC gaming market using Steam games data from years 2010 - 2025.

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

## Dashboard Components
The dashboard includes the following components:
- **Month Filter**: Dropdown to select the analysis period.
- **KPIs**:
  - Total sales, orders, and quantity sold with month-over-month comparisons.
- **Sales by Date**: Line chart showing daily sales trends with an average sales line.
- **Sales by Week**: Donut chart showing the split between weekdays and weekends.
- **Sales by Product Category**:
  - Bar chart displaying sales across categories like coffee, tea, bakery, etc.
- **Sales by Product Type**:
  - Detailed breakdown of sales by specific product types.
- **Sales by Store Location**:
  - Comparison of sales across different store locations with month-over-month differences.
- **Sales by Day and Hour**:
  - Heatmap showing sales patterns across days of the week and hours of the day.
