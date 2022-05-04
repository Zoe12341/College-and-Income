---
title: "Maximizing Earning Potential"
author: "Zoe Buck and Samantha Remotigue"
date: "2022-05-04"
output: 
  prettydoc::html_pretty:
    toc: true
    theme: architect
    keep_md: TRUE 

---






## Introduction {.tabset .tabset-fade}

As college students, there is one thing propelling us to continue working hard: the future. The 4 am study sessions and endless piles of homework are draining, but in the end these accomplishments pave the way for a successful career - or do they? 

Is your future job salary truly based off your achievements and work ethic, or is it simply based off the type of college you attend and the degree you obtain? We seek to understand the true affect of the college you attend on your future salary. There is a high focus on salary potential because of the high cost of colleges. Students pour thousands of dollars into their education, with the expectation that it will land them a higher paying job and more money in the long run. 

A study by Georgetown University found that, in general, students who graduate from ivy league colleges go on to have higher earnings. We wanted to test the strength of this correlation. ^[[Georgetown Study](https://1gyhoq479ufd3yna29x7ubjn-wpengine.netdna-ssl.com/wp-content/uploads/CEW-Buyer-Beware.pdf)]   


## About our Data

In this study, we explored data on the salaries of graduates from different types of undergraduate schools. ^[[Data Source](https://www.kaggle.com/datasets/wsj/college-salaries/code)] We compared the differences in salaries to examine correlations between the college you attend and your future salary. To make this comparison, we want to look at the population of all people who graduate from colleges in the US with an undergraduate degree. The data we have is a sample of this population, and contains 269 observations. Each observation represents data from a certain school, and the variables we look at from this dataset are shown below:   


| Variable                 | Type               | Notes                                                       |   |   |
|--------------------------|--------------------|-------------------------------------------------------------|---|---|
| School.Name              | Categorical Nominal        | Names of 269 unique colleges                                |   |   |
| School.Type              | Categorical Nominal        | Levels: Engineering, Party, Liberal Arts, Ivy League, State |   |   |
| Starting.Median.Salary   | Discrete Numerical | The median starting salary of graduates                     |   |   |
| Mid.Career.Median.Salary | Discrete Numerical | The median mid career salary of graduates                   |   |   |





## <span style="text-decoration:underline"> Visualizations </span>

### Univariate summary


![](Project-Draft_files/figure-html/unnamed-chunk-2-1.png)<!-- -->



**Description: ** We first generated a univariate graph of salaries (both the mid career and starting salary) to get a sense of what their centers and distributions looked like. The allows us to get a better understanding of these variables, before we look more deeply at the relationship between them. 

The starting median salaries are right skewed, with a median of $45,100 and a mean of $46,253. The starting median salaries range from around $34,500 to $75,500. Also, they have an interquartile range of 6,900 and a standard deviation of 6,617.038. Mid career salaries have a much wider spread, ranging from $43,900 to $134,000, with an IQR of 19,525, and a standard deviation of 15,191.44. There doesn't appear to be a skew, and the median is $82,700. We would expect the median to be higher for mid career salaries than starting salaries since people in more senior positions tend to make more money. It is interesting that some of the mid career salaries are actually lower than some of the starting median salaries. This occurs because graduates of some colleges have a higher starting salary than other schools' median mid career salaries. 

Here is a summary these values:

| Time                 | Median               | Mean                                                       | IQR  | Range |
|--------------------------|--------------------|-------------------------------------------------------------|---|---|
| Mid Career              | 82,700        | 83,932.34                                |  19,525 |  90,100 |
| Starting Career              | 45,100        | 46,253 | 6,900  | 41,000  |




### Scatterplot 

![](Project-Draft_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

**Description: ** Using the salaries by college type dataset, we constructed a scatterplot comparing the starting career salaries of college types, to the mid career salaries of those college types. Our population of interest for is college students who graduated from undergrad and earn a salary.

There appears to be a positive correlation between the starting median salary and the mid career salary. However, correlation does not mean causation and a proper experiment would be necessary to determine if having a higher starting salary causes one to have a higher mid career salary. 

In total, there are 269 observations and 8 variables. Two of the variables being categorical, “School.Name” and “School.Type”, which grouped schools according to the type of college they were (Engineering, Liberal Arts, State, Ivy league, Party). The other six variables are “Starting.Median.Salary”, “Mid.Career.Median.Salary”, “Mid.Career.10th.Percentile.Salary”, “Mid.Career.25th.Percentile.Salary”, “Mid.Career.75th.Percentile.Salary” , and “Mid.Career.25th.Percentile.Salary”. These numerical variables are labeled in units of US dollars. For the Starting Median Salary, values ranged from $40,000 to $75,000. However, for the Mid Career Salary, the values ranged from $40,000 all the way up to $120,500. 


## Testing our hypothesis {.tabset .tabset-fad}
We decided to use hypothesis testing to test our prediction that there is a significant difference in average mid career salaries from different types of schools. We will use a significance level of .05

Our null hypothesis is that there is no difference in average mid career salaries of graduates from different types of schools. In symbols this can be represented as: μ <sub>ivy</sub> = μ<sub>state</sub> = μ<sub>liberal</sub> = μ<sub>party</sub> = μ<sub>engineer</sub> where μ is the average midcareer salary. 

Our alternative hypothesis is that there is a difference in average mid career salaries of graduates from at least one type of colleges. 

### Analysis of variance
We are looking at samples from 5 different populations: graduates of ivy league schools, graduates of state schools, graduates of liberal arts schools, graduates of party schools, and graduates of engineering schools. We can use ANOVA testing to analyse the variance between these groups. To use ANOVA testing, we are assuming our observations are independent of each other, we have a large sample size, and we have normality. 

First, we need to compute the F statistic to estimate the total relative variance between our different groups of college graduates: 
      F statistic = MSG/MSE = variance between groups/variance within groups
      We generate our F-statistic using R:
      


```
## Analysis of Variance Table
## 
## Response: Mid.Career.Median.Salary
##              Df     Sum Sq    Mean Sq F value    Pr(>F)    
## School.Type   4 2.4453e+10 6113309686  52.694 < 2.2e-16 ***
## Residuals   264 3.0628e+10  116014507                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

Based on the values given above, our F score = 52.694 and our P-value = 2.2e-16. This means there is a 0.000000000000022% chance that differences in future salaries of graduates from different types of colleges are simply due to chance.  

We can check also make a histogram of our residual values to check for normality visually:
![](Project-Draft_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

From the histogram above, we can see that the normality assumption seem to be met since the histogram roughly forms a bell curve, indicating that the residuals follow a normal distribution. 

### Conclusion
Our p value of 2.2e-16 is much smaller than our significance level of .05. Therefore, we can reject our null hypothesis. There is evidence that graduates of at least one college type tend to have different mid career salaries than other college types. 



## <span style="text-decoration:underline"> Analysis with Linear Models </span> 


### Model between the response and neither of the explanatory variables

![](Project-Draft_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

#### Description
First, we considered just the Mid career median salary, in order to see the average mid career median salary. In addition, we showed the average starting median salary on the graph to better visualize where the averages of the two variables meet. ^[[Vertical line info](https://www.geeksforgeeks.org/add-vertical-and-horizontal-lines-to-ggplot2-plot-in-r/)]

**Model Equation: ** Mid.Career.Salary = 83932.34

- **y-intercept: ** The intercept for the response variable only is the same as the mean. The average mid career salary for college graduates is $83,932.32.
- **slope: ** The slope is zero since this is simply a horizontal line


### Model between the response and the numerical explanatory variable:
![](Project-Draft_files/figure-html/unnamed-chunk-7-1.png)<!-- -->



| Coefficient                 | Estimate        | Std. Error             | t-value  | P-value |
|--------------------------|--------------------|-------------------------------------------------------------|---|---|
| Intercept              | -7.699e+03        | 2.905e+03         |  -2.65 |  0.00853 |
| Slope              | 1.989e+00        | 6.246e-02 | 31.84  | < 2e-16  |



#### Description
Next, we created a model for the relationship between the starting median salary and mid career salary. This allows us the quantify the relationship between the two variables and see how significant the relationship is. 

**Model Equation**
Mid.Career.Median.Salary = -.007699 + 1.989(Starting.Median.Salary)

- **Slope:** The slope for this equation is 1.989. This means that as the Starting Median Salary increases by $1, we would expect the Mid Career Salary to increase by approxiamately 1.989 dollars. 
- **Y-intercept:** The y-intercept is -.007699. This means when the Starting salary is 0, we expect the mid career salary to be -.007699
 

### Model between the starting median salary and the school type 
![](Project-Draft_files/figure-html/unnamed-chunk-9-1.png)<!-- -->




|Coefficients:     |  Estimate | Std. Error | t value |  P value  |  
|-------------------|-----------|------------|-----------------------|
|(Intercept)        |       103842      | 2471 | 42.024 | < 2e-16  |
|School.TypeIvy League |     16283     |  4540 |  3.587 | 0.000399  |
|School.TypeLiberal Arts  | -14463    |   2928 | -4.939 | 1.39e-06  |
|School.TypeParty        |  -19157   |    3451 | -5.552 | 6.88e-08  |
|School.TypeState       |   -25275    |   2602 | -9.715  | < 2e-16 |

#### Description
We also made a model for the relationship between the school type and the mid career salary. Similary to our plot of 
the relationship between the starting median salary and mid career salary, this model allows us the quantify the relationship between the two variables and see how significant the relationship is. 

**Model Equation**
Mid.Career.Median.Salary = 103842 + 16283(School.TypeIvy) + -14463(School.TypeLiberal) + -19157(School.TypeParty) + -25275(School.TypeState)

- **The y-intercept:** The y-intercept is 103842. This means if the school is an engineering school (the reference variable), we expect the mid career salary to be 103842. 

- **School.TypeIvy League: ** The coefficient 16283 represents the slope of the line and adjusts for if the school is a Ivy League. If the school is an ivy league we expect the mid career salary to increase by approximately 16,283 dollars in comparison to an engineering school if all other variables are held constant.

- **School.TypeLiberal Arts: ** The coefficient -14463 represents the slope of the line and adjusts for if the school is liberal arts. If the school is liberal arts we expect the mid career salary to decrease by approximately 14463 dollars in comparison to an engineering school if all other variables are held constant.

- **School.TypeParty: **The coefficient -19157 represents the slope of the line and adjusts for if the school is a party school. If the school is a party school, we expect the mid career salary to decrease by approximately 19157 dollars in comparison to an engineering school if all other variables are held constant.

- **School.TypeState:** The coefficient -25275 represents the slope of the line and adjusts for if the school is a state school. If the school is a state school, we expect the mid career salary to decrease by approximately 25275 dollars in comparison to an engineering school if all other variables are held constant.



### Parallel slopes Model
![](Project-Draft_files/figure-html/unnamed-chunk-11-1.png)<!-- -->


#### Description
Next, we wanted to begin trivariant analysis to consider the interaction between all three variables of interest. To do this, we used a parallel slopes model because it is one of the main ways of conducting trivariate analysis. 

**Model Equation**
Mid.Career.Median.Salary = -15,630 + 2.023(Starting Median Salary) + 13,420(School.TypeIvy) + 12,460(School.TypeLiberal) + 7,834(School.TypeParty) + 4,930(School.TypeState)

- **Y-intercept: ** The y-intercept is -1,5630. This means if the school is an engineering school (the reference variable) and the starting career salary is $0, we expect the mid career salary to be -1,5630. 

  - The intercept has a p-value of 0.000840. This value is much smaller than our significance level of .05, so this variable has a significant affect on the response variable. 

- **Starting Median Salary coefficient:** The coefficient 2.023 represents the slope of the line. When the starting slary increases by $1, we expect the mid career salary to increase by approximately 2.023.

  - This coefficient has a p-value of 0.000840. This value is much smaller than our significance level of .05, so this variable has a significant affect on the response variable.

- **School.TypeIvy:** The coefficient 13,420 is the average difference in mid career salary between a engineering school graduate and and an ivy league graduate. It shows up as a difference in intercept on the plot. If the school is an ivy league we expect the mid career salary to increase by approximately 13,420 in comparison to an engineering school if all other variables are held constant. 

  - This coefficient has a p-value of 0.000840. This value is much smaller than our significance level of .05, so this variable has a significant affect on the response variable.

- **School.TypeLiberal:** The coefficient 12,460 is the average difference in mid career salary between a engineering school graduate and and an liberal arts school graduate. It shows up as a difference in intercept on the plot. If the school is liberal arts, we expect the mid career salary to increase by approximately 12,460 in comparison to an engineering school if all other variables are held constant. 

  - This coefficient has a p-value of 0.000840. This value is much smaller than our significance level of .05, so this variable has a significant affect on the response variable.

- **School.TypeParty: **The coefficient 7,834 is the average difference in mid career salary between a engineering school graduate and and an party school graduate. It shows up as a difference in intercept on the plot. If the school is a party school we expect the mid career salary to increase by approximately 7,834 in comparison to an engineering school if all other variables are held constant. 

  - This coefficient has a p-value of 0.000164. This value is much smaller than our significance level of .05, so this variable has a significant affect on the response variable.

- **School.TypeState: **The coefficient 4,930is the average difference in mid career salary between a engineering school graduate and and a state school graduate. It shows up as a difference in intercept on the plot. If the school is a state school we expect the mid career salary to increase by approximately 4,930 in comparison to an engineering school if all other variables are held constant. 

  - This coefficient has a p-value of 0.005312 This value is much smaller than our significance level of .05, so this variable has a significant affect on the response variable. However, it is worth noting that this variable is slightly less significant than our other variables since it is only significant at the .001 level and not the .0001 level. 

### Interaction model 
![](Project-Draft_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


#### Description 
Continuing our tivariant analysis, we constructed an interaction model because we believed in an interaction between Starting Median Salary and Mid Career Median Salary with respect to undergraduate school type. If there was an insignificant interaction then the Parallel Slopes model would fit best for the data. The interactive model we generated has an R squared value of 0.85. This value is close to 1 suggesting our model is a good fit for these variables.

Unlike the parallel slope model, our interactive model takes into account the individual slope for each school type: Engineering, Liberal Arts, Party, State, and Ivy League. Additionally, the interactive model takes into account the different intercepts for each school type as well.

**Model Equation**
Mid.Career.Median.Salary = -1,5630 + 2.023(Starting Median Salary) + 13,420(School.TypeIvy) + 12,460(School.TypeLiberal) + 7,834(School.TypeParty) + 4,930(School.TypeState)

- **Y-intercept** The y-intercept is 0.52438. This means if the school is an engineering school (the reference variable) and the starting career salary is $0, we expect the mid career salary to be 0.52438. 

  - It has a p-value of .524, which is much larger than our significance level of .05. This means we would not include this value in our ideal interactive model since it is insignificant. 

- **Starting Median Salary coefficient:** The coefficient 1.652 represents the slope of the line. When the starting slary increases by $1, we expect the mid career salary to increase by approximately $1.652
  - It has a p-value of 2e-16. This is extremely small and definitely smaller than our significance level of .05. This means this coefficient has a significant effect on our response variable. 

- **School.TypeIvy:** The coefficient 3,2280 is the average difference in mid career salary between a engineering school graduate and and an ivy league graduate. It shows up as a difference in intercept on the plot. If the school is an ivy league we expect the mid career salary to increase by approximately 3,2280 in comparison to an engineering school if all other variables are held constant. 

  - It has a p-value of .423, which is much larger than our significance level of .05. This means we would not include this value in our ideal interactive model since it is insignificant. 

- **School.TypeLiberal:** The coefficient -2,6870 is the average difference in mid career salary between a engineering school graduate and and an liberal arts school graduate. It shows up as a difference in intercept on the plot. If the school is liberal arts, we expect the mid career salary to increase by approximately -2,6870 in comparison to an engineering school if all other variables are held constant.

  - It has a p-value of .039. This smaller than our significance level of .05. This means this coefficient has a significant effect on our response variable.

- **School.TypeParty: **The coefficient 4,689 is the average difference in mid career salary between a engineering school graduate and and an party school graduate. It shows up as a difference in intercept on the plot. If the school is a party school we expect the mid career salary to increase by approximately 4,689 in comparison to an engineering school if all other variables are held constant. 

  - It has a p-value of 0.80, which is much larger than our significance level of .05. This means we would not include this value in our ideal interactive model since it is insignificant. 

- **School.TypeState: **The coefficient -20,160 is the average difference in mid career salary between a engineering school graduate and and a state school graduate. It shows up as a difference in intercept on the plot. If the school is a state school we expect the mid career salary to increase by approximately -20,160 in comparison to an engineering school if all other variables are held constant. 

  - It has a p-value of .061, which is sligtly larger than our significance level of .05. This means we would not include this value in our ideal interactive model since it is insignificant. 

- **Starting.Median.Salary:School.TypeIvy League:** The coefficient -.3033 represents the difference in slope between the engineering schools and ivy league school graduates' mid career salaries. You would add -.3033 to the slope if the school is an engineering school. It accounts for the difference in slope between engineering and ivy league schools. 

  - It has a p-value of .649, which is much larger than our significance level of .05. This means we would not include this value in our ideal interactive model since it is insignificant. 

- **Starting.Median.Salary:School.TypeLiberal Arts: ** The coefficient .7521 represents the difference in slope between the engineering schools and ivy league school graduates' mid career salaries. You would add .7521 to the slope if the school is a liberal arts. It accounts for the difference in slope between engineering and liberal arts schools.

  - It has a p-value of .002. This smaller than our significance level of .05. This means this coefficient has a significant effect on our response variable.

- **Starting.Median.Salary:School.TypeParty: ** The coefficient -.03936 represents the difference in slope between the engineering schools and ivy league school graduates' mid career salaries. You would add -.03936 to the slope if the school is a party school. It accounts for the difference in slope between engineering and party schools. 

  - It has a p-value of .917, which is much larger than our significance level of .05. This means we would not include this value in our ideal interactive model since it is insignificant. 

- **Starting.Median.Salary:School.TypeState: ** The coefficient .4432 represents the difference in slope between the engineering schools and ivy league school graduates' mid career salaries. You would add .4432 to the slope if the school is a state school. It accounts for the difference in slope between engineering and state schools.

  - It has a p-value of .021. This smaller than our significance level of .05. This means this coefficient has a significant effect on our response variable.


## Results and the future

There appears to be a strong linear correlation between starting career salary and mid career salary, and the linear regression model we generated for this had a R squared value of 0.7916. When we took college type into account, we were able to produce an interactive model with a R squared value of 0.8584. This suggests that school type also plays a role in determining one's mid career salary. The R squared value 0.85 of our interactive model was approximately the same as the R squared value 0.8488 of our parallel slopes model. Both these models have high R squared values suggesting both would be a good fit to describe the interaction between the three variables. However, if we were to use the interactive  model, we would consider removing the coefficients we listed as insignificant above to simplify the equation. One of the advantages of the parallel slopes model is that all the coefficients included are significant, so we would likely use this model over the interactive one.  

Especially with the financial insecurity that the COVID pandemic has brought on for many, considering a school's track record for producing financially successful students might be a factor potential students want take into account. However, it is worth noting that a higher salary potential comes at a cost. Although our interactive model found that graduates from ivy league schools on average have a mid career salary $52,440 more than state school graduates, ivy league schools tend to cost more to attend. In 2022, ivy league schools cost $78,417 on average to attend per year ^[[Ivy Tuition](https://www.thebalance.com/can-you-afford-an-ivy-league-education-for-your-child-795012)] while state schools cost $10,338 for in-state students and $22,698 for out of state students on average. Therefore students might also want to look at schools with the best value ^[[State Tuition](https://www.usnews.com/education/best-colleges/paying-for-college/articles/paying-for-college-infographic)]. 

- Our next steps would be looking at how other variables affect the mid career salary. For example we could look more closely at the effect of degree type of mid career salary. 
- Another step for the future could be testing for a relationship between the two categorical variables college type and degree type 
- Also, we might want further hypothesis testing to test the extent of the differences between schools (since the ANOVA testing we did only proved there was a significant difference of at least *1* college type)


## Further Exploration
### Boxplot
![](Project-Draft_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

In exploring further, we wanted to compare the Mid Career salary, by percentile, to School Type. Using a boxplot, we are able to clearly see the mid carrer salary by percentile for each School type, as well as, the median and inter quartile range. Additionally, we are able to see how to data in symmetric or skewed. One interesting observation we can note from this graph is that the Mid Career 75th percentile for Ivy League schools ranges within the same salary as the mid career 90th percentile for Engineering, Liberal Arts, Party, and State schools.

### Examining affect of degree type on salary
![](Project-Draft_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

In this scatterplot, we wanted to assess the affect of degree type on salary. In this graph, we compared the Starting Median Salary and Mid Career Median Salary by the major given in our salaries_by_degrees dataset. The salary ranges from $0-$110,000. Looking at the graph, we can see the difference between the starting and mid career salary for each degree. This displays which degrees show the most growth in salary between starting and mid career. For example, a degree in religion has a $40,000 difference between starting and mid career salary, while a degree in chemical engineering has a $50,000 difference.

## References








