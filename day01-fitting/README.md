Day 1 - Fitting an SLR Model
================

In this repository/directory you should see two items:

- `README.md` - this document.
- `activity02-day01.Rmd` - the file you will complete in RStudio.

## Task 1: Open the RMarkdown document

Read these directions first, then work through them.

- In the **Files** pane of RStudio, locate and click on the
  `activity02-day01.Rmd` file to open it.
- This file is essentially a blank document with only a `title` and
  `output` option (to produce a GitHub friendly Markdown file). You will
  follow the tasks in this `README` file and do the work (coding,
  responding, etc.) in RStudio.

![check-in](../README-img/noun-magnifying-glass.png) **Check in**

Think of how you can use your Markdown skills from last week to help
keep your RMarkdown file neatly organized. Also, be as descriptive in
your response to questions and even leave comments in your code to help
you understand what you are doing.

## Task 2: Load the necessary packages

We will be using two packages from Posit (formerly
[RStudio](https://posit.co/)): `{tidyverse}` and `{tidymodels}`. If you
would like to try the *ISLR* labs using these two packages instead of
base R, [Emil Hvitfeldt](https://www.emilhvitfeldt.com/) (of Posit) has
put together a [complementary online
text](https://emilhvitfeldt.github.io/ISLR-tidymodels-labs/index.html).

- In the **Packages** pane of RStudio, check if `{tidyverse}` and
  `{tidymodels}` are installed. Be sure to check both your **User
  Library** and **System Library**.

- If either of these are not currently listed, type the following in
  your **Console** pane, replacing `package_name` with the appropriate
  name, and press Enter/Return afterwards.

  ``` r
  install.packages("package_name")
  ```

- Once you have verified that both `{tidyverse}` and `{tidymodels}` are
  installed, load these packages in the R chunk titled `setup`. Press
  Enter/Return after line 7 to add more code lines, then type the
  following:

  ``` r
  library(tidyverse)
  library(tidymodels)
  ```

- Run the `setup` code chunk or **knit**
  <img src="../README-img/knit-icon.png" alt="knit" width = "20"/> icon
  your Rmd document to verify that no errors occur.

Remember to organize your RMarkdown document using your Markdown skills.

## Task 3: Load the data and

The data we’re working with is from the OpenIntro site:
`https://www.openintro.org/data/csv/hfi.csv`

- Create a new R code chunk to read in the linked CSV file.
- Rather than downloading this file, uploading to RStudio, then reading
  it in, explore how to load this file directly from the provided URL
  with `readr::read_csv` (`{readr}` is part of `{tidyverse}`).
- Assign this data set into a data frame named `hfi` (short for “Human
  Freedom Index”).

After doing this and viewing the loaded data, answer the following
questions:

1.  What are the dimensions of the dataset? What does each row
    represent?

- The dataset spans a lot of years. We are only interested in data from
  year 2016.
  - Create a new R code chunk,
  - Filter the data `hfi` data frame for year 2016, and
  - Assign the result to a data frame named `hfi_2016`.

2.  What type of plot would you use to display the relationship between
    the personal freedom score, `pf_score`, and `pf_expression_control`?

- Create a new R code chunk and plot this relationship using the
  variable `pf_expression_control` as the predictor.

3.  Does the relationship look linear? If you knew a country’s
    `pf_expression_control`, or its score out of 10, with 0 being the
    most, of political pressures and controls on media content, would
    you be comfortable using a linear model to predict the personal
    freedom score?

## Task 4: Sum of squared residuals

In this section, you will use an interactive function provided by the
OpenIntro team to investigate what is meant by “sum of squared
residuals”. You will need to run this function in your **Console**, not
in your markdown document. Running the function also requires that the
`hfi_2016` dataset is loaded in your environment (verify this is listed
in the **Environment** pane). You will also need to make sure the Plots
tab in the lower right-hand corner has enough space to make a plot (you
can use your mouse to make this area horizontally and vertically
larger).

- In your **Console**, type the following. Be sure to press Enter/Return
  after each line.

  ``` r
  install.packages('statsr')
  statsr::plot_ss(x = pf_expression_control, y = pf_score, data = hfi_2016)
  ```

- After running this command, you’ll be prompted to click two points on
  the plot to define a line. Once you’ve done that, the line you
  specified will be shown in black and the residuals in blue.

If your plot is appearing below a previous code chunk and will not let
you select points to make a line, take the following steps:

- Go to the Tools bar at the top of RStudio
- Click on “Global Options…”
- Click on the “R Markdown pane” (on the left)
- Uncheck the box that says “Show output inline for all R Markdown
  documents”

Recall that the residuals are the difference between the observed values
and the values predicted by the line:

$$
  e_i = y_i - \hat{y}_i
$$

The most common way to do linear regression is to select the line that
minimizes the sum of squared residuals. To visualize the squared
residuals, you can rerun the plot command and add the argument
`showSquares = TRUE`.

Note that the output from `statsr::plot_ss` provides you with the slope
and intercept of your line as well as the sum of squares.

Answer the following question:

4.  Using `statsr::plot_ss`, choose a line that does a good job of
    minimizing the sum of squares. Run the function several times. What
    was the smallest sum of squares that you got? How does it compare to
    your neighbour’s?

## Task 5: The linear model

It is rather cumbersome to try to get the correct least squares line,
i.e. the line that minimizes the sum of squared residuals, through trial
and error. Instead, you can use the `lm` function from base R to fit the
linear model (i.e., the regression line).

- Create a new R code chunk and type the following, then run your code
  chunk or knit your document.

  ``` r
  m1 <- lm(pf_score ~ pf_expression_control, data = hfi_2016)
  ```

The first argument in the function `lm()` is a formula that takes the
form `y ~ x`. Here it can be read that we want to make a linear model of
`pf_score` as a function of `pf_expression_control`. The second argument
specifies that R should look in the `hfi` data frame to find the two
variables.

**Note:** Piping (`%>%`) **will not** work here, as the data frame is
not the first argument!

The output of `lm` is an object that contains all of the information we
need about the linear model that was just fit. We can access this
information using `broom::tidy` (`{broom}` is part of `{tidymodels}`).

- In the previous R code chunk add the following line.

  ``` r
  tidy(m1)
  ```

Let’s consider this output piece-by-piece. First, the formula used to
describe the model is shown at the top, in what’s displayed as the
“Call”. After the formula you find the five-number summary of the
residuals. The “Coefficients” table shown next is key; its first column
displays the linear model’s y-intercept and the coefficient of
`pf_expression_control`. With this table, we can write down the least
squares regression line for the linear model:

$$
\hat{y} = 4.28 + 0.542 \times pf\_expression\_control
$$

Using this equation…

5.  Interpret the *y*-intercept.

6.  Interpret the slope

## What is next?

We will continue exploring how to fit SLR models and assess their fit
using `{tidymodels}`.
