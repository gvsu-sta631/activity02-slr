Day 1 - Fitting an SLR Model
================

In this repository/directory you should see two items:

- `README.md` - this document.
- `activity02.Rmd` - the file you will complete in RStudio.

For today’s portion, we are going to focus on descriptive analyses of
your data: visualizations, numerical summaries, and describing model
parameter estimates. We also dig into the concept of *sum of squared
residuals*. Day 2 will further our assessment of SLR models and
introduce creating training and testing subsets.

## Task 1: Open the RMarkdown document

Read these directions first, then work through them.

- In the **Files** pane of RStudio, locate and click on the
  `activity02.Rmd` file to open it.
- This file is essentially a blank document with only a `title` and
  `output` option (to produce a GitHub friendly Markdown file). You will
  follow the tasks in this `README` file and do the work (coding,
  writing, etc.) in RStudio.

![check-in](../README-img/noun-magnifying-glass.png) **Check in**

Think of how you can use your Markdown skills from last week to help
keep your RMarkdown file neatly organized. I encourage you to treat the
`activity02.Rmd` file as a way to document you work. That is,

- Leave future you quality comments in your code,
- Provide a summary AND interpretation of your output,
- Practice telling your data’s story. Avoid summarizing what you did
  (your code does that). Instead, think about what your results mean in
  your data’s context.

Before we get too far, underneath the R Code Chunk titled
`global-options` (essentially the only thing in this document), provide
a description of your data:

1.  Explain why you chose that - why is it interesting to you?
2.  Explain where you obtained your data from.
3.  Who created this dataset?

I will invite you to update this section on the second day of this
activity.

## Task 2: Load the necessary packages

I provided you with examples of how to fit a simple linear regression
model using two packages from Posit (formerly
[RStudio](https://posit.co/)): `{tidyverse}` and `{tidymodels}`. If you
would like to develop your skills with these packages, I strongly
recommend [Emil Hvitfeldt](https://www.emilhvitfeldt.com/)’s (of Posit)
[complementary online text of *ISL*s lab
sections](https://emilhvitfeldt.github.io/ISLR-tidymodels-labs/index.html).

When loading any packages, be sure to:

- In the **Packages** pane of RStudio, check if they are already
  installed. Be sure to check both your **User Library** and the
  **System Library**.

- If they are not listed, install them in your **Console** pane, by
  typing the following - replacing `package_name` with the appropriate
  name - and press Enter/Return afterwards.

  ``` r
  install.packages("package_name")
  ```

- Once you have verified that the packages are installed, load them
  packages in an R chunk. Be sure that you provide a descriptive code
  chunk title. Then type the following for as many packages as you are
  loading (one `library` per `{package}`):

  ``` r
  library(package_name)
  ```

Some helpful notes:

- You might need to load more packages as you work. Add those to this
  same place. If you end up not using a package, comment it out and
  explain why you didn’t need it or end up using it.

- To create R code chunks:

  - My favorite method is to use keyboard shortcuts: Ctrl + Alt + I (mac
    users: Cmd + Option + I).
  - You could also click on the Insert Code Chunk
    <img src="../README-img/code-chunk-icon.png" alt="code chunk" width = "20"/>
    icon near the upper right-hand corner of your `.Rmd` file.

- Knit your document frequently. First, this saves your work
  automatically. Second, this runs your code from a “vanilla” R session
  so it will let you know of any errors/warnings.

- Remember to organize your RMarkdown document using your Markdown
  skills. Use section headers, subsection headers, text formats (bold
  and italics), lists, etc.

## Task 3: Load your data

In Activity 1, you read data from a website. Your data might not be
accessible like data from *OpenIntro*.

Explore different ways to load in your data. For example, what do you
need to upload your data into your cloned (local version) RStudio
repository? Note that this might be difficult if you have a very large
dataset. One of my favorite methods for reading in large data that I
don’t want to also push to GitHub is to load it to my Google Drive, then
access it using
[`{googlesheets4}`](https://googlesheets4.tidyverse.org/) from the
brilliant Dr. Jenny Bryan.

- Create a new R code chunk to read in your data and provide a
  descriptive title.
- Access your data and assign it (i.e., `<-`) to an R data frame (we
  used `readr::read_csv` in Activity 1 for a CSV file) with a
  descriptive name.

After doing this and viewing the loaded data, answer the following
questions:

1.  What are the dimensions of the dataset? What does each row
    represent?

2.  Do you have multiple measurements over time? Across different
    locations? Do you plan on focusing on all of these values? Do you
    need to subset your dataset to be more focused? For example, we
    focused on data from the year 2016 in Activity 1.

3.  What two variables are you focusing on? That is, what is your
    research question and what information do you have to explore this
    question? Keep in mind that for this activity we are focusing on SLR

## Task 4: Explore your data

4.  Create a new R code chunk (or multiple R code chunks) and plot each
    of your variables - separately and together. Be sure to describe
    what you notice/wonder. Does the relationship look linear?

## Task 5: Sum of squared residuals

In this section, you will use an interactive function provided by the
OpenIntro team to investigate what is meant by “sum of squared
residuals”. You will need to run this function in your **Console**, not
in your markdown document. Running the function also requires that the
`hfi_2016` dataset is loaded in your environment (verify this is listed
in the **Environment** pane). You will also need to make sure the Plots
tab in the lower right-hand corner has enough space to make a plot (you
can use your mouse to make this area horizontally and vertically
larger).

- In your **Console** (**NOT** in your `.Rmd` file), type the
  following - replace `x_variable`, `y_variable`, and `data_name` with
  the appropriate details from your data. Be sure to press Enter/Return
  after each line.

  ``` r
  install.packages('statsr')
  statsr::plot_ss(x = x_variable, y = y_variable, data = data_name)
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
and intercept of your line as well as the sum of squared residuals.

Answer the following question:

Use `statsr::plot_ss` to choose a line that does a good job of
minimizing the sum of squares. Run the function several times.

Answer the following questions:

5.  What was the smallest sum of squares that you got? What was the
    relationship between your line and the data points?
6.  What was the largest sum of squares you got? What was the
    relationship between your line and the data points?

## Task 5: The linear model

It is rather cumbersome to try to get the correct least squares line -
i.e., the line that minimizes the sum of squared residuals - through
trial and error. Instead, you can use R to fit the linear model (i.e.,
the regression line).

Recall that in Activity 1 we did the following:

``` r
# Created a parsnip specification for a linear model

lm_spec <- linear_reg() %>%
  set_mode("regression") %>%
  set_engine("lm")

# Fit our specification to our data

slr_mod <- lm_spec %>% 
fit(y_variable ~ x_variable, data = data_name)

# View our model output
tidy(slr_mod)
```

With your *tidy* output, write down the least squares regression line
for the linear model. Hint fill in the appropriate information:

$$
\hat{y} = b_0 + b_1 \times x
$$

Using your equation…

5.  Interpret the *y*-intercept.

6.  Interpret the slope

## What is next?

We will continue exploring how to fit SLR models and assess their fit
using `{tidymodels}` and introduce creating training and testing
subsets.
