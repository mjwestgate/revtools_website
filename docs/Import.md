---
layout: default
title: Import
---
# Getting Started
revtools is built to perform some useful tasks with as few functions as possible, so you should be able to use it even if you have no coding experience. However, there are a few steps that you will need to take to get it to work.

## Downloading and Installing R
revtools is a package that runs in the R environment; it can't be used by itself. Consequently, the first thing you'll need to do is download and install R.

Before we do that, a quick note on terminology: R is both a program that you can download, and a language that you use to get that program to run. This can be a little confusing for new users, but just stick with me!

You can download R from a couple of different places. Perhaps the easiest option is to use <a href="https://www.rstudio.com" target="_blank" rel="noopener">RStudio</a>, which gives a very stable, familiar-looking statistical interface to the R language. If you'd prefer something simpler, you can get the 'default' version from the <a href="https://cran.r-project.org" target="_blank" rel="noopener">Comprehensive R Archive Network</a>. CRAN are the people who actually build and maintain R, but their user interface is fairly basic, which can be off-putting for some users.

Regardless of which 'type' of R you prefer, it's straightforward to download and install it from either of these sites.

## Installing revtools
Assuming that your installation has worked and you can open R, now you can install revtools. Once you've loaded R, you're faced with the command window. Paste in the following code:

```
install.packages("revtools")
library(revtools)
```

That's it! If everything goes well, this should install revtools, as well as all the other software packages needed to get revtools to work. If it doesn't work for some reason, or you want to use the 'development' version, you can try downloading it from GitHub instead:

```
install.packages("devtools")
install_github("mjwestgate/revtools")
library(revtools)
```

At this point you should be ready to go.

## Getting data
revtools is designed to import bibliographic data; specifically the kinds of files that you can export from academic databases such as Web of Science or Scopus. Alternatively, most bibliographic management software (such as Zotero, Mendeley or EndNote) can export to a range of formats, including <code>.ris</code>.

## read_bibliography
Bibliographic data can be stored in a range of formats with differing properties (with BibTeX and RIS formats among the most common). In revtools, you can use a single function (<code>read_bibliography</code>) to import your data regardless of what file type that data is stored in. This approach differs from other R packages such as <a href="https://cran.r-project.org/package=RefManageR" target="_blank" rel="noopener">RefManageR</a> or <a href="https://cran.r-project.org/package=bibtex" target="_blank" rel="noopener">bibtex</a> that are really good at importing .bib files, but don't support .ris formats. For example, if you had the same data stored in both .bib and .ris formats, then these two commands would give the same result:

```
data1 <- read_bibliography("my_data.ris")
data2 <- read_bibliography("my_data.bib")

class(data1) # = data.frame
```

If you are working with multiple files, you can import them all by detecting the file names and passing them all to <code>read_bibliography</code>:

```
# If the files are in the working directory:
file_names <- list.files()

# Or if they are in a subdirectory:
path <- "./raw_data/"
file_names <- paste0(path, list.files(path = path))

# Then import to a list
data_list <- lapply(
  file_names,
  function(x){read_bibliography(x)}
)
```

## Merging two data.frames
If your two (or more) datasets are from the same source then it is possible that they will contain all of the same types of information, and be imported to R with identical numbers of columns, and the same column names. If that is the case, you can combine them using the base R command <code>rbind</code>.
```
data_all <- rbind(data1, data2)
```

In many cases, however, your files will contain different kinds of data, an using different headings. To merge these using revtools, you can use the function <code>merge_columns</code>:
```
data_all <- merge_columns(data1, data2)
```

# Internal data structures
By default, <code>read_bibliography</code> returns a <code>data.frame</code>. However, it does this via an intermediate step of generating a list-based format called class <code>bibliography</code>. Most users probably won't use this format very often (if at all), but as it makes up a lot of the architecture of revtools, it might be worth checking. If you find an error in your <code>data.frame</code>s, then knowing about this class might be useful for locating the error.

Each <code>bibliography</code> entry is a list containing all the information provided on a given reference. Further, the tags are converted to a standardised format; so regardless of the format your data are stored in, you get meaningful headings.

```
data1 <- read_bibliography("my_data.ris", return_df = FALSE)

 > class(data)
 "bibliography"

 > class(data[[1]])
 "list"

 > names(data[[1]])
 [1] "type"   "author"    "year"    "title"   "journal"
```

If you import from multiple files, you can merge (or 'append') them using <code>c</code>, for example:
```
x <- read_bibliography("file1.ris")
y <- read_bibliography("file2.bib")
z <- c(x, y)
```
This can be useful if you are collating data from multiple sources. You can also re-export from class <code>bibliography</code> to other bibliographic software using <code>write_bibliography</code>.

You can use the S3 methods <code>print</code> or <code>summary</code> to give an overview of the content of a bibliography object. Calling <code>print</code> will show the formatted reference for the first n entries (default n = 5), meaning that it is basically a wrapper function to <code>revtools::format_citation</code>. In contrast, calling <code>summary</code> gives more detailed information on the number of articles in the <code>bibliography</code> object, the proportion that contain abstracts, and the most common sources (i.e. journal titles) in that dataset. Finally, you can easily convert your <code>bibliography</code> object into a <code>data.frame</code> by calling <code>as.data.frame</code>.