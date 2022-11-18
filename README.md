
### Title

Temporal and spatial analysis of the characteristics of successful movies

  

### Abstract

  

Movies are an inseparable part of our lives. They are a form of art, loved and consumed by many. The movie industry is very competitive, as the number of movies produced per year grows exponentially, so there is a need to maximize chances of producing successful movies. However, little is known about what people's interests are as well as how they have changed over time. By utilizing the CMU dataset, enhanced by an IMDb rating dataset, the goal is to delve into the key ingredients that form a successful movie. The motivation is to find out which aspects influence a movie’s success as well as the evolution of the corresponding factors in various geographical regions and over different time periods. The results could provide support to movie producers as they will capture the essence of what people desire in a movie.

  

### Research questions

-   What are the most impactful factors for a successful movie?
    
-   Are they different depending on the country?
    
-   Are they changing over time? What are the trends and how they are evolving over the years?
    

### Proposed additional dataset

[IMDb_ratings](https://www.imdb.com/interfaces/) for the ratings as a measurement of movie success. We observed that movies are not uniquely identified by their names, nor by both (movie_name, release_year) tuple (e.g. “Sangam”, 1964). Even when we considered the full date instead of the year only there was an ambiguity. To tackle this problem, we used Wikidata Query Service to obtain IMDb ids based on freebase ids. This allowed us to successfully merge the two. The IMDb ratings dataset provides us with an average rating for each movie (on the scale from 1 to 10) as well as the number of votes, which can also be interpreted as popularity.

  

FreebaseID-to-IMDbID dataset - We have decided to make use of the [Wikidata Query Service](https://query.wikidata.org/#PREFIX%20wd%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%0APREFIX%20wdt%3A%20%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0APREFIX%20wikibase%3A%20%3Chttp%3A%2F%2Fwikiba.se%2Fontology%23%3E%0A%0ASELECT%20%3Fitem%20%3FfreebaseID%20%3FimdbID%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP31%2Fwdt%3AP279%2a%20wd%3AQ11424.%0A%20%20%3Fitem%20wdt%3AP646%20%3FfreebaseID.%0A%20%20%3Fitem%20wdt%3AP345%20%3FimdbID.%0A%20%20%7D) in order to create a bridge between the CMU dataset and IMDb ratings dataset.

### Methods

-   Obtaining a success measurement:
    

During exploratory data analysis, we discovered a tremendous amount of null values in the revenue column (only around 10% of data is available), so we decided to discard this feature in our future analysis. Because of that, we considered the IMDb ratings as the output we want to predict in our pipeline. We believe this crowdsourcing approach will provide an indicative feedback for finding what a successful movie is. We assume that these ratings are truthful enough for this purpose, as they usually combine the opinions of many people.

  

-   Data construction - in order to utilize the IMDb ratings we had to combine it with the CMU dataset.
    

-   The dataset is small enough to be completely loaded on our personal computers.
    
-   After various attempts to properly merge the CMU and IMDb ratings dataset (including - relying on movie name, release year and runtime) there were some movies which due to minor differences were left out. This led us to use the FreebaseID-toIMDbID dataset. Due to API restrictions (30 queries per 1 minute), we fetched the entire dataset from the Wikidata Query Service and then used it as a bridge between the 2 other datasets.
    

  
  

-   Investigate correlation between two categorical features:
    

-   Example using Languages and Countries:
    

We noticed that some movies could have several languages associated with them. To compute the correlation we created all the combinations between these languages and the country of the movie. Then, we calculated the occurrences for each pair. From that we performed a chi squared-tests with the null hypothesis being that the two features are independent. We observed the p-value.

  

-   Obtaining the effect of each feature on the success of the movie:
    

Correlation between each feature from the dataset and the rating will be computed.

For the numerical continuous features, we will calculate the Pierson’s correlation coefficient in order to get the strength of linear dependence between the feature and the success. Moreover, to determine if there is any non-linear dependence, we will compute the Spearman’s correlation coefficient.

These coefficients cannot be derived for the categorical features. For them, we will create a boxplot for each value of the categorical variable.

![](https://lh6.googleusercontent.com/tbTpR_fS_f-NGpnRMqGvntsdTSdwp5q8v1gyoDTtxU-rExv3hXrBUWnzHHc80rhzTBpZMzr79NMgxgZo6LLH2x2IvA69AA7BH146mm8nvJU1iFJgSTHRgSYu259l1_1HAX3NepnsA4L4kEwOl689nEUZiA1g4hvELdXS3GvQgcWIJZFpN_fjgZGFjr9Z7Q)
<p align = "center">Example of using a categorical box plot</p>
  

Then, for a quantitative calculation, we will compute the mutual information, or group by value of the categorical variable and compute the mean of the ratings corresponding to each of these values. We will investigate whether the countries with the highest average ratings are the ones leading to the highest ratings.

  

Finally, to get a ranking of the features based on their effect on the success, including temporal and spatial analysis, the decision tree model will be utilized.

  

In the future, we want to analyze the effect of collectively relevant features and try to apply an online feature selection.

  

-   Visualization - ideas for presenting results from our analysis include:
    

-   World map showing features of movies produced in different countries/ continents both as count and as highest average rating.
    
-   Time series plot representing the change in popularity of features.
    

  

-   Website creation and polishing of repository and storytelling - this step is of high importance for the successful completion of the project and presenting our results.
    

### Proposed timeline:

-   25.11.2022 Continue analysis from milestone 2
-   05.12.2022 Apply proposed data analysis pipeline in regards to research questions
-   10.12.2022 Summerize all insights taken from the data
-   15.12.2022 Prepare datastory
-   23.12.2022 Milestone 3 deadline

### Organizational within the team:
 
SpaCy Training on AD2 and AD3: Teammate 1: 
Datastory: Teammate 2:
Website: Teammate 3 and 4: 
Steps: Teammate 1,2,3,4:

Questions:

-   For the visualization part, which type of plots are preferable? Pie charts or box plots?
    
-   Should we remove rows having nan values for any of the analyzed features?
