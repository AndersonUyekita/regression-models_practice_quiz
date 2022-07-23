`Quiz 3 (Optional)` Regression Models
================

-   👨🏻‍💻 Author: Anderson H Uyekita
-   📚 Specialization: <a
    href="https://www.coursera.org/specializations/data-science-foundations-r"
    target="_blank" rel="noopener">Data Science: Foundations using R
    Specialization</a>
-   📖 Course:
    <a href="https://www.coursera.org/learn/regression-models"
    target="_blank" rel="noopener">Regression Models</a>
    -   🧑‍🏫 Instructor: Brian Caffo
-   📆 Week 3
    -   🚦 Start: Tuesday, 05 July 2022
    -   🏁 Finish: Tuesday, 19 July 2022
-   🌎 Rpubs: [Interactive
    Document](https://rpubs.com/AndersonUyekita/quiz-3_regression-models)

------------------------------------------------------------------------

## Question 1

You are being asked to participate in a research experiment with the
purpose of better understanding how people analyze data. If you complete
this quiz, you are giving your consent to participate in the study. This
quiz involves a short data analysis that gives you a chance to practice
the regression concepts you have learned so far.

**We anticipate that this will take about 15 minutes to complete. You
will be receiving feedback on your work immediately after submission.
For this reason, we ask that you do not post on the forums about this
quiz to maintain the integrity of this experiment.**

> Thank you for helping us learn more about data science! – Brian,
> Roger, Jeff

Your assignment is to study how income varies across different
categories of college majors. You will be using data from a study of
recent college graduates. Make sure to use good practices that you have
learned so far in this course and previous courses in the
specialization.

If you will proceed with the analysis, click “Yes”. Otherwise, click
“No” and exit the quiz.

-   [x] Yes
-   [ ] No

## Question 2

Your assignment is to study how income varies across college major
categories. Specifically answer: “Is there an association between
college major category and income?”

To get started, start a new R/RStudio session with a clean workspace. To
do this in R, you can use the q() function to quit, then reopen R. The
easiest way to do this in RStudio is to quit RStudio entirely and reopen
it. After you have started a new session, run the following commands.
This will load a data.frame called college for you to work with.

``` r
install.packages("devtools")
devtools::install_github("jhudsl/collegeIncome")
library(collegeIncome)
data(college)
```

Next download and install the matahari R package with the following
commands:

``` r
devtools::install_github("jhudsl/matahari")
library(matahari)
```

This package allows a record of your analysis (your R command history)
to be documented. You will be uploading a file containing this record to
GitHub and submitting the link as part of this quiz.

Before you start the analysis for this assignment, enter the following
command to begin the documentation of your analysis:

``` r
dance_start(value = FALSE, contents = FALSE)
```

You can then proceed with the rest of your analysis in R as usual. When
you have finished your analysis, use the following command to save the
record of your analysis on your desktop:

``` r
dance_save("~/Desktop/college_major_analysis.rds")
```

Please upload this college_major_analysis.rds file to a public GitHub
repository. In question 4 of this quiz, you will share the link to this
file.

A codebook for the dataset is given below:

-   `ank`: Rank by median earnings
-   `major_code`: Major code
-   `major`: Major description
-   `major_category`: Category of major
-   `total`: Total number of people with major
-   `sample_size`: Sample size of full-time, year-round individuals used
    for income/earnings estimates: p25th, median, p75th
-   `p25th`: 25th percentile of earnings
-   `median`: Median earnings of full-time, year-round workers
-   `p75th`: 75th percentile of earnings
-   `perc_men`: % men with major (out of total)
-   `perc_women`: % women with major (out of total)
-   `perc_employed`: % employed (out of total)
-   `perc_employed_fulltime`: % employed 35 hours or more (out of
    employed)
-   `perc_employed_parttime`: % employed less than 35 hours (out of
    employed)
-   `perc_employed_fulltime_yearround`: % employed at least 50 weeks and
    at least 35 hours (out of employed and full-time)
-   `perc_unemployed`: % unemployed (out of employed)
-   `perc_college_jobs`: % with job requiring a college degree (out of
    employed)
-   `perc_non_college_jobs`: % with job not requiring a college degree
    (out of employed)
-   `perc_low_wage_jobs`: % in low-wage service jobs (out of total)

``` r
library(collegeIncome)
library(kableExtra)

# Loading the college dataset.
data(college)

# Exploring de dataset.
str(college)
```

    ## 'data.frame':    173 obs. of  19 variables:
    ##  $ rank                            : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ major_code                      : int  2419 2416 2415 2417 2405 2418 6202 5001 2414 2408 ...
    ##  $ major                           : chr  "Petroleum Engineering" "Mining And Mineral Engineering" "Metallurgical Engineering" "Naval Architecture And Marine Engineering" ...
    ##  $ major_category                  : chr  "Engineering" "Engineering" "Engineering" "Engineering" ...
    ##  $ total                           : int  2339 756 856 1258 32260 2573 3777 1792 91227 81527 ...
    ##  $ sample_size                     : int  36 7 3 16 289 17 51 10 1029 631 ...
    ##  $ perc_women                      : num  0.911 0.515 0.594 0.652 0.418 ...
    ##  $ p25th                           : num  25000 26000 26700 26000 31500 23000 32500 37900 29200 23000 ...
    ##  $ median                          : num  40000 37000 45000 35000 62000 44700 45000 57000 36000 32200 ...
    ##  $ p75th                           : num  50000 40000 60000 45000 109000 50000 58000 67000 46000 47100 ...
    ##  $ perc_men                        : num  0.0891 0.4846 0.4058 0.3479 0.5821 ...
    ##  $ perc_employed                   : num  0.912 0.798 0.787 0.847 0.852 ...
    ##  $ perc_employed_fulltime          : num  0.921 0.711 0.883 0.937 0.809 ...
    ##  $ perc_employed_parttime          : num  0.177 0.362 0.339 0.167 0.402 ...
    ##  $ perc_employed_fulltime_yearround: num  0.77 0.709 0.774 0.653 0.685 ...
    ##  $ perc_unemployed                 : num  0.0885 0.2019 0.2128 0.1534 0.1484 ...
    ##  $ perc_college_jobs               : num  0.67 0.387 0.729 0.246 0.587 ...
    ##  $ perc_non_college_jobs           : num  0.182 0.516 0.176 0.411 0.386 ...
    ##  $ perc_low_wage_jobs              : num  0.0554 0.2156 0.0301 0.0432 0.118 ...

``` r
# Creating a auxiliary dataset.
df_college <- college

# Converting charactes variables into factor.
df_college %>%
    mutate(major = factor(major), 
           major_category = factor(major_category)) -> df_college

# Exploring 2.
summary(df_college)
```

    ##       rank       major_code                                     major    
    ##  Min.   :  1   Min.   :1100   Accounting                           :  1  
    ##  1st Qu.: 44   1st Qu.:2403   Actuarial Science                    :  1  
    ##  Median : 87   Median :3608   Advertising And Public Relations     :  1  
    ##  Mean   : 87   Mean   :3880   Aerospace Engineering                :  1  
    ##  3rd Qu.:130   3rd Qu.:5503   Agricultural Economics               :  1  
    ##  Max.   :173   Max.   :6403   Agriculture Production And Management:  1  
    ##                               (Other)                              :167  
    ##                    major_category     total         sample_size    
    ##  Engineering              :29     Min.   :   124   Min.   :   2.0  
    ##  Education                :16     1st Qu.:  4361   1st Qu.:  39.0  
    ##  Humanities & Liberal Arts:15     Median : 15058   Median : 130.0  
    ##  Biology & Life Science   :14     Mean   : 39168   Mean   : 356.1  
    ##  Business                 :13     3rd Qu.: 38844   3rd Qu.: 338.0  
    ##  Health                   :12     Max.   :393735   Max.   :4212.0  
    ##  (Other)                  :74                                      
    ##    perc_women         p25th           median           p75th       
    ##  Min.   :0.0000   Min.   :18500   Min.   : 22000   Min.   : 22000  
    ##  1st Qu.:0.3397   1st Qu.:24000   1st Qu.: 33000   1st Qu.: 42000  
    ##  Median :0.5357   Median :27000   Median : 36000   Median : 47000  
    ##  Mean   :0.5226   Mean   :29501   Mean   : 40151   Mean   : 51494  
    ##  3rd Qu.:0.7020   3rd Qu.:33000   3rd Qu.: 45000   3rd Qu.: 60000  
    ##  Max.   :0.9690   Max.   :95000   Max.   :110000   Max.   :125000  
    ##                                                                    
    ##     perc_men       perc_employed    perc_employed_fulltime
    ##  Min.   :0.03105   Min.   :0.0000   Min.   :0.5743        
    ##  1st Qu.:0.29798   1st Qu.:0.7477   1st Qu.:0.7741        
    ##  Median :0.46429   Median :0.8028   Median :0.8319        
    ##  Mean   :0.47745   Mean   :0.7886   Mean   :   Inf        
    ##  3rd Qu.:0.66033   3rd Qu.:0.8410   3rd Qu.:0.8974        
    ##  Max.   :1.00000   Max.   :0.9562   Max.   :   Inf        
    ##                                                           
    ##  perc_employed_parttime perc_employed_fulltime_yearround perc_unemployed  
    ##  Min.   :0.0000         Min.   :0.5857                   Min.   :0.04383  
    ##  1st Qu.:0.2090         1st Qu.:0.7009                   1st Qu.:0.15899  
    ##  Median :0.2862         Median :0.7484                   Median :0.19723  
    ##  Mean   :0.2874         Mean   :0.7476                   Mean   :0.21140  
    ##  3rd Qu.:0.3623         3rd Qu.:0.7896                   3rd Qu.:0.25229  
    ##  Max.   :0.5518         Max.   :1.0000                   Max.   :1.00000  
    ##  NA's   :1                                                                
    ##  perc_college_jobs perc_non_college_jobs perc_low_wage_jobs
    ##  Min.   :0.0633    Min.   :0.08278       Min.   :0.00000   
    ##  1st Qu.:0.2974    1st Qu.:0.27995       1st Qu.:0.06957   
    ##  Median :0.4160    Median :0.42020       Median :0.10857   
    ##  Mean   :0.4478    Mean   :0.41498       Mean   :0.11481   
    ##  3rd Qu.:0.6170    3rd Qu.:0.52756       3rd Qu.:0.15353   
    ##  Max.   :0.8383    Max.   :0.85364       Max.   :0.36566   
    ##  NA's   :1         NA's   :1             NA's   :1

``` r
library(plotly)

fig <- plot_ly(df_college, x = ~p25th, y = ~p75th, z = ~median, color = ~major_category)
fig <- fig %>% add_markers()
fig <- fig %>% layout(scene = list(xaxis = list(title = '25th Percentile'),
                     yaxis = list(title = '75th Percentile'),
                     zaxis = list(title = '50th Percentile (Median)')))
fig
```

![](quiz-3-optional_regression-models_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
# Fitting models
fit_p50 <- lm(data = df_college, formula = median ~ major_category - 1)
fit_p25 <- lm(data = df_college, formula = p25th ~ major_category - 1)
fit_p75 <- lm(data = df_college, formula = p75th ~ major_category - 1)

summary(fit_p25)$coeff %>% round(4)
```

    ##                                                   Estimate Std. Error t value
    ## major_categoryAgriculture & Natural Resources     30300.00   2854.331 10.6154
    ## major_categoryArts                                28775.00   3191.239  9.0169
    ## major_categoryBiology & Life Science              32457.14   2412.350 13.4546
    ## major_categoryBusiness                            37207.69   2503.414 14.8628
    ## major_categoryCommunications & Journalism         34000.00   4513.094  7.5336
    ## major_categoryComputers & Mathematics             26545.45   2721.498  9.7540
    ## major_categoryEducation                           25615.62   2256.547 11.3517
    ## major_categoryEngineering                         28662.07   1676.121 17.1002
    ## major_categoryHealth                              28916.67   2605.636 11.0977
    ## major_categoryHumanities & Liberal Arts           25966.67   2330.552 11.1419
    ## major_categoryIndustrial Arts & Consumer Services 30428.57   3411.578  8.9192
    ## major_categoryInterdisciplinary                   22900.00   9026.188  2.5371
    ## major_categoryLaw & Public Policy                 27600.00   4036.634  6.8374
    ## major_categoryPhysical Sciences                   31280.00   2854.331 10.9588
    ## major_categoryPsychology & Social Work            31066.67   3008.729 10.3255
    ## major_categorySocial Science                      28955.56   3008.729  9.6238
    ##                                                   Pr(>|t|)
    ## major_categoryAgriculture & Natural Resources       0.0000
    ## major_categoryArts                                  0.0000
    ## major_categoryBiology & Life Science                0.0000
    ## major_categoryBusiness                              0.0000
    ## major_categoryCommunications & Journalism           0.0000
    ## major_categoryComputers & Mathematics               0.0000
    ## major_categoryEducation                             0.0000
    ## major_categoryEngineering                           0.0000
    ## major_categoryHealth                                0.0000
    ## major_categoryHumanities & Liberal Arts             0.0000
    ## major_categoryIndustrial Arts & Consumer Services   0.0000
    ## major_categoryInterdisciplinary                     0.0122
    ## major_categoryLaw & Public Policy                   0.0000
    ## major_categoryPhysical Sciences                     0.0000
    ## major_categoryPsychology & Social Work              0.0000
    ## major_categorySocial Science                        0.0000

``` r
summary(fit_p50)$coeff %>% round(4)
```

    ##                                                   Estimate Std. Error t value
    ## major_categoryAgriculture & Natural Resources     43500.00   3590.819 12.1142
    ## major_categoryArts                                38050.00   4014.658  9.4778
    ## major_categoryBiology & Life Science              43864.29   3034.796 14.4538
    ## major_categoryBusiness                            49153.85   3149.357 15.6076
    ## major_categoryCommunications & Journalism         42000.00   5677.583  7.3975
    ## major_categoryComputers & Mathematics             34718.18   3423.712 10.1405
    ## major_categoryEducation                           37937.50   2838.792 13.3640
    ## major_categoryEngineering                         40393.10   2108.602 19.1563
    ## major_categoryHealth                              40316.67   3277.954 12.2993
    ## major_categoryHumanities & Liberal Arts           35166.67   2931.891 11.9945
    ## major_categoryIndustrial Arts & Consumer Services 40428.57   4291.850  9.4198
    ## major_categoryInterdisciplinary                   27500.00  11355.167  2.4218
    ## major_categoryLaw & Public Policy                 37800.00   5078.185  7.4436
    ## major_categoryPhysical Sciences                   40400.00   3590.819 11.2509
    ## major_categoryPsychology & Social Work            39888.89   3785.055 10.5385
    ## major_categorySocial Science                      39066.67   3785.055 10.3213
    ##                                                   Pr(>|t|)
    ## major_categoryAgriculture & Natural Resources       0.0000
    ## major_categoryArts                                  0.0000
    ## major_categoryBiology & Life Science                0.0000
    ## major_categoryBusiness                              0.0000
    ## major_categoryCommunications & Journalism           0.0000
    ## major_categoryComputers & Mathematics               0.0000
    ## major_categoryEducation                             0.0000
    ## major_categoryEngineering                           0.0000
    ## major_categoryHealth                                0.0000
    ## major_categoryHumanities & Liberal Arts             0.0000
    ## major_categoryIndustrial Arts & Consumer Services   0.0000
    ## major_categoryInterdisciplinary                     0.0166
    ## major_categoryLaw & Public Policy                   0.0000
    ## major_categoryPhysical Sciences                     0.0000
    ## major_categoryPsychology & Social Work              0.0000
    ## major_categorySocial Science                        0.0000

``` r
summary(fit_p75)$coeff %>% round(4)
```

    ##                                                   Estimate Std. Error t value
    ## major_categoryAgriculture & Natural Resources     53600.00   4756.197 11.2695
    ## major_categoryArts                                45262.50   5317.590  8.5118
    ## major_categoryBiology & Life Science              56214.29   4019.720 13.9846
    ## major_categoryBusiness                            58861.54   4171.461 14.1105
    ## major_categoryCommunications & Journalism         50000.00   7520.208  6.6488
    ## major_categoryComputers & Mathematics             44454.55   4534.856  9.8029
    ## major_categoryEducation                           52375.00   3760.104 13.9291
    ## major_categoryEngineering                         53379.31   2792.935 19.1123
    ## major_categoryHealth                              50750.00   4341.794 11.6887
    ## major_categoryHumanities & Liberal Arts           46133.33   3883.419 11.8796
    ## major_categoryIndustrial Arts & Consumer Services 51028.57   5684.743  8.9764
    ## major_categoryInterdisciplinary                   38000.00  15040.417  2.5265
    ## major_categoryLaw & Public Policy                 49400.00   6726.279  7.3443
    ## major_categoryPhysical Sciences                   50900.00   4756.197 10.7018
    ## major_categoryPsychology & Social Work            50888.89   5013.472 10.1504
    ## major_categorySocial Science                      52555.56   5013.472 10.4829
    ##                                                   Pr(>|t|)
    ## major_categoryAgriculture & Natural Resources       0.0000
    ## major_categoryArts                                  0.0000
    ## major_categoryBiology & Life Science                0.0000
    ## major_categoryBusiness                              0.0000
    ## major_categoryCommunications & Journalism           0.0000
    ## major_categoryComputers & Mathematics               0.0000
    ## major_categoryEducation                             0.0000
    ## major_categoryEngineering                           0.0000
    ## major_categoryHealth                                0.0000
    ## major_categoryHumanities & Liberal Arts             0.0000
    ## major_categoryIndustrial Arts & Consumer Services   0.0000
    ## major_categoryInterdisciplinary                     0.0125
    ## major_categoryLaw & Public Policy                   0.0000
    ## major_categoryPhysical Sciences                     0.0000
    ## major_categoryPsychology & Social Work              0.0000
    ## major_categorySocial Science                        0.0000

``` r
par(mfrow = c(2, 2))
plot(fit_p25)
```

![](quiz-3-optional_regression-models_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
shapiro.test(resid(fit_p75))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  resid(fit_p75)
    ## W = 0.88291, p-value = 2.112e-10

**Question:** Based on your analysis, would you conclude that there is a
significant association between college major category and income?

-   [ ] Yes
-   [ ] No

## Question 3

Please type a few sentences describing your results.

#### **Answer**

``` r
library(collegeIncome)
data(college)
library(matahari)
```

``` r
dance_start(value = FALSE, contents = FALSE)
```

``` r
dance_save("~/Desktop/college_major_analysis.rds")
```

## Question 4

Please upload the file generated by matahari
(college_major_analysis.rds) to a **public** GitHub repository and paste
the link to that file here.

## Question 5
