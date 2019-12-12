---
layout: default
title: Introduction
---
# Introduction

## What is evidence synthesis?
Evidence synthesis is the process of searching, collating and interpreting scientific information. Of course, this definition covers a whole range of possible  activities, from simple literature searches on a single topic or question, right through to a full systematic review or meta-analysis. Whatever their goal, however, many researchers are finding it increasingly difficult to keep track of the amount of literature that they must read to gain an overview of a given research field. This is where revtools can help.

In practical terms, revtools provides some simple functions for importing and managing 'bibliographic' data; i.e. lists of books or articles, when they were published, and who they were authored and published by. Rather than just import these data, however, revtools also includes a number of user interfaces to help you interactively sort and categorize that content. These functions run in your browser, and support a range of tasks from manually sorting article titles or abstracts, right through to automated cluster identification using topic models. By default, each interface hides identifying information of each article, meaning that revtools is consistent with the screening guidelines for systematic reviews given by <a href="https://www.cochrane.org" target="_blank" rel="noopener">Cochrane</a>, the <a href="https://campbellcollaboration.org" target="_blank" rel="noopener">Campbell Collaboration</a>, or the <a href="http://www.environmentalevidence.org" target="_blank" rel="noopener">Collaboration for Environmental Evidence</a>.

This site gives you some basic information on how to import, de-duplicate, and screen articles using revtools.

## What is R?
R is a programming language that is widely used for statistical analysis, particularly in academia. If you want to use revtools, you first need to install R, then use R to download and install 'packages' that provide extra functionality, of which revtools is one.

You can download R from a couple of different places. Perhaps the easiest option is to use <a href="https://www.rstudio.com" target="_blank" rel="noopener">RStudio</a>, which gives a very stable, familiar-looking statistical interface to the R language. If you'd prefer something simpler, you can get the 'default' version from the <a href="https://cran.r-project.org" target="_blank" rel="noopener">Comprehensive R Archive Network</a>. CRAN are the people who actually build and maintain R, but their user interface is fairly basic, which can be off-putting for some users. Regardless of which 'type' of R you prefer, it's straightforward to download and install it from either of these sites.


## Getting started
Assuming that your installation has worked and you can open R, now you can install revtools. revtools is built to perform some useful tasks with as few functions as possible, so you should be able to use it even if you have no coding experience. However, there are a few steps that you will need to take to get it to work.

Once you've loaded R, you're faced with the command window. Paste in the following code:

```
install.packages("revtools")
library(revtools)
```

That's it! If everything goes well, this should install revtools, as well as all the other software packages needed to get revtools to work. If it doesn't work for some reason, or you want to use the 'development' version, you can try downloading it from GitHub instead:

```
install.packages("remotes")
remotes::install_github("mjwestgate/revtools")
library(revtools)
```

At this point you should be ready to go.