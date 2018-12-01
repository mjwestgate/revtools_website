---
layout: user_manual
title: removing duplicates
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

# Removing duplicates
Duplicate identification and removal is a large field in itself, but the method applied in <code>revtools</code> is intentionally simple. Basically, you can use the function <code>find_duplicates</code> to look for repeated information within a column of data within a <code>data.frame</code>. The easiest way to get a feel for how these functions work is to investigate them with <code>screen_duplicates</code>, which aunches a Shiny app; but you can run the underlying string matching algorithms from the command line if you prefer.

You can launch <code>screen_duplicates</code> in one of three different ways. First, if you want to import data within the app, then you just run the function by itself:
```
screen_duplicates()
```

Second, you can launch the app using data from the workspace:
```
data <- read_bibliography("my_data.ris")
screen_duplicates(data)
```

Finally, if you want to save results from the app back to the workspace, then you need to specify an object where that data can be returned:
```
data <- read_bibliography("my_data.ris")
result <- screen_duplicates(data)
```

## Specifying variables
The 'Data' tab contains four menus:

<img src="/assets/screenshots/screen_duplicates_data_tab.png" width="200"/>

<b>Import:</b> If you haven't passed any data to <code>screen_duplicates</code>, then this allows you to drag-and-drop a dataset directly in to the app.

<b>Is there a variable describing duplicates in this dataset?:</b> If you have identified calculated duplicates in your dataset - either manually, or using <code>find_duplicates</code> - then you can use this to specify where those data are located in your <code>data.frame</code>.

<b>Select column to search for duplicates:</b> This specifies which data should be searched for matches. Most often this will be the article title, but you might want to search for matches in DOIs, or even journal titles.

<b>Select grouping Variable(s):</b> If no variables are specified, then the matching function (<code>find_duplicates</code>) will search every value against every other value in a <code>while</code> loop. This is computationally expensive for large datasets, so this menu allows you to limit the search for matches. The default is to search for titles, but only within the entries with the same journal and year.

## String distances
This section has 5 options:

<img src="/assets/screenshots/screen_duplicates_matching_tab.png" width="200"/>

<b>Select function</b> has three options:
- fuzzdist
- stringdist
- exact

<b>Select method</b> allows you to select a matching algorithm for the specified function.

<b>Select maximum distance</b> sets the threshold for matching pairs of strings.

<b>Make lower case</b> and <b>remove punctuation</b> do just that.


## Alternatives
If you'd rather not screen each duplicate manually, you can run all of the specified functions in the command line.
```
data <- read_bibliography("my_data.ris")

matches <- find_duplicates(
  data = titles,
  match_variable = "x",
  group_variable = NULL,
  match_function = "fuzzdist",
  method = "fuzz_partial_ratio",
  threshold = 0
)
```
Once you have searched for potential duplicates, you can use <code>extract_unique_references</code> to automatically extract one reference from every 'group' of matched documents. This function simply picks the document with the most text from each group.
```
data_unique <- extract_unique_references(data, matches)
```

<a href="/user_manual/3_working_with_data.html">Previous: Working with data</a> | <a href="/user_manual/5_manual_screening.html">Next: Manual screening</a>