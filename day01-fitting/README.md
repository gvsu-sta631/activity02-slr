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

You will be working through this activity for both Days 1 and 2 - these
are labeled with section headers “Day 1” and “Day 2” to help you. Before
opening the the `activity02.Rmd` file in the **Files** pane of RStudio,
take a few minutes to remind yourself of these best practices when
working in RMarkdown documents…

![check-in](../README-img/noun-magnifying-glass.png) **Check in**

Think of how you can use your Markdown skills from last week to help
keep your RMarkdown file neatly organized. I encourage you to treat the
`activity02.Rmd` file as a way to document you work. That is,

- Leave future you quality comments in your code,
- Provide a summary AND interpretation of your output (and make it clear
  to you when these differ),
- Practice telling your data’s story. Avoid summarizing what you did
  (your code does that). Instead, think about what your results mean in
  the data’s context.

### Friendly reminders when working in RStudio

- You might choose to install/load more packages as you work.

  - Only `install.packages` in your R **Console** and never in your
    RMarkdown file.
  - I like to load (`library`) packages at the top of my documents so
    that they are easy to find to remove if I do not end up using them.
    If you end up not using a package in your work, I recommend that you
    comment it out and also explain (in a comment) why you didn’t need
    it or end up using it. Note that this is mostly for when you are
    testing out new packages and likely not useful for a final report.

- As you work, you might want to create new R code chunks. Here are a
  few ways to do that:

  - I prefer to use keyboard shortcuts: Ctrl + Alt + I (mac users: Cmd +
    Option + I). I think, “‘I’ for ‘Insert’”.
  - You could also click on the Insert Code Chunk
    <img src="../README-img/code-chunk-icon.png" alt="code chunk" width = "20"/>
    icon near the upper right-hand corner of your `.Rmd` file.

- Knit your document frequently. First, this saves your work
  automatically. Second, this runs your code from a “vanilla” R session
  so it will let you know of any errors/warnings.

- Remember to organize your RMarkdown document using your Markdown
  skills. Use section headers, subsection headers, text formats (bold
  and italics), lists, etc. Avoid using section headers (`##`) to make
  text stand out (unless it is a header) and this make your document
  less accessible to individuals that rely on screen readers - bold and
  italic are better suited for this.

## What is next?

We will continue see how to assess SLR model fit using `{tidymodels}`
and a introduction to other validation methods.
