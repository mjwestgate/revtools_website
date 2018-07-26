<h1>New to R?</h1>
Interested in <code>revtools</code> but haven't used R before? This is for you!

<code>revtools</code> is built to perform some useful tasks with as few functions as possible, so you should be able to use it even if you have no coding experience. I've tried to lay out some logical steps below, but please drop me an email (or write in the comments) if there is anything missing or unclear.

<h2>1. Installing R</h2>
<code>revtools</code> is a package that runs in the <code>R</code> environment; it can't be used by itself. Consequently, the first thing you'll need to do is download and install <code>R</code>.

Before we do that, a quick note on terminology: <code>R</code> is both a program that you can download, and a language that you use to get that program to run. This can be a little confusing for new users, but just stick with me!

You can download <code>R</code> from a couple of different places. Perhaps the easiest option is to use <a href="https://www.rstudio.com" target="_blank" rel="noopener">RStudio</a>, which gives a very stable, familiar-looking statistical interface to the <code>R</code> language. If you'd prefer something simpler, you can get the 'default' version from the <a href="https://cran.r-project.org" target="_blank" rel="noopener">Comprehensive R Archive Network</a>. CRAN are the people who actually build and maintain <code>R</code>, but their user interface is a bit more basic, which can be off-putting for some users.

Regardless of which 'type' of <code>R</code> you prefer, it's straightforward to download and install it from either of these sites.

<h2>2. Installing revtools</h2>
Assuming that your installation has worked and you can open <code>R</code>, now you can install <code>revtools</code>. Once you've loaded R, you're faced with the command window. Paste in the following code:

<code>install.packages("revtools")<br>
library(revtools)</code>

That's it! If everything goes well, this should install <code>revtools</code>, as well as all the other software packages needed to get <code>revtools</code> to work. If it doesn't work for some reason, or you want to use the 'development' version, you can try downloading it from GitHub instead:

<code>install.packages("devtools")<br>
install_github("mjwestgate/revtools")<br>
library(revtools)</code>

At this point you should be ready to go.

<h2>3. Importing your data</h2>
<code>revtools</code> is designed to import bibliographic data; specifically the kinds of files that you can export from academic databases such as Web of Science or Scopus. These are typically some type of .ris or .bib format; but different websites tend to have very different styles. Consequently, revtools ignores the suffix and tries to autodetect the sort of file that you have given it.

To import your file, first ensure that it is located in your "working directory". This is the location that R searches for new data, and also where it will save any outputs. In the version of <code>R</code> that I have, the dropdown menu item we're looking for (called 'Change Working Directory') is rather unhelpfully listed under 'Misc', but it might be somewhere else in RStudio.

<b>3. Exploring your data</b>
Once you have set your working directory, and placed the file you'd like to view in that directory, you're ready to use <code>revtools</code>. Copy and paste the following code into your browser (it may take some time to run, especially for large files), being careful to change 'my_file.ris' to the name of your actual dataset:

<code>my_data<-read_bibliography("my_file.ris")<br>
screen_visual(my_data)</code>

The first line of this is fairly straightforward; it imports your dataset and converts it into a standard format. However, the second function (<code>screen_visual</code>) does several things behind the scenes:
<ol>
	<li>converts the data into a spreadsheet style (known as a <code>data.frame</code> in <code>R</code>)</li>
	<li>extracts any titles, keywords and abstracts from each reference in the bibliography</li>
	<li>uses that information to create a 'document term matrix' (DTM), which lists which terms are found in each reference</li>
	<li>uses the DTM as the input to a topic model</li>
	<li>opens a browser window and plot the resulting cloud of references</li>
</ol>
After that, what you do with it is up to you! It is important to remember, however, that <code>revtools</code> will not automatically save your progress, so remember to use the 'save' option in the bottom of the left-hand sidebar. Saving to .csv format is most useful for investigating your data manually, but the other option (.rda) is more useful if you want to revisit the same browser window at a later time. Either way, the file you save should appear in your working directory.

That's all for now - more information will be available in other tutorials soon!