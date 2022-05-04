# Data_606_Final_Project:
![title1](/visual_charts/title1.jpg)

This is an experimental study where a group of 249 mice were monitored after administrating a variety of drug regimens over a 45-day treatment period. The impact of Capomulin drug on tumor growth, and survival rates were monitored, along with Infubinol, Ketapril, and Placebo.
- There are 10 different drug treatments. 
- Four drug treatments: Capomulin, Infubinol, Ketapril, and - Placebo.
- Sample size of mice is 25 for each drug of interest.

# Research Question:
- Question 1: Is Capomulin effective more effective in reducing the tumor size than Infubinol, or Ketapril?
- Question 2: Is there a correlation between the age, weight and the tumor size growth for each drug category?
- Hypothesis Test:
- Null Hypothesis: There is no difference between the mean percent change in tumor volume for the four drug categories.
- Alternate Hypothesis: There is a difference between the mean percent change in tumor volume for the four drug categories.

## Approach for answering the research question:
1- Calculate the mean percent change in tumor volume for the four drug categories.
2- Perform the One-Way Variance (Anova) Hypothesis test to find out whether or not the difference exist between the mean tumor size for all four drug categories.
3- Perform linear regression to study the correlation between various variables by calculating the correlation coefficient.
4- Finally analyze the results to find out if Capomulin more or less effective in reducing the tumor size of sample mice than Infubinol, or Ketapril.

# Response & Explanatory Variable

- The response variable is the size of tumor, “Tumor.Volume..mm3.” and it holds a numerical data.(being measured)

- The explanatory variable are the “Drug.Regimen” which holds a categorical data and “Timepoint” which holds numerical data. The ‘Timepoint’ unit is days.

- The two datasets, metadata and results are read into Rmd file and merged together.

- After thorough exploratory data analysis and cleaning of data, the summary statistics are calculated.

- The initial Tumor Volume at starting timepoint zero is 45 mm3 for all mice.

![bar plot](/visual_charts/barplot.png)

You can see the negative bar showing the reduce size of tumor volume.

![box plot](/visual_charts/boxplot.png)

# Analysis for the box plots: 

The drug categories represented on the x_axis and percent change in tumor size on the y_axis.

Infubinol drug category has one datapoint indicating the outlier. 

Infubinol and Ketapril shows that the median and mean are closely alligned, which shows data is normally distributed, and we can ignore the outlier in Infubinol.

Ketapril drug category has more variance of data points than the Infubinol drug category.

The mean < median for the Capomulin, is making it left skewed. Also, the percent change is tumor size is below zero, showing that the Capomulin is effective in reducing the size of the tumor.

Since Capomulin appears to be different than Infubinol and Ketapril, this is an indication that we will find the difference between means of Capomulin and the other two categories.

# QQ plot and Shapiro-Wilk test of normality:

![assumptions](/visual_charts/assumption_test.png)

## To compare the means of three or more samples, One Way Variance (Anova) is the most appropriate test to use.

### Performing the test of normality.

The ANOVA test makes a few assumptions about the data:

- Independence of the observations. Each subject should belong to only one group. 
- No significant outliers in any group
- Normality. the data for each group should be approximately normally distributed.
- Homogeneity of variances. The variance of the outcome variable should be equal in every group.

![shapiro test](/visual_charts/shapiro_wilktest.png)

![grp_assumption](/visual_charts/norm_grp_test.png)

## Performing a Shapiro-Wilk test of normality

In the QQ plot that I showed previously, all the points fall approximately along the reference line, so we can assume normality. 
This conclusion is supported by the Shapiro-Wilk test. 
The p-value is not significant (p = 0.6), so we can assume normality.
The score were normally distributed (p > 0.05) for each group, as assessed by Shapiro-Wilk’s test of normality.

## Homogeneity of variance assumption

![homogeneity test](/visual_charts/homog_test.png)

In the plot above, there is no evident relationships between residuals and fitted values (the mean of each groups), which is good. So, we can assume the homogeneity of variances.

![hypothesis test](/visual_charts/hypothsis_test.png)

### Report: 
Degree of freedom: 3, since we have 4 categories, so 4-1 =3 degree of freedom
Sum of Squares: 5.3104
Mean Sum of Squares: 1.7701
F-Statistics: 69.737, F(3, 96) = 69.74

### Conclusion:

The F-value in an ANOVA is calculated as: variation between sample means / variation within the samples.
The higher the F-value in an ANOVA, the higher the variation between sample means relative to the variation within the samples.
The higher the F-value, the lower the corresponding p-value.


Here the p-Value, tells weather or not we found significance difference or not. 
The p-Value: 2.2e-16,  less than alpha=0.05 shows that we found the difference in at one of the means in the data sample. And that is what we suspected from the boxplot analysis.

Since the p-value is below a threshold (α = .05), we can reject the null hypothesis of the ANOVA and conclude that there is a statistically significant difference between group means.

Therefore, we can reject the null hypothesis that there is no difference between the means in the data sample.

But we are not sure about which category mean is different, so we perform Post-hoc tests to determine that.

# Post-hoc Test:

![post hoc calc](/visual_charts/post_hoc_calc.png)

A significant one-way ANOVA is generally followed up by Tukey post-hoc tests to perform multiple pairwise comparisons between groups.

# Report TukeyHSD Results:

when p-adj < p-value, there is a significant difference between the two categories mean.

the lwr and upr bounds  shows that we are 95% confident that the true mean lies between the lwr and upr bounds of confidence Interval.

The p-Value for Infubinol-Capomulin, Ketapril-Capomulin, Placebo-Capomulin is less than alpha=0.05 and that shows there is significant difference between the means of these categories.

The p-Value for the other three group comparison is greater than alpha=0.05 shows there is no significant difference between the means of these categories.

Thus, we conclude that, Capomulin is more effective in reducing the tumor size than Infubinol, or Ketapril. 

In the visualization the middle line on each bar  shows the difference in mean for different drug categories .

Both end limits on each bar shows the upper and lower limits of confidence intervals.

# Regression Model for Analyzing Correlation between Age, weight and Tumor_Volume_mm3

![alt text](/visual_charts/lm_calc.png)

When building regression models, we hope that this p-value is less than some significance level because it indicates that the predictor variables are actually useful for predicting the value of the response variable.

we used an alpha level of α = .05 to determine which predictors is significant in this regression model, we’d say that weight is accounting for most of the variance, which has (p=1.49e-08) < is (α = .05) and is statistically significant predictors.

while age (p=0.481 ) > is (α = .05) and is not statistically significant predictors.

Estimate: The estimated coefficient. This tells us the average increase in the response variable associated with a one unit increase in the predictor variable, assuming all other predictor variables are held constant.

Std. Error: This is the standard error of the coefficient. This is a measure of the uncertainty in our estimate of the coefficient.

t value: This is the t-statistic for the predictor variable, calculated as (Estimate) / (Std. Error).

Residual standard error: This tells us  the average distance that the observed values fall from the regression line. The smaller the value, the better the regression model is able to fit the data.

I performed the regression test for weight and age verses tumor size separately and come up with the same result in my Rmd file

Adjusted R-squared: This is a modified version of R-squared that has been adjusted for the number of predictors in the model. It is always lower than the R-squared.

F-statistic: This indicates whether the regression model provides a better fit to the data than a model that contains no independent variables. In essence, it tests if the regression model as a whole is useful.

![lm wt](/visual_charts/lm_wt.png)

Multiple R-Squared: This is known as the coefficient of determination. It tells us the proportion of the variance in the response variable that can be explained by the predictor variables. This value ranges from 0 to 1. The closer it is to 1, the better the predictor variables can predict the value of the response variable.

p-value: This is the p-value that corresponds to the F-statistic. If this value is less than some significance level (e.g. 0.05), then the regression model fits the data better than a model with no predictors.


![lm age](/visual_charts/lm_age.png)


# Final Conclusion:

## Why is this analysis important?

ANOVA test determines the difference in mean between two or more independent groups. 

 It provides the overall test of equality of group means. 

 It can control the overall type I error rate (i.e., false positive finding)

## Limitations of the analysis?

One-way ANOVA can only be used when investigating a single factor and a single dependent variable. When comparing the means of three or more groups, it can tell us if at least one pair of means is significantly different, but it can't tell us which pair.

ANOVA assumes that the data is normally distributed. The ANOVA also assumes homogeneity of variance, which means that the variance among the groups should be approximately equal. ANOVA also assumes that the observations are independent of each other.

# Data Source Links:

The datasets are provided by Pymaceuticals Inc.. Below is the link for the original source of the datasets:


[Data Source](
https://c-l-nguyen.github.io/web-design-challenge/index.html
)


The raw datasets are imported from the GitHub links provided below:


[Raw Data GitHub Link1](https://raw.githubusercontent.com/rfpoulos/pymaceuticals/master/data/Mouse_metadata.csv
)

[Raw Data GitHub Link2](https://raw.githubusercontent.com/rfpoulos/pymaceuticals/master/data/Study_results.csv
)










