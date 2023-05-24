Day 2 - Assessing an SLR Model
================

In this repository/directory you should see two items:

- `README.md` - this document.

You will continue working in your `day01-fitting/activity02.Rmd` file
that you started on [Day 1](../day01-fitting)

## Task 1: Pull your changes from GitHub into RStudio

You successfully updated your GitHub repo, but we still need to update
your RStudio files. Read these directions first, then work through them.

- In the **Git** pane of RStudio (upper right-hand area), locate and
  click on the
  <img src="../README-img/pull-icon.png" alt="knit" width = "20"/>
  **Pull** icon.
- After a few moments (you might need to provide your GitHub username
  and PAT), your **Files** pane will be updated with the new items.

Since you are likely looking at the `README` (this page) on GitHub,
nothing of importance for your work today was brought in. However, it is
always a good habit to **pull** from GitHub before starting to work
after taking a break. For example, if you were collaborating on a
project with others, they might do work at different times than you (or
even at the same time). It is always good to solve problems on your end
before **push**ing to GitHub and causing more problems.

## Train-test splits

In Day 1, you used your entire dataset to fit an SLR model. However,
when we wish to evaluate how good a model is, using the same data does
not provide us with much information about how the model will perform on
new data. If our data is *sufficiently* large (a quite subjective
requirement and really specific to each problem), we can split our
dataset into two subsets:

- A **training** dataset that is used to fit our model, and
- A **testing** dataset to evaluate the fit of our model.

How do we know when we have a sufficiently large dataset? I will answer
this question with another question: If you were to subset your data
into two subset datasets, do you believe that each of these subset
datasets will representative samples of the population (assuming that
the original dataset was also representative of the population)? That is
(another question), are there enough observations to cover all common
cases and most uncommon cases in the population?

If your data does not seem sufficiently large, we will explore methods
better suited for the “small” datasets when we cover Chapter 5. For the
remainder of this section, I will walk through the process of creating
these two subset datasets and some other best practices for train-test
splits.

When splitting a dataset, we want to use random sampling to create the
two subset datasets.

Splits for train-test subset datasets are defined as a percentage of the
original dataset. Probably the most common split is to train on 80% of
the data, then test on 20%. However, these percentages are arbitrary and
you need to take into consideration the “sufficiently large” problem as
well as how long it will take a computer to analyze the data.

When using randomness to allocate observations to one of the two subset
datasets it is difficult to write reports unless you save the splits
into files. If you run the split code again, you will get different
allocations which will change your results. If you were to do all of
your work in one sitting, know exactly what to code, and make no
mistakes, this would not be a problem. However, [pobody’s
nerfect](https://idioms.thefreedictionary.com/pobody%27s+nerfect). A
solution to this is to use pseudo-randomness. That is, we will set a
seed to ensure we get the same random splits everytime we run our code.

Here I generate a random sample of 5 values pulled from a standard
normal distribution (a [normal
distribution](https://en.wikipedia.org/wiki/Normal_distribution) with a
mean of 0 and standard deviation of 1), then I generate another random
sample of 5 values (again from a standard normal distribution).

``` r
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -2.08190178  0.03169535  0.30296139  0.62555065 -0.46465036

``` r
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.37943400  0.09894424  1.30425850  0.21574878 -0.59060727

Notice that the results differ. Now I set a seed using the appropriately
named function `set.seed`. For simplicity, you provide this function
with any integer.

``` r
set.seed(631)
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.4750141  2.4155808  1.4483972  0.5968030  0.4631324

``` r
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.4044494  1.1611284  1.9393113 -1.4279279 -0.9133888

Notice that this does not produce the same results each time we call
`rnorm`. However, look what happens if we run that same code again.

``` r
set.seed(631)
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.4750141  2.4155808  1.4483972  0.5968030  0.4631324

``` r
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.4044494  1.1611284  1.9393113 -1.4279279 -0.9133888

The same two individual random samples! What if we set the seed each
time we generate a random sample?

``` r
set.seed(2023)
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.08378436 -0.98294375 -1.87506732 -0.18614466 -0.63348570

``` r
set.seed(2023)
rnorm(5, mean = 0, sd = 1)
```

    ## [1] -0.08378436 -0.98294375 -1.87506732 -0.18614466 -0.63348570

Yay! The same exact *random* samples. So how can we use this to create
our train-test splits? There are many ways, though we will stick to our
`{tidymodels}` workflow.

``` r
library(tidymodels)
# diamonds dataset from {ggplot2} (loaded with {tidymodels})
diamonds
```

    ## # A tibble: 53,940 × 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  0.23 Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
    ##  2  0.21 Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
    ##  3  0.23 Good      E     VS1      56.9    65   327  4.05  4.07  2.31
    ##  4  0.29 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
    ##  5  0.31 Good      J     SI2      63.3    58   335  4.34  4.35  2.75
    ##  6  0.24 Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
    ##  7  0.24 Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
    ##  8  0.26 Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
    ##  9  0.22 Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
    ## 10  0.23 Very Good H     VS1      59.4    61   338  4     4.05  2.39
    ## # … with 53,930 more rows

``` r
# set seed before random split
set.seed(1)
# put 80% of the data into the training set
diamonds_split <- initial_split(diamonds, prop = 0.80)

# assign the two splits to data frames - with descriptive names
diamonds_train <- training(diamonds_split)
diamonds_test <- testing(diamonds_split)

# splits
diamonds_train
```

    ## # A tibble: 43,152 × 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  0.41 Very Good D     SI2      62.3    61   638  4.72  4.75  2.95
    ##  2  0.5  Very Good F     VS2      62.8    57  1402  5.05  5.08  3.18
    ##  3  1.03 Fair      I     SI2      65.2    56  3530  6.42  6.35  4.16
    ##  4  1.1  Ideal     I     SI1      62.1    57  5037  6.6   6.64  4.11
    ##  5  1.51 Very Good E     VS2      63.3    61 13757  7.24  7.17  4.56
    ##  6  0.3  Ideal     H     VS2      62.1    55   457  4.3   4.33  2.68
    ##  7  0.87 Premium   J     SI1      61.4    57  2321  6.17  6.14  3.78
    ##  8  1.05 Very Good H     VS1      63.3    57  5657  6.45  6.4   4.07
    ##  9  1    Good      F     SI1      64      57  4372  6.29  6.33  4.04
    ## 10  2.01 Good      I     SI1      63.8    57 13976  7.95  7.91  5.06
    ## # … with 43,142 more rows

``` r
diamonds_test
```

    ## # A tibble: 10,788 × 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  0.3  Good      J     SI1      64      55   339  4.25  4.28  2.73
    ##  2  0.3  Very Good J     VS2      62.2    57   357  4.28  4.3   2.67
    ##  3  0.23 Very Good F     VS1      60.9    57   357  3.96  3.99  2.42
    ##  4  0.23 Very Good F     VS1      59.8    57   402  4.04  4.06  2.42
    ##  5  0.23 Very Good D     VS1      61.9    58   402  3.92  3.96  2.44
    ##  6  0.23 Good      F     VS1      58.2    59   402  4.06  4.08  2.37
    ##  7  0.23 Good      E     VS1      64.1    59   402  3.83  3.85  2.46
    ##  8  0.32 Good      H     SI2      63.1    56   403  4.34  4.37  2.75
    ##  9  0.32 Good      H     SI2      63.8    56   403  4.36  4.38  2.79
    ## 10  0.3  Ideal     I     SI2      61      59   405  4.3   4.33  2.63
    ## # … with 10,778 more rows

Notice the dimensions of these splits (about 40k in the training set and
10k in the testing set - for 80% of the original data in the training
set). Now we can build our model using `*_train` and `predict` (remember
from Activity 1, Day 3?) using `*_test`.

Note: Random samples are one way to create train-test splits. Suppose
that you have data collected over two years. It would then make more
sense to treat the first year as your train dataset, then evaluate your
model on the second year.

## Task 2: Try it another way

- Open your `../day01-fitting/activity02.Rmd` file and
  <img src="../README-img/knit-icon.png" alt="knit" width = "20"/>
  **knit** it to run the work you completed during Day 1 of this
  activity.

Rather than redoing everything you worked on during last class period,
create a new section in your document (give it a descriptive header) to
continue our work today.

- Using the example code provide to you in [the previous
  section](#Train-test-splits), split your data into training and
  testing subsets. Remember to create a new R code chunk and provide a
  descriptive title.
- Using only your *training* data, replicate your work from Day 1 (i.e.,
  explore, fit, and describe). Remember to create new R code chunks with
  descriptive titles AND provide some narrative to explain your results.
  My encouragement is to discuss why you are doing things, not what you
  did (your code will show what you did).

## Task 3: Assess with your training data

Back in [Activity 1, Day
3](https://github.com/gvsu-sta631/activity01-course-tools/tree/main/day03-rstudio-r),
you worked through a complete(ish) SLR analysis in your
`activity01-day03-slr.Rmd` file.

- Still using your *training* data, assess how well your model fits
  these data. You can refer to the these two sections from your
  `activity01-day03-slr.Rmd` file: **4. Assess our model** and **Model
  diagnostics** Remember to create new R code chunks with descriptive
  titles AND provide some narrative to explain your results.

## Task 4: Assess with your testing data

You just fit a model and evaluated it using the exact same data. This is
a bit of circular reasoning and does not provide much information about
the model’s performance. Luckily, you still have your *untouched*
testing data!

- In a new R code chunk (with descriptive title), add the following
  code. Note that you might need to change `slr_fit` to whatever you
  assigned your model output to and `data_test` to whatever you assigned
  your testing data to.

``` r
slr_aug <- augment(slr_fit, new_data = data_test)
slr_aug
```

This takes your SLR model and applies it to your testing data. The
`.fitted` column in this output is the same as doing the following
(remember the `predict` function from Activity 1, Day 3?):

``` r
predict(slr_fit, new_data = data_test)
```

Now, using Sections **5. Predict** and **Model diagnostics** from your
`activity01-day03-slr.Rmd` file as an example, assess how well your
model fits your testing data. Compare your results here to your results
from Day 1 of this activity. Did this model perform any differently?

## What is next?

We will explore how to fit multiple linear regression (MLR) models with
only quantitative explanatory variables. The next week we will explore
MLR models with qualitative explanatory variables, interactions between
variables, and how to address potential problems that arise with linear
models. Then, the following week will be the first **Mini-competition**
(with prize opportunities!).
