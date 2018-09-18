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
Duplicate identification and removal is a large field in itself, but the method applied in <code>revtools</code> is intentionally simple. Basically, you can use the function <code>find_duplicates</code> to look for repeated information within a column of data within a <code>data.frame</code>. In practice, however, several factors influence how accurate the result will be, and how long it takes to calculate.

## Methodological approach
In practical terms, <code>find_duplicates</code> uses a <code>while</code> loop to search for potential duplicates.

A <code>while</code> loop, while faster than matching every pair of can be slow

## String distances
[in development]
functions: fuzzdist & stringdist (external), find_duplicates, extract_unique_references, merge_columns

arguments: thresold, to_lower, remove_punctuation

## Automated duplicate extraction
Once you have searched for potential duplicates, you can use <code>extract_unique_references</code> to automatically extract one reference from every 'group' of matched documents. This function simply picks the document with the most text from each group.

## Manual duplicate extraction
Intro to screen_duplicates
