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

The most important functions in R call shiny apps that run in your browser. Each of these helps with a different part of the screening process, and will be discussed in the next section. If you'd like to use revtools function in the command line, however, or just want to understand the details underlying these shiny apps, then this section is for you.

## Data import and export
functions: read_bibliography, write_bibliography, format_citation
class: bibliography; print, summary

## Searching for duplicates
functions: fuzzdist & stringdist (external), find_duplicates, extract_unique_references

## Text mining
functions: make_DTM, run_LDA