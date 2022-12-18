# Data-Science---Module-7-Assignment
To complete this assignment:
- download the data (make sure the data file is saved as movie_metadata.csv),
- run the following code in RStudio, and
- use functions and visualizations to explore the data and answer each question.
The data set can be downloaded from Movie Metadata
If it does not download, click here: movie_metadata.csv
Remember that because you are downloading the data set to your local computer you will need to set your working directory (folder) using setwd() before importing the data into R, and make sure that you have the required packages {dplyr}, {ggplot2}, and {corrplot} installed.
![image](https://user-images.githubusercontent.com/59670247/208313672-9a12cf9a-dfc8-4db3-8a8f-df33feefef8b.png)
# Load Packages
library(dplyr)  
library(ggplot2) 
library(corrplot)
 
# Import Data
dat <- read.csv("movie_metadata.csv")
 
# Subset Data  
dat <- dat %>%
     filter(budget < 150000000)  %>%
     select(color, duration, budget, imdb_score, aspect_ratio, movie_facebook_likes) 
Question 1: Which of the following statements is true?
•	Color is the only variable stored as a factor, and the average number of Facebook likes is approximately 158
•	Duration is the only variable stored as a factor, and the average number of Facebook likes is approximately 6998
•	Color is the only variable stored as a factor, and the average aspect ratio is approximately 2.1
•	Duration is the only variable stored as a factor, and the average aspect ratio is approximately 4.7

Correct – The summary() function provides important statistics about each variable, and the str() function provides information about the class and contents of each variable.

Question 2: Use a histogram and/or the summary() function to determine which of the following statements is true.
> summary(dat$duration)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    7.0    94.0   104.0   107.8   118.0   330.0       5 
> hist(dat$duration)
![image](https://user-images.githubusercontent.com/59670247/208313684-864d79d9-5965-47fc-8ea5-f8a5fe3254a7.png)
![image](https://user-images.githubusercontent.com/59670247/208313701-c77d6138-71c6-4f66-8634-809677468646.png)
•	Most films are between 80 and 120 minutes in duration
•	Most films are between 120 and 180 minutes in duration
•	The maximum duration is 300 minutes
•	The minimum duration is 60 minutes

Correct – Most movies are between 60 and 180 minutes.


Question 3: Use {ggplot2} to create a boxplot with color on the x axis and budget on the y axis. Which of the following statements is true?
> ggplot(dat) + 
   geom_boxplot(aes(x = color, y = budget))
![image](https://user-images.githubusercontent.com/59670247/208313718-4d167dd5-f659-4376-9354-490a35d8f20d.png)
![image](https://user-images.githubusercontent.com/59670247/208313727-fe5966b0-8a81-4543-949e-2a8d8cef37da.png)
Which of the following statements is true? 
•	All movies are labelled as either "Black and White" or "Color", and black and white movies tend to have larger budgets than color movies.
•	All movies are labelled as either "Black and White" or "Color", and color movies tend to have larger budgets than black and white movies
•	There are some movies that are not labelled as either "Black and White" or "Color", and color movies tend to have larger budgets than black and white movies.
•	There are some movies that are not labelled as either "Black and White" or "Color", and black and white movies tend to have larger budgets than color movies.

Question 4: Use {ggplot2} to create a histogram of budget. Which of the following statements is true? Note: To improve the readability of your plot, you may want to use the values of budget / 1000000 rather than the raw values.
> budget_divided_by_1000000 <- dat$budget / 1000000
> hist(budget_divided_by_1000000)
![image](https://user-images.githubusercontent.com/59670247/208313747-1cc110a9-c48a-461e-b0b2-35ea593f5ca3.png)
![image](https://user-images.githubusercontent.com/59670247/208313763-27cf31e8-51e1-4fb0-8622-39f6eb0ed3e0.png)
> hist(dat$budget)![image](https://user-images.githubusercontent.com/59670247/208313771-acdb0918-9b3c-4c35-a347-ebb1cbd05427.png)
![image](https://user-images.githubusercontent.com/59670247/208313781-6f70f6bb-be29-48d2-b147-77434a50f467.png)
> ggplot(dat) + 
   geom_histogram(aes(x = budget / 1000000))
`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
![image](https://user-images.githubusercontent.com/59670247/208313790-2cf1ba7a-7c38-45f8-84a0-1dd8357d0446.png)
![image](https://user-images.githubusercontent.com/59670247/208313794-c374a757-5b96-428b-845d-7854513c2fa0.png)
•	Most movies budgets are between $50 million and $100 million.
•	Most movies budgets are less than $50 million.
•	Most movies budgets are greater than $50 million.
•	The budget variable is approximately normally distributed.


Question 5: Use {ggplot2} to create a scatter plot with budget on the x axis and IMDB score on the y axis. Use cor() to calculate the correlation coefficient of the two variables. Which of the following statements is true?
> ggplot(dat) +
   geom_point(aes(x = budget, y = imdb_score))
![image](https://user-images.githubusercontent.com/59670247/208313815-2d009b4f-8222-46a3-8a55-937af968b426.png)
![image](https://user-images.githubusercontent.com/59670247/208313829-bed924a8-862a-452e-9bc6-bbd2a515d964.png)
> cor_budget_and_imdb_score <- dat %>%
   select(budget, imdb_score)

> cor_budget_imdb_output <- cor(cor_budget_and_imdb_score)

> corrplot(cor_budget_imdb_output, method = "number")
![image](https://user-images.githubusercontent.com/59670247/208313839-e66e6fbc-bf3b-49de-9052-dadab7c51e74.png)
![image](https://user-images.githubusercontent.com/59670247/208313852-0164514e-0ca4-49b0-99ff-99dab64bbb31.png)
•	There is no clear relationship between budget and IMDB score.
•	Movies with lower budgets tend to have higher IMDB scores.
•	The correlation coefficient of budget and IMDB scores cannot be quantified using the available data.
•	Movies with larger budgets tend to have higher IMDB scores.

Correct – the correlation coefficient is very close to zero which indicates that there is not a strong relationship between the two variables.

Question 6: Use corrplot() and cor() to create a correlation plot of the numeric variables found in the data set. Which of the following statements is true? Note: To select only numeric columns from the data set and to drop records with missing values, use
dat %>%
     select_if(is.numeric) %>%
     drop_na()

> numeric_variables1 <- dat %>%
   select_if(is.numeric) %>%
   drop_na()

> cor_numeric_variables1_output <- cor(numeric_variables1)

> corrplot(cor_numeric_variables1_output, method = "number")
![image](https://user-images.githubusercontent.com/59670247/208313862-edafce47-b744-4a3a-9be8-9258c4308664.png)
![image](https://user-images.githubusercontent.com/59670247/208313875-79c79801-f7d6-4237-a56e-539a784ab0be.png)
•	There is a positive correlation between IMDB score and the number of Facebook likes for the movie.
•	There is a weak negative correlation between IMDB score and movie duration.
•	There is a strong positive correlation between IMDB score and movie budget.
•	There is a strong correlation between movie budget and aspect ratio.

Module 7 Quiz

Question 10 pts
A correlation plot or calculation assesses: 
The linear association between two variables.
How data should be imputed.
The confidence interval for your estimates.
The level of statistical significance.

Question 20 pts
Recoding (binning) a column has a downside, the downside is: 
Plots are more difficult to interpret.
The names of the bins might not be intuitive.
There is no way to transform the data back.
You lose information by binning your values.

Question 30 pts
Useful plots in exploratory data analysis include: 
Select all that apply.
Scatter plots
Pie charts
Histograms
Box plots

Question 40 pts
When handling missing values (NULL / na) it is important to consider:
Select all that apply.
Never removing nulls and should attempt to find a way to impute them.
Consider if removing the null would introduce bias
Consider if the values can be reasonably imputed
Just remove all the nulls because they cannot be used in modeling

Question 50 pts
Which of the following variables appear to be normally distributed?
 
None of the listed variables
Capital Gain and Capital Loss
Age
Hours per Week

Although age is typically a normally distributed variable, our age variable is this example is truncated at 17 years old.  Therefore, none of these variables are normally distributed


Question 60 pts
How could we improve the following plot?
![image](https://user-images.githubusercontent.com/59670247/208313902-1f354097-d796-430f-ad95-aeab1b2b70a2.png)
![image](https://user-images.githubusercontent.com/59670247/208313911-4211d9f5-a6eb-4111-96d4-43c5d33f196e.png)
Select all that apply.
Make the x-axis labels readable for all countries
Order the bars by frequency of occurrence for easier comparison
Add data labels so you can easily read each frequency
Remove the US from the chart, to get a better idea of the frequency of other countries. Then just list the frequency of US and the percentage of the population it represents on the chart so all data is included.

Question 70 pts
What are the purposes/benefits of Exploratory Data Analysis?
Select all that apply.
Gain understanding of your data through graphical representations.
To detect any outliers/anomalies in your data
Leverage summary statistics to better understand your data.
To discover patterns and associations
![image](https://user-images.githubusercontent.com/59670247/208313927-f63c5a9c-9e01-4baa-8de4-c4d3cc4f3b8f.png)
