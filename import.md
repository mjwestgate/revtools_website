---
layout: default
title: Import
---
# Importing data
revtools is designed to import bibliographic data; specifically the kinds of files that you can export from academic databases such as Web of Science or Scopus. Alternatively, most bibliographic management software (such as Zotero, Mendeley or EndNote) can export to a range of formats, including <code>.ris</code>.

## read_bibliography
Bibliographic data can be stored in a range of formats with differing properties (with BibTeX and RIS formats among the most common). In revtools, you can use a single function (<code>read_bibliography</code>) to import your data regardless of what file type that data is stored in. This approach differs from other R packages such as <a href="https://cran.r-project.org/package=RefManageR" target="_blank" rel="noopener">RefManageR</a> or <a href="https://cran.r-project.org/package=bibtex" target="_blank" rel="noopener">bibtex</a> that are really good at importing .bib files, but don't support .ris formats. For example, if you had the same data stored in both .bib and .ris formats, then these two commands would give the same result:

```
data1 <- read_bibliography("my_data.ris")
data2 <- read_bibliography("my_data.bib")
class(data1) # = data.frame
```

If you are working with multiple files, you can import them all by passing their names to <code>read_bibliography</code> as a vector or list:

```
data_all <- read_bibliography(c("my_data.ris", "my_data.bib"))
```

A common extension to this approach is to detect all of the file names in a given subdirectory, and import them all simultaneously:

```
# If the files are in the working directory:
file_names <- list.files()

# Or if they are in a subdirectory:
path <- "./raw_data/"
file_names <- paste0(path, list.files(path = path))

# Then import to a data.frame
data_all <- read_bibliography(file_names)
```

If you have imported your files separately but still want to combine them into a single object, the default method in R is to use <code>rbind</code>:

```
data1 <- read_bibliography("my_data.ris")
data2 <- read_bibliography("my_data.bib")
data_all <- rbind(data1, data2)
```

This approach is unlikely to work with bibliographic data because they often have different numbers of columns, or columns with different names. Instead, you can combine your data using the function <code>merge_columns</code>:
```
data_all <- merge_columns(data1, data2)
```

## Internal data structures
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