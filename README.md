Activity 02 - Simple Linear Regression (SLR)
================

This activity is intended to be completed in one week - outside of class
preparation work and class meetings. On our Blackboard course site you
were provided with items to read, watch, and do prior to attempting this
activity. Do not proceed in this activity until you have minimally:

1.  (Day 1 portion) Read *ISLR* Chapter 1 & Sections 2.1 - 2.2
2.  (Day 2 portion) Read *ISLR* Sections 3.0 & 3.1.

In this repository/directory, you should see five items:

- `README-img` - a folder containing images that I am embedding within
  this `README.md` file and other files. You do not need to do anything
  with this.
- `.gitignore` - a file that is used to specify what Git can ignore when
  pushing to GitHub. You do not need to do anything with this.
- `README.md` - the document you are currently reading.
- `day01-fitting` - a folder that contains items for you to complete
  during the first class meeting.
- `day02-assessing` - a folder that contains items for you to complete
  during the second class meeting.

We will explore most of these items over this week. Before doing that,
you will first make your own copy of this repository.

### Optional Resources

Do you want an interactive way to check your understanding outside of
class? Though not a perfect fit for our class,
[OpenIntro](https://www.openintro.org/team/) is a team of passionate
stat educators focused on increasing peoples data skills. [Benjamin
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

## Day 1

### Task 1: Forking & cloning

I forgot to include this information at the end of last week’s activity.
I like to sketch/diagram processes to help me make my thoughts physical
(or digital in this case) and it provides me with an opportunity to
check my understanding. Over the last week, we began to practice the
“Bradford STA 631 GitHub + RStudio” workflow - long name and likely
unique to our current class needs. When you are working outside of STA
631, your workflow with GitHub and RStudio will likely be different than
what we do here.

<figure>
<img src="README-img/updated-workflow.svg"
alt="Blackboard icon to fork icon to clone icon to edit icon to commit icon to push icon" />
<figcaption aria-hidden="true">Blackboard icon to fork icon to clone
icon to edit icon to commit icon to push icon</figcaption>
</figure>

Or in words:

1.  I will post a link to an activity repo on Blackboard,
2.  You will make your own copy of (fork) this repo,
3.  You will create an RStudio Project and Clone this repo,
4.  You will edit and work on the activity,
5.  You will commit your changes, and
6.  You will push your changes back to GitHub.

![check-in](README-img/noun-magnifying-glass.png) **Check in**

I encourage you to find a way to visualize or list out processes to help
you determine if anything is missing. These do not need to be perfect
and might include a lot of “it depends” scenarios. You can always
include this (if it is a frequently occurring “it depends”) or make note
of them in some other way.

For your preparation tasks, you were asked to create an outline of your
current understanding of how to approach a simple linear regression
analysis. With your neighbors for the next 5 minutes, talk through your
processes.

As a class we will discuss these items:

- What similarities did you notice?
- Did someone have a consideration/step in their process that you had
  heard of before, but forgot to include in yours?
- What changes, currently, do you plan to make to your process?

#### Forking

Now you will go through our GitHub + RStudio process. Read these
directions first, then work through them as this is likely still new to
you. Ask questions of your neighbors and Bradford as you have them.

In this GitHub repo (i.e., my repo):

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

#### Cloning

You connected RStudio and GitHub for Day 2 of this activity. If you are
experiencing issues, get a hold of me or verify that you successfully
set up RStudio and GitHub to communicate by redoing [this previously
assigned preparation](https://github.com/gvsu-sta518/preparation02).

Read these directions first, then work through them during your second
reading. Note that you will be switching between RStudio and your GitHub
repo (that you previously forked) so it might be helpful to have this
page open on half of your screen and RStudio open on the other half.

1.  In RStudio, click on the
    <img src="README-img/rproj-icon.png" alt="RStudio Project" width = "20"/>
    icon (the icon below the Edit drop-down menu).
2.  Click on **Version Control** on the *New Project Wizard* pop-up.
3.  Click on **Git** and you should be on a “Clone Git Repository” page.
4.  Back to **your** `activity06-logistic-regression` GitHub repo, click
    on the green **Code** button near the top of the page.
5.  Verify that **HTTPS** is underlined in orange/red on the drop-down
    menu, then copy the URL provided.
6.  Back in RStudio, paste the URL in the “Repository URL” text field.
7.  The “Project directory name” text field should have automatically
    populated with `activity02-slr`. If yours did not (this is usually
    an issue on Macs),
    - Click back into the “Repository URL” text field.
    - Highlight any bit of this text (it does not seem to matter what or
      how much).
    - Press Ctrl/Cmd and the “Project directory name” should now have
      automatically populated with `activity02-slr`.
8.  Browse to `STA 631/Activities` (assuming you followed my opinionated
    file structure from earlier in the semester), then click **Choose**.
9.  Click on **Create Project**.

Your screen should refresh and the **Files** pane should say that you
are currently in your `activity02-slr` folder that currently has the
same files and folders as your GitHub repo. If you are asked for your
GitHub credentials, provide your GitHub username and your PAT (not your
password).

![check-in](README-img/noun-magnifying-glass.png) **Check in**

Take a moment to reflect on what is possibly your second time doing this
forking process.

- How is this process going for you? Is it “muscle memory” yet?
- What is easier since last week?
- What do you still need help remembering?

### Task 2: One quantitative response variable and one quantitative explanatory variable

You have data that you found interesting and are bringing it with you
for this activity. This data might be in a format that is not
necessarily ready to be analyzed. Therefore, Day 1 of this activity is
lighter than Day 2 to provide you with time and space to do any needed
data management. Day 1 is essentially doing a process similar to what
you did in [Activity 1, Day
3](https://github.com/gvsu-sta631/activity01-course-tools/tree/main/day03-rstudio-r).
I encourage you to do all data management work in R so that it is
documented (and hopefully commented) and thus, [reproducible and/or
replicable](https://the-turing-way.netlify.app/reproducible-research/overview/overview-definitions.html).

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

## Day 2

In your `username/activity02-slr` repo, go into the `day02-assessing`
subfolder and follow the tasks listed in the `README`. You will continue
to work in your `activity02.Rmd` file that you started during Day 1 of
this activity.
