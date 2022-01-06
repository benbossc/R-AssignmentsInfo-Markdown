# R-Markdown

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

# Acknowledgements
These instructions were based off of Dr. Noli Brazil's <a href="https://crd150.github.io/hw_guidelines.html#R_Markdown"> Assignment Guidelines for "CRD 150 - Quantitative Methods in Community Research." </a>

# Introduction/Summary

During the first half of the semester, a handful of classes will be devoted to increasing your comfort level and proficiency with using R/Rstudio. Assignments will be released during or after a “Lab/Exploration Day” (see <a href="https://docs.google.com/document/d/1KawpnImzubKawB5cPN-WXyKWmwjfK24sLVd_mTmG4mw/edit?usp=sharing"> syllabus </a> for reference). These assignments will be handed in:

1. an R Markdown format (.Rmd)
2. a knitted .html file

Markdown files should be submitted via Canvas by class time (1:59 PM) based on respective due dates (see <a href="https://docs.google.com/document/d/1KawpnImzubKawB5cPN-WXyKWmwjfK24sLVd_mTmG4mw/edit?usp=sharing"> syllabus </a> for reference).

You will use <a href="https://rmarkdown.rstudio.com/"> R Markdown </a> to write up all R related assignments. This guide will go through the steps for answering and submitting class assignment questions using R Markdown.

# R Markdown

R Markdown is a simple formatting syntax for authoring html, pdf, and Microsoft Word documents in RStudio. 

These documents will provide us an easy-to-read document to grade; more importantly, you will get to practice (1) writing scripts, (2) keeping track of the analyses you run, and (3) organizing your output in a reader-friendly manner. When you submit these documents on Canvas, <strong> do not combine them into a zipped compressed folder </strong>. They should be two separate files.

To be clear, R is a <i>programming language</i>. RStudio is an <i>application</i>. R Markdown is a <i>markup syntax</i> to convert R script and text into a pdf or html document. It allows for presentation-ready documents that show commands and results in a seamless flow. When you write R code and embed it in presentation documents created using R Markdown, you are forced to explicitly state the steps you took to do your research.

In RStudio, install the packages <strong>knitr</strong> and <strong>rmarkdown</strong> using the ```install.packages()``` command. Type the following in your RConsole window after ```>```

```R
install.packages("knitr")
install.packages("rmarkdown")
```

Once you’ve installed these packages, you don’t need to install them any more in the future. You also do not need to load them in at any time using ```library()```.

# Opening an R Markdown File

An ```.Rmd``` template will be provided for each assignment. Download the week’s assignment template, which will be linked at the top of every assignment, and save it into an appropriate folder on your hard drive. File management is important here. Here are some tips.

1. Set up a clear and understandable hierarchical file system for this class on your hard drive. For example, create a class folder (MDSC 30100). Within this class folder, create the folder Assignments. Within the Assignments folder, create separate folders for each Assignment (e.g. Assignment 1, Assignment 2, …). Save that week’s assignment template here. When you knit your Rmd (we’ll get to what knitting means below), this is where your html file will go. Don’t work from your Desktop. Or from the Downloads folder. Or some randomly named folder that you will have a hard time finding a month, week or day from now.
2. To open an .Rmd file in RStudio, select File -> Open File and navigate to the folder you saved the assignment template in and select the file. You should see the R Markdown file pop up on the top left portion of your RStudio interface like below.

<img src = "fig/R-Markdown-fig1.png">

# Authoring an R Markdown document

R Markdown documents contain 3 major components:

1. A YAML header surrounded by - - -
2. Chunks of R code surrounded by ```
3. Text mixed with simple text formatting using the <a href="https://www.markdownguide.org/cheat-sheet/"> Markdown syntax</a>.

## YAML header
The YAML header controls how R Markdown renders your ```.Rmd``` file. A YAML header is a section of key:value pairs surrounded by - - - marks.

In the assignment template’s YAML, change your name, assignment number, lab number, and the date. Other than those items, <strong>the YAML format for each assignment is set for you in the template, so don’t change it</strong>. It will generally look like the following.

```{r}
---
title: "R Assignment #[insert number here]"
subtitle: MDSC 30100
author: Your full name here
date: Assignment due date
output: 
  html_document:
    theme: cosmo
---
```

# R Code chunks
When answering an assignment question, you’ll have the following sequence of components in your R Markdown document: Question, R code answering the question, and your text to explain the results. Let’s say you have the following question in one of your assignments.

```{r}
Q1

1+1

What does the above code do?
```

Assignments will ask you to write R code to accomplish a data analysis task. You present and execute your R code inside R code chunks. R chunks start with ````  ```{r} ````  and end with ```` ``` ```` , and you insert your R code in between. To designate ```1+1``` as R code, it will look like the following in your R Markdown document.

````{r}
```{r}
1+1
```
```` 

All code inside a chunk will be executed when knitting the markdown file (i.e. the html file will show your code and its result). This means that your R code must reside inside an R code chunk in order for it to be processed as R code (otherwise R Markdown will think it is text). This also means that nothing but executable code (or comments, which we’ll get to next) should be inside a chunk.

We will ask you to annotate your R code so that we (and you) know what is being done in that line of code. You designate annotations or comments in R code using the ```#``` symbol. So, to annotate the above line of code 1+1, you add in your R code chunk

````{r}
```{r}
#this adds one plus one
1+1
```
```` 

You put your comments after the ```#```.

The first line of the chunk has ```{r}``` which basically states that everything inside the chunk will be in R code. Next to the ```r```, we can give the chunk a name, such as

````{r}
```{r q1chunk1}
#this adds one plus one
1+1
```
```` 

Here, I named the chunk ```q1chunk1``` which indicates this is question 1, chunk 1. You can name the chunk whatever you like (bulbasaur, ivysaur, venusaur). The chunk name is not required; however, it is good practice to give each chunk a unique name (we’ll see its value later when we talk about knitting).

````{r}
```{r}
knitr::opts_chunk$set(warning=FALSE, message = FALSE)
```
```` 

Do not delete or alter this chunk, always keep it in your R Markdown. The above code establishes global options for every R chunk code in your R Markdown file. These options alter the way R results are spit out in your formatted knitted document. The above code hides non error messages for every single R code chunk in your file. These non error messages are unnecessary for the purposes of this class. Other chunk options can be found here.

You can also set options for individual chunks. These are local options - local to that chunk - and won’t be applied to other chunks in your file. For example, you can add the options ```warning=TRUE``` and ```message=TRUE``` to an individual R code chunk as follows to show the messages for the R code in that chunk. Notice that each argument is separated by a comma.
