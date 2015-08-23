---
title       : Word prediction app
subtitle    : The new prediction algorithm for text input.
author      : James Longman
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

<h2 style="color:#000000;">Word prediction app</h2>

<p style="display:block; margin:10px 0px 10px 0px;">This app is designed to be very simple to use offering the user a clean interface, simple text input box and, as shown below, textual and graphical representations of the next predicted word based upon their entry.</p>

![title](Capture.PNG)

<p style="display:block; margin:10px 0px 10px 0px;">There is also a language selection box to allow alternate prediction languages to be selected.  Using this will result in a small delay whilst the new language data is loaded to support the prediction functions.</p>
--- .class #id bg:#ccccff

<h2 style="color:#000000;">Data cleaning</h2>

<p style="display:block; margin:10px 0px 10px 0px;">With language evolving so quickly you need a new approach to achieve the best prossible predictions. </p> 

<p style="display:block; margin:10px 0px 10px 0px;">This app makes use of custom regular expressions in addition to standard natural language processing functions to try and sanitise the user input taking in to account some variations of emoiticons and "text speak".</p>  


<p style="display:block; margin:10px 0px 10px 0px;">Numbers and profanity (as defined by the <href="https://github.com/shutterstock/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words">Shutterstock list</a>) are replaced by generic tokens so as not to skew the proability calcualtions.  </p>

<p style="display:block; margin:10px 0px 10px 0px;">These tokens will never be presented as predictions to the user.</p>

--- .class #id

<h2 style="color:#000000;">n-Gram construction and probabilities</h2>

<p style="display:block; margin:10px 0px 10px 0px;">This app has data tables of the most popular 1 to 6-grams.</p>

<p style="display:block; margin:10px 0px 10px 0px;">Each of the 2 through 6-gram tables stores the probability of the last (n) word occuring given the preceding (n-1) words.</p>

<p style="display:block; margin:10px 0px 10px 0px;">For the 1-grams diversity of preceding words (as witnessed by the 2-gram table) is used rather than overall frequency of word.</p>

--- .class #id bg:#ccccff 

<h2 style="color:#000000;">Prediction algorithm</h2>

<p style="display:block; margin:10px 0px 10px 0px;">To construct the predictions two things are done:-</p>
1. User input is put through the same cleaning routines that the original data corpus to build the model was.
2. Starting with the highest available n-Gram table, as dictated by the size of the input string post cleaning, the n-Gram tables are cycled through calculating the probability of the next word.

<p style="display:block; margin:10px 0px 10px 0px;">This calculation uses simple back-off techniques</p>

<span style="display:block; font-size=20px;">$$total probability = a + b*0.4^1 + c*0.4^2 + d*0.4^3$$</span>

<p style="display:block; margin:10px 0px 10px 0px;">e.g.</p>
<p style="display:block; margin:10px 0px 10px 0px;">a = probability of x in n grams</p>
<p style="display:block; margin:10px 0px 10px 0px;">b = probability of x in n-1 grams</p>
<p style="display:block; margin:10px 0px 10px 0px;">c = probability of x in n-2 grams</p>
<p style="display:block; margin:10px 0px 10px 0px;">d = probability of x in n-3 grams</p>







