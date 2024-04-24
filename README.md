# Predicting fencing success

Fencing is one of the five original Olympic sports. Despite being rooted in historical European dueling tradition, fencing is a living sport. Changes in technical execution and strategic conceptualization have evolved as new minds and athletes participate, creating a culture where new schools of thought often usurp the old. The most recent coaching schema has reduced the importance of a “this for that” approach to fencing actions in favor of steadily applying pressure until favorable conditions are created. Using high-level, international data, we want to test this coaching schema by answering the following questions:
* How does aggression predict scoring success?
* How does score difference inform a fencer’s strategy?
This data is useful to any fencer or fencing coach. In particular, the Buckeye Fencing Club stands to immediately and directly benefit from the results of this project.

## Data Collection
We collected a wealth of fencing phrase (i.e., from when the referee commands “fence” to when a touch is scored) data including fencer identities, tournament location and date, who scored a touch, where the touch was scored (i.e., where on the body a fencer was stabbed), etc. These data were all scraped from The Fencing Database (https://www.fencingdatabase.com/).

There were 7 total features in the initial dataframe: weapon (weapon), initiator (initiated), where the touch occurred on the strip (strip_location), where the touch was scored (body_location), score after touch occurred (left_score and right_score), and which fencer scored in the phrase (touch). From these, we used one hot encoding to summarize strip location (touch_num), which fencer is winning (scorer_lead), and what the score difference was before the touch occurred (score_diff_pre). 

## Modeling Approach
For our final models, we split data by each weapon (i.e., epee, foil, and saber) due to the fundamental differences in how points are scored in each. To understand how aggression predicts scoring success, we built a logistic regression model for each weapon using initiated and touch_num. For these logistic regression models, we withheld 20% of the data for training. Across all weapons, our models show that more the more aggressive fencer (defined as being the initiated and touch_num on the opponent’s side) scores approximately 70% of the time (80% for saber, 65% for epee, 64.5% for foil). To understand how score difference predicts a fencer’s strategy, we compared who initiated an attack (left or right) to who was leading in points. We found that fencers who were winning initiated in saber and fencers who were losing initiated in epee. We did not find a strong signal within foil.

## Conclusions and Future Directions
Fencing is an inherently difficult sport to analyze. Tactics within a bout, especially at the international/Olympic-level, evolve as fencers get a better feel for each other. Previous analyses of fencing data at small scales have highlighted the impacts of referring and rule interpretation (particularly in saber) as well as the impact travel has on anticipated tournament results. 

Compared to other sports, fencing is in a “statistical infancy” and not much about any one individual fencer or tournament is recorded compared to other sports like American football or basketball. Our results support the current schema fencing coaches employ. In fact, during the execution of this project and following through on some preliminary results hinting at the importance of aggression, several members of the Buckeye Fencing Club were able to earn medals and national ratings at local tournaments. Future projects could build upon this by looking at tactics in greater depth (e.g., sword movements and actions used), accounting for referee bias with datasets that include both the referees call and a community-assessment (see https://actions.quarte-riposte.com/ for examples), and accounting for the non-independence of data points since fencers often meet each other multiple times at the international/Olympic-level.

# Repository description
[Data](./data) contains all data scraped for this project as .csv files.

[Preprocessing and preliminary visualizations](./Preprocessing%20+%20Preliminary%20visualization.ipynb) can be found as a jupyter notebook detailing how data were intitially gathered.

[How does aggression predict scoring success?](./Logistic%20Regression.ipynb) is answered in this jupyter notebook. Includes all models, stats, and figures.

[How does score difference inform a fencer’s strategy?](./Linear_regression_with_score_differences.ipynb) is answered in this jupyter notebook. Includes all models, stats, and figures.
