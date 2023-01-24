Activity 02 - Simple Linear Regression (SLR)
================

This activity is intended to be completed in one week - outside of class
preparation work and two 75-minute class meetings. On our Blackboard
course site you were provided with items to read, watch, and do prior to
attempting this activity. Do not proceed in this activity until you have
minimally:

1.  (Day 1 portion) Read ISL [Sections 3.0 (the chapter introduction) &
    3.1.1](https://rdcu.be/c3STG).
2.  (Day 2 portion) Read ISL [Sections 3.1.2 &
    3.1.3](https://rdcu.be/c3STG).

In this repository/directory, you should see five items:

- `README-img` - a folder containing images that I am embedding within
  this `README.md` file and other files. You do not need to do anything
  with this.
- `.gitignore` - a file that is used to specify what Git can ignore when
  pushing to GitHub. You do not need to do anything with this.
- `README.md` - the document you are currently reading.
- `day01-fitting` - a folder that contains items for you to complete
  during the first 75-minute class meeting.
  <!-- - `day02-assessing` - a folder that contains items for you to complete during the second 75-minute class meeting. -->

We will explore most of these items over this week. Before doing that,
you will first make your own copy of this repository.

![check-in](README-img/noun-magnifying-glass.png) **Check in**

Do you want an interactive way to check your understanding outside of
class? Though not a perfect fit for our class,
[OpenIntro](https://www.openintro.org/team/) is a team of passionate
educators focused on increasing access to education (in particular
introductory statistics and mathematics). [Benjamin
Baumer](https://beanumber.github.io/www/) (associate professor at Smith
College), in collaboration with the OpenIntro team and others, created a
series of interactive tutorials using `{learnr}` that follow the
OpenIntro books (if you took STA 418/518 with me, you have experienced
these types of tutorials before with the assigned preparation
[Primers](https://posit.cloud/learn/primers)). The following tutorials
will provide you with an applied approach to our topics (reorganized to
better correspond with our readings):

Day 1:

- 3.1 - [Visualizing two
  variables](https://openintro.shinyapps.io/ims-03-model-01/)
- 3.3 - [Simple linear
  regression](https://openintro.shinyapps.io/ims-03-model-03/)
- 3.4 - [Interpreting regression
  models](https://openintro.shinyapps.io/ims-03-model-04/)

Day 2:

- 3.2 - [Correlation](https://openintro.shinyapps.io/ims-03-model-02/)
- 3.5 - [Model fit](https://openintro.shinyapps.io/ims-03-model-05/)

## STA 631 Topics Overview

Before we get into the work of this activity, I thought it would be
beneficial to align the textbook topics with our course schedule along
with provide some ideas for extending your learning. We will also use
this time to brainstorm tasks for this semester: assignments, projects,
etc. Essentially, ways to demonstrate and reflect on your learning of
the STA 631 [course
objectives](https://dykesb.netlify.app/courses/sta631/#course-objectives).

| Week | ISLR                               |
|------|------------------------------------|
| 2    | Ch 1 & 2                           |
| 3    | Sec 3.0 & 3.1                      |
| 4    | Sec 3.2                            |
| 5    | Sec 3.3 (opt 3.4 - 3.6)            |
| 6    | Sec 4.0 - 4.2                      |
| 7    | Sec 4.3                            |
| 8    | Sec 4.4 (opt 4.5)                  |
| 9    | Spring Break                       |
| 10   | Sec 4.6 (opt 4.7)                  |
| 11   | Ch 5 (opt 5.4)                     |
| 12   | Sec 6.0 - 6.2, 6.4 (opt 6.3 & 6.5) |
| 13   | Ch 13 (opt 13.6)                   |

Looking at the remaining chapters, this is my understanding of how they
fit into GVSU’s DSA program.

- Ch 7: Are Ch 1 – 3 mostly review? Consider exploring this as a project
  idea.
- Ch 8: CIS 635 & 678
- Ch 9: Do you want to extend Sec 4.2? Consider exploring this as a
  project idea.
- Ch 10: CIS 678 & maybe 677
- Ch 11: STA 628 (elective)
- Ch 12: STA 526 & CIS 678, maybe 635

![check-in](README-img/noun-magnifying-glass.png) **Check in**

- How do we want to demonstrate your learning? Some of my ideas are:
  - Who are you? (You did this with your Positionality Statement)
  - What do you currently know? (This will be assigned end of this week
    or beginning of next.)
  - Where are you going and how will you know when you get there? (This
    will be assigned around the middle of the semester.)

Notice that these are more focused on you and your growth. This is
important to me and I hope you will see how this is important to future
you. However, I also want to provide you with opportunities to
demonstrate what you have learned. What do you want this to look like?
How will we share this with me and your peers in STA 631? Do we want to
share it with others (faculty, potential employers, etc.)?

## Task 1: Forking the Repository

Read these directions first, then work through them. In this GitHub repo
(i.e., my repo):

1.  Click on the ![fork](README-img/fork-icon.png) **Fork** icon near
    the upper-right-hand corner. You will be taken to a **Create a new
    fork** screen.
2.  Verify that your GitHub username is selected under **Owner** and
    that the **Repository name** is `activity02-slr` with a green check
    mark (this verifies that you do not already have a GitHub repository
    with this name).
3.  You may provide a **Description** if you would like. This is a way
    to provide some additional, more descriptive, meta information
    related to the things you did. I like to provide a brief description
    of what happened.
4.  Verify that **Copy the `main` branch only** is selected.
5.  Click on the green **Create fork** button at the bottom of this
    page.

You should be taken a copy of this repo that is in your GitHub account.
That is, your page title should be `username/activity02-slr`, where
`username` is replaced with your GitHub username. Directly below this,
you will see the following message:

> forked from
> [gvsu-sta631/activity02-slr](https://github.com/gvsu-sta631/activity02-slr)

You will complete the rest of this activity in **your** forked copy of
the `activity02-slr` repo.

![check-in](README-img/noun-magnifying-glass.png) **Check in**

Take a moment to reflect on what is possibly your second time doing this
forking process.

- What was easier this time?
- What is still muddy?
- What do you need to try/do/explore to help with this muddiness?

## Task 2: One quantitative response variable and one quantitative explanatory variable

The Human Freedom Index is a report that attempts to summarize the idea
of “freedom” through a bunch of different variables for many countries
around the globe. It serves as a rough objective measure for the
relationships between the different types of freedom - whether it is
political, religious, economical or personal freedom - and other social
and economic circumstances. The Human Freedom Index is an annually
co-published report by the Cato Institute, the Fraser Institute, and the
Liberales Institut at the Friedrich Naumann Foundation for Freedom.

Read these directions first, then work through them.

1.  In your `activity02-slr` repo folder/directory, locate and click
    into the `day01-fitting` subfolder.
2.  In the `day01-fitting` subfolder, you will be greeted by a new
    `README.md` file. Do your best to complete the tasks/directions
    provide in this subfolder by **11:59 pm (EST) on Tue, Jan 24**.
3.  In our Teams workspace (linked on Blackboard), find the **Muddy**
    channel and post what was muddiest from these tasks. If someone else
    already posted what you though was muddy, add any clarification to
    their post and give them a “+ 1” 👍. Remember that this space is for
    conversations as well as posting questions. Read through your peers’
    muddy posts and do your best to provide help.

The rest of this `README` document contains tasks/directions for the
second class meeting of this week.

## Task 3: Still in progress

I will have the rest of this activity completed by our next class
session. I will also show you how to update your forked repos from my
original repo 🎆

## Attribution

This document is based on labs from
[OpenIntro](https://www.openintro.org/).

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png"
style="border-width:0" alt="Creative Commons License" /></a><br />This
work is licensed under a
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative
Commons Attribution-ShareAlike 4.0 International License</a>.
