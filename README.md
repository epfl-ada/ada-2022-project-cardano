## Milestone 2

### Files description
* `dataPreprocessing.ipynb`: notebook that contains the steps for preprocessing the data, in order to convert the data from the movie.metadata.tsv file of the CMU dataset to a format that enables us to use it for our analysis.
* `projectMilestone2.ipynb`: notebook that contains the first steps of our study.




### Title

Temporal and spatial analysis of the characteristics of successful movies

  

### Abstract

Movies are an inseparable part of our lives. They are a form of art, loved and consumed by many. The movie industry is very competitive, as the number of movies produced per year grows exponentially, so there is a need to maximize chances of producing successful movies. However, little is known about what people's interests are, as well as how they have changed over time. By utilizing the CMU dataset, enhanced by an IMDb rating dataset, the goal is to delve into the key ingredients that form a successful movie. The motivation is to find out which aspects influence a movie’s success as well as the evolution of the corresponding factors in various geographical regions and over different time periods. The results could provide support to movie producers as they will capture the essence of what people desire in a movie.



### Research questions

-   What are the most impactful factors for a successful movie?
    
-   Are they different depending on the country?
    
-   Are they changing over time? What are the trends and how they are evolving over the years?



### Proposed additional dataset

[IMDb_ratings](https://www.imdb.com/interfaces/) - We use the ratings from this dataset as a measurement of movie success. The IMDb ratings dataset provides us with an average rating for each movie (on the scale from 1 to 10) as well as the number of votes, which can also be interpreted as popularity.


FreebaseID-to-IMDbID dataset - We have decided to make use of the [Wikidata Query Service](https://query.wikidata.org/#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0APREFIX%20wikibase%3A%20%3Chttp%3A%2F%2Fwikiba.se%2Fontology%23%3E%0A%0ASELECT%20%3Fitem%20%3FfreebaseID%20%3FimdbID%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP31%2Fwdt%3AP279%2a%20wd%3AQ11424.%0A%20%20%3Fitem%20wdt%3AP646%20%3FfreebaseID.%0A%20%20%3Fitem%20wdt%3AP345%20%3FimdbID.%0A%20%20%7D) in order to create a bridge between the CMU dataset and IMDb ratings dataset. We observed that movies are not uniquely identified by their names, nor by both (movie_name, release_year) tuple (e.g. “Sangam”, 1964). Even when we considered the full date instead of the year only, there was an ambiguity. To tackle this problem, we used Wikidata Query Service to obtain IMDb IDs based on Freebase IDs. This allowed us to successfully merge the two.



### Methods

-   **Storing the data**:
The dataset is small enough to be completely loaded on our personal computers.


-   **Obtaining a success measurement**:
During exploratory data analysis, we discovered a tremendous amount of null values in the revenue column (only around 10% of data is available), so we decided to discard this feature in our future analysis. Because of that, we considered the IMDb ratings as a replacement for the popularity measerement. We believe this crowdsourcing approach will provide an indicative feedback for finding what a successful movie is. We assume that these ratings are truthful enough for this purpose, as they usually combine the opinions of many people.



-   **Investigating correlation between two categorical features** (e.g. Languages and Countries):
We noticed that some movies could have several languages associated with them. To compute the correlation, we created all the combinations between these languages and the country of the movie. Then, we calculated the occurrences for each pair. From that, we performed a chi squared-test with the null hypothesis being that the two features are independent. We observed the p-value and rejected the null hypothesis for small values.



-   **Obtaining the effect of each feature on the success of the movie**:
Correlation between each feature from the dataset and the rating will be computed.

    -   For the numerical continuous features, we will calculate the Pierson’s correlation coefficient, in order to get the strength of linear dependence between the feature and the success. Moreover, to determine if there is any non-linear dependence, we will compute the Spearman’s correlation coefficient.

    -   These coefficients cannot be derived for the categorical features. For them, we will first, for visualization, create a boxplot for each value of the categorical variables.

Then, for a quantitative calculation, we will compute the mutual information in order to obtain the strength of existing relationships. We could also group by value of the categorical variable and compute the mean of the ratings corresponding to each of these values. From this, we will investigate which countries contribute to a higher average rating.

To get a ranking of the features, the random forest model will be utilized.



-   **Analyzing the collective effect of features**: In the future, we want to analyze the effect of collectively relevant features and try to apply an online feature selection.



-   **Temporal and spatial analysis** will be conducted on the selected features.



-   **Visualizing** - ideas for presenting results from our analysis include:

    -   World map showing features of movies produced in different countries/ continents both as count and as highest average rating.
    
    -   Time series plot representing the change in popularity of features.



-   **Creating the website, polishing the repository and the storytelling**: This step is of high importance for the successful completion of the project and presenting our results.

## Milestone 3
### Project's data story
Our website can be found under [this](https://jdodinh.github.io/CardanoCritic/) link.

### Files description
* `preprocessing.ipynb`: notebook that contains the steps for the final preprocessing of the data, including extending it with information scraped from [IMDb_pro](https://www.pro.imdb.com/)
* `analysis.ipynb`: notebook that contains main analysis we perfmed on the final version of the dataset
* `models.ipynb`: notebook that contains functions we used for a regression and director-related analysis
* `requirements.txt`: libraries needed to run the code

### Proposed additional source of data
[IMDb_title.basics]([https://www.imdb.com/interfaces/](https://pro.imdb.com/signup/index.html)) - We use the 'title types' for removing tv series and keeping only valid movied. 

[IMDb_pro]([https://www.pro.imdb.com/](https://pro.imdb.com/signup/index.html)) - We use IMDb pro as an API for providing us additional details related to movies: budgets, box offices, directors, We write a few web scraping scripts to automatize this task. 
