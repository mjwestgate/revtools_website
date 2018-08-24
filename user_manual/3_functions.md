---
layout: user_manual
title: Command-line Functions
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

# Functions
The most important functions in <code>revtools</code> call shiny apps that run in your browser. Each of these helps with a different part of the screening process, and will be discussed in the next section. If you'd like to use <code>revtools</code> function in the command line, however, or just want to understand the details underlying these shiny apps, then this section is for you.

## Data import and export
Bibliographic data can be stored in a range of formats with differing properties (with BibTeX and RIS formats among the most common). In <code>revtools</code>, you can use a single function (<code>read_bibliography</code>) to import your data regardless of what file type that data is stored in. For example, if you had the same data stored in both .bib and .ris formats, then these two commands would give the same result:

```
data <- read_bibliography("my_data.ris")
data <- read_bibliography("my_data.bib")
```

 This approach differs from other R packages such as <a href="https://cran.r-project.org/package=RefManageR" target="_blank" rel="noopener">RefManageR</a> or <a href="https://cran.r-project.org/package=bibtex" target="_blank" rel="noopener">bibtex</a> that are really good at importing .bib files, but don't support .ris formats.

Once your data have been imported, they are stored in a list-based format of class <code>bibliography</code>. Each <code>bibliography</code> entry is another list containing all the information provided on a given reference. You can use the S3 methods <code>print</code> or <code>summary</code> to give an overview of the content of a bibliography object. Calling <code>print</code> will show the formatted reference for the first n entries (default n = 5), meaning that it is basically a wrapper function to <code>revtools::format_citation</code>. In contrast, calling <code>summary</code> gives more detailed information on the number of articles in the <code>bibliography</code> object, the proportion that contain abstracts, and the most common sources (i.e. journal titles) in that datasets.

Finally, you can easily convert your <code>bibliography</code> object into a <code>data.frame</code> by calling <code>as.data.frame</code>, or re-export to other bibliographic software using <code>write_bibliography</code>.

## Searching for duplicates
functions: fuzzdist & stringdist (external), find_duplicates, extract_unique_references, merge_columns

## Text mining
functions: make_DTM, run_LDA