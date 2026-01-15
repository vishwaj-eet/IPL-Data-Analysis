# IPL Data Analysis with PySpark

## Project Overview
This project performs an in-depth analysis of Indian Premier League (IPL) cricket data using Apache Spark, specifically through its Python API, PySpark. The goal is to extract meaningful insights from various aspects of the game, including player performance, match outcomes, and team strategies.

## Datasets Used
### Dataset Link- [Download from here](https://data.world/raghu543/ipl-data-till-2017)
The analysis utilizes several CSV datasets related to IPL cricket:
-   `ball_by_ball.csv`: Contains ball-by-ball details of all matches.
-   `match.csv`: Provides general information about each match.
-   `player.csv`: Details about individual players.
-   `player_match.csv`: Player-specific performance and match-related data.
-   `team.csv`: Information about the participating teams.

## Key Analyses and Transformations
The notebook includes a series of data loading, cleaning, transformation, and analysis steps:

### Data Loading and Preparation
-   **Schema Definition**: Custom `StructType` schemas are defined for each CSV file to ensure correct data type inference in PySpark DataFrames.
-   **DataFrame Creation**: Data is loaded into PySpark DataFrames from the CSV files.
-   **SparkSession**: A SparkSession is created for data processing.

### Data Cleaning and Feature Engineering
-   **Ball-by-Ball Data (`ball_by_ball_df`)**:
    -   Filtered to exclude `wides` and `noballs` for specific analyses.
    -   Calculated total and average runs per `match_id` and `innings_no`.
    -   Introduced a `running_total_runs` column using window functions to track cumulative scores within an over.
    -   Created a `high_impact` flag for balls resulting in a wicket or more than 6 runs.
-   **Match Data (`match_df`)**:
    -   Extracted `year`, `month`, and `day` from `match_date`.
    -   Categorized `win_margin` into 'High', 'Medium', and 'Low'.
    -   Added `toss_match_winner` to indicate if the toss-winning team also won the match.
-   **Player Data (`player_df`)**:
    -   Normalized `player_name` by converting to lowercase and removing special characters.
    -   Handled missing values in `batting_hand` and `bowling_skill` with 'unknown'.
    -   Categorized players into 'Left-Handed' or 'Right-Handed' based on `batting_hand`.
-   **Player Match Data (`player_match_df`)**:
    -   Added a `veteran_status` column based on `age_as_on_match` (>= 35 years).
    -   Calculated `years_since_debut` based on the `season_year`.

### SQL-like Queries and Aggregations (using Spark SQL)
-   **Temporary Views**: All processed DataFrames (`ball_by_ball_df`, `match_df`, `player_df`, `player_match_df`, `team_df`) are registered as temporary SQL views.
-   **Top Scoring Batsmen per Season**: Identified batsmen with the highest total runs in each season.
-   **Economical Bowlers in Powerplay**: Found bowlers with the best average runs conceded per ball during the first 6 overs, considering minimum balls bowled.
-   **Toss Impact on Individual Matches**: Analyzed the outcome of matches where a team won the toss.
-   **Average Runs in Wins**: Calculated the average runs scored by players in matches their team won.
-   **Scores by Venue**: Determined the average and highest scores recorded at different venues.
-   **Dismissal Types**: Counted the frequency of different dismissal types.
-   **Team Toss Win Performance**: Analyzed how often teams win the match after winning the toss.

## Visualizations
Various visualizations are generated using Matplotlib and Seaborn to illustrate the insights:
-   Bar plot showing the most economical bowlers in powerplay overs.
-   Count plot illustrating the impact of winning the toss on match outcomes.
-   Bar plot displaying average runs scored by top batsmen in winning matches.
-   Bar plot showing the distribution of scores by venue.
-   Bar plot visualizing the frequency of different dismissal types.
-   Bar plot showcasing team performance after winning the toss.

<img width="1189" height="790" alt="image" src="https://github.com/user-attachments/assets/adf4879d-06c0-4a83-b2ef-76dfe4dfc3b2" />
<img width="984" height="590" alt="image" src="https://github.com/user-attachments/assets/b4afeb30-9bce-488c-b067-802c08932d70" />
<img width="1189" height="790" alt="image" src="https://github.com/user-attachments/assets/307f9ac6-a4c3-4838-8821-2e85bd03233b" />
<img width="1511" height="701" alt="image" src="https://github.com/user-attachments/assets/cf62208a-7811-4667-bdc0-ea08539b6059" />
<img width="1120" height="547" alt="image" src="https://github.com/user-attachments/assets/de0ddf29-bf19-4ddf-8843-21bf57cd2e13" />
<img width="1179" height="701" alt="image" src="https://github.com/user-attachments/assets/5edb007a-943a-45a6-8b4d-88b33c10905c" />







## Technologies Used
-   **PySpark**: For large-scale data processing and analysis.
-   **Pandas**: For converting Spark DataFrames to Pandas DataFrames for visualization.
-   **Matplotlib**: For creating static, animated, and interactive visualizations.
-   **Seaborn**: For making statistical graphics based on Matplotlib.
