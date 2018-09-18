---
layout: user_manual
title: data structures
---
<head>
  <!-- Global site tag (gtag.js) - Google Analytics -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=UA-121833450-2"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());

    gtag('config', 'UA-121833450-2');
  </script>
</head>

# Structures for bibliographic data

## Import
Bibliographic data can be stored in a range of formats with differing properties (with BibTeX and RIS formats among the most common). In <code>revtools</code>, you can use a single function (<code>read_bibliography</code>) to import your data regardless of what file type that data is stored in. This approach differs from other R packages such as <a href="https://cran.r-project.org/package=RefManageR" target="_blank" rel="noopener">RefManageR</a> or <a href="https://cran.r-project.org/package=bibtex" target="_blank" rel="noopener">bibtex</a> that are really good at importing .bib files, but don't support .ris formats. For example, if you had the same data stored in both .bib and .ris formats, then these two commands would give the same result:

```
data <- read_bibliography("my_data.ris")
data <- read_bibliography("my_data.bib")
```

## Class bibliography
Once your data have been imported, they are stored in a list-based format of class <code>bibliography</code>. Each <code>bibliography</code> entry is another list containing all the information provided on a given reference. Further, the tags are converted to a standardised format; so regardless of the format your data are stored in, you get meaningful headings.

```
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
This can be useful if you are collating data from multiple sources. You can also re-export from class 'bibliography' to other bibliographic software using <code>write_bibliography</code>.

## Viewing bibliographic data
You can use the S3 methods <code>print</code> or <code>summary</code> to give an overview of the content of a bibliography object. Calling <code>print</code> will show the formatted reference for the first n entries (default n = 5), meaning that it is basically a wrapper function to <code>revtools::format_citation</code>. In contrast, calling <code>summary</code> gives more detailed information on the number of articles in the <code>bibliography</code> object, the proportion that contain abstracts, and the most common sources (i.e. journal titles) in that dataset.

## Converting to data frames
You can easily convert your <code>bibliography</code> object into a <code>data.frame</code> by calling <code>as.data.frame</code>. One problem with this approach is that it makes it difficult to merge different datasets together if they contain different data. So, to continue our earlier example:

```
x <- as.data.frame(read_bibliography("file1.ris")) # works
y <- as.data.frame(read_bibliography("file2.bib")) # works
z <- rbind(x, y) # often fails
```

This approach fails because different data structures rarely contain exactly the same tagged information, and therefore have different column names. You can get around this by using <code>merge_columns</code>, e.g.

```
x <- as.data.frame(read_bibliography("file1.ris"))
y <- as.data.frame(read_bibliography("file2.bib"))
z <- merge_columns(x, y)
```