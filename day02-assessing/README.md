Day 2 - Assessing an SLR Model
================

In this repository/directory you should see two items:

- `README.md` - this document.

You will continue working in your `day01-fitting/activity02-day01.Rmd`
file that you started on [Day 1](../day01-fitting)

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

## Task 2: Overall model fit

- Open your `day01-fitting/activity02-day01.Rmd` file and
  <img src="../README-img/knit-icon.png" alt="knit" width = "20"/>
  **knit** it to run the work you completed during Day 1 of this
  activity.

Hopefully, you were able to interpret the SLR model parameter estimates
(i.e., the *y*-intercept and slope) as follows:

> For countries with a `pf_expression_control` of 0 (those with the
> largest amount of political pressure on media content), we expect
> their mean personal freedom score to be 4.28.

> For every 1 unit increase in `pf_expression_control`, we expect a
> country’s mean personal freedom score to increase 0.542 units.

Looking back at the scatterplot you created during Day 1 of this
activity. If the relationship looks linear, we can quantify the strength
of the relationship with the correlation coefficient (often denoted
$r$).

- Create a new R code chunk.
- Using your `{dplyr}` skills, obtain the correlation coefficient (hint:
  explore the `cor` function from Base R) between
  `pf_expression_control` and `pf_score`.

After doing this and running the code, answer the following questions:

1.  What does this value mean in the context of this model?

Now we would like to assess our model fit using $R^2$, the proportion of
variability in the response variable that is explained by the
explanatory variable. We use `broom::glance` (remember that `{broom}` is
loaded when you load `{tidymodels}`) to access this information.

- Create a new R code chunk and type the following code.

  ``` r
  glance(m1)
  ```

After doing this and running the code, answer the following questions:

2.  What is the value of $R^2$ for this model?
3.  What does this value mean in the context of this model?
4.  Fit a new model that uses `pf_expression_control` to predict
    `hf_score`, or the total human freedom score. Using the estimates
    from the R output, write the equation of the regression line. What
    does the slope tell us in the context of the relationship between
    human freedom and the amount of political pressure on media content?

## Task 3: Prediction and prediction errors

Before we start predicting, you will first create a scatterplot with the
least squares line for `m1` laid on top.

- Copy-and-paste the *entire* code chunk of the scatterplot you created
  in Day 1 of this activity below.
- Add a layer to this (remember how `{ggplot2}` represents adding
  various data layers to plots) that shows a *smooth* line *geometry*.
- In this layer, be sure to specify the `method` as `"lm"` and do
  **not** display confidence intervals around your bands (hint: look at
  the help documentation for the layer you added).

This line can be used to predict $y$ at any value of $x$. When
predictions are made for values of $x$ that are beyond the range of the
observed data, it is referred to as *extrapolation* and is not usually
recommended. However, predictions made within the range of the data are
more reliable. They’re also used to compute the residuals.

Answer the following question:

6.  If someone saw the least squares regression line and not the actual
    data, how would they predict a country’s personal freedom school for
    one with a 3 rating for `pf_expression_control`?
7.  Is this an overestimate or an underestimate, and by how much? In
    other words, what is the individual residual value for this
    prediction?

## Task 4: Model diagnostics

To assess whether the linear model is reliable, we should check for (1)
linearity, (2) nearly normal residuals, and (3) constant variability.
Note that the normal residuals is not really necessary for all models
(sometimes we simply want to describe a relationship for the data that
we have or population-level data, where statistical inference is not
appropriate/necessary).

In order to do these checks we need access to the fitted (predicted)
values and the residuals. We can use `broom::augment` to calculate
these.

- Create a new R code chunk and type the following code.

  ``` r
  m1_aug <- augment(m1)
  ```

![check-in](../README-img/noun-magnifying-glass.png) **Check in**

Look at the various information produced by this code. Can you identify
what each column represents?

**Linearity**: You already checked if the relationship between
`pf_score` and `pf_expression_control` is linear using a scatterplot. We
should also verify this condition with a plot of the residuals
vs. fitted (predicted) values.

- Create a new R code chunk and type the following code.

  ``` r
  ggplot(data = m1_aug, aes(x = .fitted, y = .resid)) +
    geom_point() +
    geom_hline(yintercept = 0, linetype = "dashed", color = "red") +
    xlab("Fitted values") +
    ylab("Residuals")
  ```

Notice here that `m1_aug` can also serve as a data set because stored
within it are the fitted values ($\hat{y}$) and the residuals. Also note
that we are getting fancy with the code here. After creating the
scatterplot on the first layer (first line of code), we overlay a red
horizontal dashed line at $y = 0$ (to help us check whether the
residuals are distributed around 0), and we also rename the axis labels
to be more informative.

Answer the following question:

8.  Is there any apparent pattern in the residuals plot? What does this
    indicate about the linearity of the relationship between the two
    variables?

**Nearly normal residuals**: To check this condition, we can look at a
histogram of the residuals.

- Create a new R code chunk and type the following code.

  ``` r
  ggplot(data = m1_aug, aes(x = .resid)) +
    geom_histogram(binwidth = 0.25) +
    xlab("Residuals")
  ```

Answer the following question:

9.  Based on the histogram, does the nearly normal residuals condition
    appear to be violated? Why or why not?

**Constant variability**:

10. Based on the residuals vs. fitted plot, does the constant
    variability condition appear to be violated? Why or why not?

## Challenge: More practice

- Choose another variable that you think would strongly correlate with
  `pf_score`. Produce a scatterplot of the two variables and fit a
  linear model. At a glance, does there seem to be a linear
  relationship?

- How does this relationship compare to the relationship between
  `pf_score` and `pf_expression_control`? Use the $R^2$ values from the
  two model summaries to compare. Does your independent variable seem to
  predict `pf_score` better? Why or why not?

- Check the model diagnostics using appropriate visualizations and
  evaluate if the model conditions have been met.

- Pick another pair of variables of interest and visualize the
  relationship between them. Do you find the relationship surprising or
  is it what you expected. Discuss why you were interested in these
  variables and why you were/were not surprised by the relationship you
  observed.

## What is next?

We will next explore how to fit multiple linear regression models and
assess their fit using `{tidymodels}`.
