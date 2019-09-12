---
title: "Activity 2.3"
output: 
  html_document: 
    keep_md: yes
---









# Exploratory Data Analysis: Tidy Data

Requirements:

- GitHub account
- RStudio Cloud account

Goals:

- Explain differences between tidy and untidy data
- Be able to tidy data so it is more useful for data analysis
- Be able to untidy data for making human readable figures and tables

**Pick a lead**:
This person is not solely responsible for doing the activity, but they are responsible for organizing the collective team effort - for example, making sure all parts are completed and pushing them to the Team GitHub repo.

## Introduction

This activity continuing our use of `dplyr` for wrangling data sets.
This activity is based on Jenny Bryan's [Lord of the Rings tidying data tutorial](https://github.com/jennybc/lotr-tidy).

Recall that tidy data has three key features:

1. Each observation is its own row
2. Each variable is its own column
3. Each value has its own cell

Before we get to making visualizations, it is important to understand whether your data is tidy or not.
Below are three tables (one per movie) summarising the total number of words spoken, by characters of different races and genders.


<table border = 1>
<tr>
<td>
<!-- html table generated in R 3.6.0 by xtable 1.8-4 package -->
<!-- Thu Sep 12 08:13:54 2019 -->
<table border=1>
<caption align="top"> The Fellowship Of The Ring </caption>
<tr> <th> Race </th> <th> Female </th> <th> Male </th>  </tr>
  <tr> <td> Elf </td> <td align="right"> 1229 </td> <td align="right"> 971 </td> </tr>
  <tr> <td> Hobbit </td> <td align="right"> 14 </td> <td align="right"> 3644 </td> </tr>
  <tr> <td> Man </td> <td align="right"> 0 </td> <td align="right"> 1995 </td> </tr>
   </table>
</td>
<td>
<!-- html table generated in R 3.6.0 by xtable 1.8-4 package -->
<!-- Thu Sep 12 08:13:54 2019 -->
<table border=1>
<caption align="top"> The Two Towers </caption>
<tr> <th> Race </th> <th> Female </th> <th> Male </th>  </tr>
  <tr> <td> Elf </td> <td align="right"> 331 </td> <td align="right"> 513 </td> </tr>
  <tr> <td> Hobbit </td> <td align="right"> 0 </td> <td align="right"> 2463 </td> </tr>
  <tr> <td> Man </td> <td align="right"> 401 </td> <td align="right"> 3589 </td> </tr>
   </table>
</td>
<td>
<!-- html table generated in R 3.6.0 by xtable 1.8-4 package -->
<!-- Thu Sep 12 08:13:54 2019 -->
<table border=1>
<caption align="top"> The Return Of The King </caption>
<tr> <th> Race </th> <th> Female </th> <th> Male </th>  </tr>
  <tr> <td> Elf </td> <td align="right"> 183 </td> <td align="right"> 510 </td> </tr>
  <tr> <td> Hobbit </td> <td align="right"> 2 </td> <td align="right"> 2673 </td> </tr>
  <tr> <td> Man </td> <td align="right"> 268 </td> <td align="right"> 2459 </td> </tr>
   </table>
</td>
</tr>
</table>

These tables could have easily been provided to you in an Excel workbook (perhaps with additional color "formating").
These tables are easy for human consumption - we can easily look up the number of words spoken by female humans in *The Return Of The King* - but we will see that this makes things difficult for a computer to find information to perform calculations or create visualizations.

**Thought Question 1**:
Using the tables above, what is the total number of words spocken by male hobbits?
Does a certain `Race` dominate a movie?
Does the dominant `Race` differ accross movies?

Suppose that you were provided with additional information from many more movies or I updated the data to include each `Race`.
Does your approach easily scale to these

## Getting started

Now that your Teams are set-up in GitHub Classroom, these instructions will be how we access Team Activities from now on.
For now, we are still relying on only one Team Member (the lead) pushing the complete activity, but the others are expected to contribute to the discussion and help the lead member complete the step, but not *push* the files from their computer (they should be able to pull, though).

1. *All* Team Members:
  - Go to the Documents section on [Bb](https://mybb.gvsu.edu)
  - Click on the link titled `activity0203`
  - Click on the "Join" button next to your corresponding team name in the **Join an existing team** section
2. *All* Team Members now will:
  - In your team repo, click the green **Clone or download** button, select "Use HTTPS" if this isn't the default option, and click on the clipboard icon to copy the repo URL
  - Go to RStudio Cloud and into the course workspace.  Create a **New Project from Git Repo** - remember that you need to click on the down arrow next to the **New Project** button to see this option.
  - Paste the URL of your activity repo into the dialogue box.
  - Click "OK".
3. *All* Team Members now will Load Package:
  - In this lab, we will work with the `tidyverse` package so we need to install and load it.
    Type the following code into your *Console*:
  
    
    ```r
    install.packages("tidyverse")
    #> Error in contrib.url(repos, "source"): trying to use CRAN without setting a mirror
    library(tidyverse)
    ```
    
  - Note that this package is also loaded in your R Markdown document.
4. *All* Team Members now will configure Git:
  - Go to the *Terminal* pane and type the following two lines of code, replacing the information inside the quotation marks with your GitHub account information:
  
    
    ```bash
    git config --global user.email "your email"
    git config --global user.name "your name"
    ```
    
  - Confirm that these changes have been implemented, run the following code:
  
    
    ```bash
    git config --global user.email
    git config --global user.name
    ```
        
  - Inform git that you want to store your GitHub credentials for $60 \times 60 \times 24 \times 7 = 604,800$ seconds, run the next line of code.  This needs to be done on a per-project basis.
  
    
    ```bash
    git config --global credential.helper 'cache --timeout 604800'
    ```
    
5. *All* Team Members will now name their RStudio project:
  - Currently your RStudio project is called *Untitled Project*.  Update the name of your project to be "Activity 2-3 - Tidy Data"
6. The *Lead* Team Member to do the following in RStudio:
  - Open the `.Rmd` file and update the **YAML** by changing the author name to your **Team** name and date to today, then knit the document.
  - Go to the *Git* pane and click on **Diff** to confirm that you are happy with the changes.
  - *Stage* just your Rmd file, add a commit message like "Updated team name" in the *Commit Message* dialogue box and click **Commit**
  - Click on **Push**.  This will prompt a dialogue where you first need to enter your GitHub user name, and then your password - this should be the only time you need to do this for the current activity.
  - Verify that your changes have been made to your GitHub repo.
7. *All other* Team Members now will do the following in RStudio:
  - Go to the *Git* pane and click on **Pull** button.  This will prompt a dialogue where you first need to enter your GitHub user name, and then your password (this should be the only time you need to do this for the current activity).
  - Observe that the changes are now reflected in their project!

Again, only one team member will be pushing the changes.
All others are encouraged to work and save changes "locally" in RStudio.Cloud, but not push.

## The data

The three tables from the Introduction are stored as three plain text, comma delimited files (one for each film) in the `data` project folder.


```r
fship <- read_csv("data/The_Fellowship_Of_The_Ring.csv")
ttow <- read_csv("data/The_Two_Towers.csv")
rking <- read_csv("data/The_Return_Of_The_King.csv")
```

**Thought Question 2**:
Each data set was brought in one at a time in your R Markdown document in the `load-data` chunk.
Use two methods to verify (i.e., in your *Console* and *Environment* panes) that they are loaded in your session.


```r
lotr_untidy <- bind_rows(fship, ttow, rking)
str(lotr_untidy)
lotr_untidy
```

**Thought Question 2**:
The `collect-data` chunk does a common data preparation task.
Describe (step-by-step) what these three lines of code do.
Remember that you can run specific portions of the code to see what the different parts do.

The `binds_rows` function is a relatively simple function for collecting data and this is possible here because the pieces are similar.
In other scenarios (as we will see after `ggplot2`) we may need to do some additional work before we can fit the pieces together.

***
**Exercise 1**:
Describe why `lort_untidy` is untidy data.

***

## Tidy the untidy data


```r
lotr_tidy <- lotr_untidy %>% 
  gather(key = 'Gender', value = 'Words', Female, Male)
lotr_tidy
```

The `gather` function is part of the `tidyr` package.
This may seem counter intuitive, but we will read the function from right to left.

We take the variables `Male` and `Female` and gathered their values into a single new variable `Words`.
By doing this, a companion variable `Gender` was forced to be created (a *key*) which tells whehter the value of `Words` came from `Male` or `Female`.
All other variables (i.e., `Film` and `Race`) remain unchanged and are replicated as needed.

See the help documentation for `gather` to see more examples and information for additional arguments.

### Write the tidy data to file

Now that we have this combined, tidy data set, we should write it to file so that we can use it in additional projects for analysis and visualizations.
This is a great way to share data files that are tool-agnostic and ready to analyze.

To do this, run the following code:


```r
write_csv(lotr_tidy, path = "data/lotr_tidy.csv")
```

Inspect that this file was created by looking in your `data` project folder.

***
**Exercise 2**:
While exploring your `data` project folder, you should have also seen two additional data files: `Female.csv` and `Male.csv`.
Write the code that reads them in and writes a single tidy data frame to file.
This is the same information we worked with, just pivoted a different way, so you can overwrite the `lotr_tidy` tibble and `lotr_tidy.csv` data file from before.

***

***
**Exercise 3:**
Write code that computes the total number of words spoken by by each race across the entire LotR trilogy.
Try this two ways:

1. Using film- or gender-specific, untidy data frames as the input data.
2. Using the `lotr_tidy` data frame as input.

Reflect on the process of writing this code and on the code itself.
Which is easier to write?
Which is easier to read?

***

***
**Exercise 4:**
Write R code to compute the total number of words spoken in each film.
Do this by copying and modifying your own code for totalling words by race.
Which approach is easier to modify and repurpose – the one based on multiple, untidy data frames or the tidy data?

***

### Tidy take away

If your data is distributed across a number of different files or data frames, you have untidy data.
So far we have seen that we can use `bind_rows` from the `dplyr` package to combine data frames with similar columns into one large data frame.

If you have a conceputal variable spread across multiple variables (e.g., word counts for males and word counts females), you have untidy data.
We used the `gather` function from the `tidyr` package to stack up all of the conceptual variables into a single variable and, in the process, create a new variable to convey which grouping variable it came from.
This also did all needed replication for the other variables.

## Preparing figures or tables

We just saw how to tidy data to use in analyses or visualizations.
Now we see how to untidy data using the `spread` function from `tidyr`.
You may be wondering, "But you just said untidy data is bad..."
However, like the tables that we started off with, untidy data is useful at the end of an analysis to create figures or tables.

### One variable per `Race`


```r
lotr_tidy %>% 
  spread(key = Race, value = Words)
```

The `spread` function is also part of the `tidyr` package.
We take the values of `Words` and want to spread these across the different `Race` values.
Therefore, each `Race` will be a new column with the corresponding value of `Words` as the cell.
All other variables (i.e., `Film` and `Gender`) remain unchanged and any missing values are automatically filled as missing values (`NA`) by default.

See the help documentation for `spread` to see more examples and information for additional arguments.

***
**Exercise 5:**
Write code that computes the total number of words spoken by by each `Gender` and LotR film in the trilogy.
Try this two ways:

1. Using functions from `dplyr`.
2. Using the `spread` data frame as input.

Reflect on the process of writing this code and on the code itself.
Which is easier to write?
Which is easier to read?

***

***
**Exercise 6:**
Let's get one variable per combo of `Race` and `Gender`.
Use the `unite` function  to combine these two variables into a new variable.
Then, `spread` the total number of words across this new variable.

Remember that you can use `?unite` to find out more information.

***

***
**Exercise 7:**
Use the `group_split` function to recreate the three original tables - total number of words spoken by each `Race` and `Gender`, for each movie.

Remember that you can use `?group_split` to find out more information.

***

Have your **Lead Team Member** commit and push the final activity to your Team's repo.
