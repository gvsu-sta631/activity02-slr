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
- `day02-assessing` - a folder that contains items for you to complete
  during the second 75-minute class meeting.

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

**Note for Bradford, you need to add the clone to RStudio information
here!**

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

## Task 3: Updating your forked GitHub repo

You will need to start reading these directions back at my
`gvsu-sta631/activity02-slr` GitHub repo **and** have your forked
`username/activity02-slr` GitHub repo handy. I recommend that you have
my repo opened on one half of your screen and your repo opened on the
other half. Read these directions first, then work through them.

1.  At the top of your `username/activity02-slr` repo (above the repo
    contents section), verify that you see a message that looks
    something like:

> This branch is X commits behind gvsu-sta631:main.

2.  Click on the hyperlinked “X commits behind” portion of that message
    to be taken to a **Comparing changes** page.
3.  Verify that your drop-down menu options specify:

- base repository: username/activity02-slr
- base: main
- head repository: gvsu-sta631/activity02-slr
- compare: main

4.  Also verify that you have a message directly below this that says:

> ✓ Able to merge. These branches can be automatically merged.

Flag me if you see something different. 5. Click on the green **Create
pull request** button under this previous message. Note you can look at
the changes that I made, if you so desire, by scrolling down. However,
this is not necessary. 6. On the next page, provide a short descriptive
message in the “Title” box (e.g., “Adding Day 2 materials”). You can
also provide a more detailed message in the “Leave a comment” box if you
choose. 7. Click on the green **Create pull request** button. 8. On the
next screen which is titled the same thing as what you provided in the
“Title” box on the previous screen, you will be presented with a bunch
of information. If you scroll down a little, you should see a green
check mark with a message that specifies:

> This branch has no conflicts with the base branch

And you can click on the green **Merge pull request**. 9. You will be
provided with with an opportunity to provide another meaningful message
(or accept the default message). Finally, click on the green **Confirm
merge** button. You can now work directly from your
`username/activity02-slr` repo.

In summary, what you just did is pulled my changes into your repository.
Git and GitHub refer to this as a “pull request” because you are asking
to pull items into your repo.

## Task 4: Updating your forked GitHub repo

In your `username/activity02-slr` repo, go into the `day02-assessing`
subfolder and follow the tasks listed in the `README`. You will continue
to work in your `activity02-day01.Rmd` file that you started during Day
1 of this activity.

## Attribution

This document is based on labs from
[OpenIntro](https://www.openintro.org/).

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png"
style="border-width:0" alt="Creative Commons License" /></a><br />This
work is licensed under a
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative
Commons Attribution-ShareAlike 4.0 International License</a>.
