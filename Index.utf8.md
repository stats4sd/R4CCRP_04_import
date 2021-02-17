---
title: "Importing data"
output: 
  learnr::tutorial:
    progressive: true
    allow_skip: true
    df_print: default
runtime: shiny_prerendered
description: >
  Learn how to import data from RStudio.
---





## Overview

In this workbook, we will learn the process of importing data into R, which consists of

- making sure the data has the right shape
- saving the data in an R-friendly format
- importing the data from RStudio


Here is a video where these steps are briefly explained:

![](https://youtu.be/truh-B_S-v4)



## Shaping the data

First let's talk about data shape. If you want to import data into R - or into any statistical software really - you need your data to have the right shape. It should take the form of one single "rectangle" of data, made of columns and rows that don't vary in size, and where

- Each row represents one observation
- Each column represents one variable

The R community calls it *tidy data*. Here is a nice presentation illustrating this tidy data concept: <a href="https://docs.google.com/presentation/d/1N7hKepabvl9OrHjvGJWPjUsfzVdB5xzV5AsFndgSwms/edit?usp=sharing" target="_blank">Make friends with tidy data </a> 

You also want your column names to be at the very top, in one **single** row, and the rest of your data to start right below this first row, like in this screenshot.

<img src="./images/well_formattedbis.PNG" width="100%" style="display: block; margin: auto auto auto 0;" />

Everything in your rectangle of data should be part of your data. There's no problem with having empty cells, but these have to be empty because the corresponding values are missing. 




### Avoid merging cells
In spreadsheets like Excel, it is tempting to merge cells in order to make things look nicer. The issue is that merged cells don't transfer well to other softwares. So if you want to look at your data from R or any other statistical software, don't merge your cells. Instead, copy the value in all the corresponding cells.
<img src="./images/merge2bis.PNG" width="80%" style="display: block; margin: auto auto auto 0;" />

### Column names good practice
It is best to keep your column names meaningful, yet short, and to avoid spaces, accent and other special characters, except for the dot and the underscore symbols. These probably sound a bit familiar. That's because, the rules for naming columns are basically the same as the rules for naming objects (see workbook of the Intro module). And this is not surprising, because columns are basically objects that lie within dataframes.

As an example, a column called "Température Minimale", could be shortened to "temp.min". 


### Missing values

As said above, having missing data is totally fine. I mean, it may be an issue for your analysis, but it is not an issue for importing data. It is common for people to have a specific code to represent missing values, like -1, 99 or NA. These are all fine. What's important is to choose a code that cannot be a value taken by your non-missing data, and to be consistent. If you code missing values differently for each of your columns, you're asking yourself for trouble. My personal preference is to simply leave the cell empty. An empty cell is easy to spot and R will recognize it automatically as a missing value.


### How to shape your data

Ideally the shape of your data should be thought through right from the start, at the design stage of your study, so that during data collection, your data already has the right shape. Unfortunately, things don't always go as planned, and you may not always have control over the way the data is collected. In such case, you could end up with some data that is not in the shape described above.

There are two ways to deal with that. Either reshaping the data in a software like Excel, or doing so in R directly. The former is probably simpler at first, but at some point, when you are more experience with R, you should consider doing most of the work in R, so that you have a script documenting clearly what you're doing and making everything you do to the data reproducible.

In both cases, make sure you keep a copy of your tidied data and your original row data, in case there is any issue.


## File format

If your data lies in a spreadsheet like Excel, Google Sheets or LibreOffice Calc, we recommend you save your data as a csv file. There are external packages that can help you import data directly from Excel, but in our experience, things are more likely to go smoothly if you import your data from a csv file. A csv file is a simple text file where your values are separated by a specific character. As "csv" stands for "comma separated value", you can guess that in general, this specific character is the comma.

Download this Excel file and follow the steps, using the tab called "Exple1 - good" as the data sheet we want to save: [BasicExample.xlsx](https://github.com/stats4sd/r2020_04Importation/raw/main/BasicExample.xlsx)
Note that if you don't have Excel on your computer, use any spreadsheet software that you like. The steps should be very similar.


Click on the tab of the data that you want to save. Check that the data is in the right shape, then click `File -> Save As`

<img src="./images/save0bis.PNG" width="80%" style="display: block; margin: auto auto auto 0;" />

Choose where you want to save your file, give it a sensible names, and in `Save as types`, choose 'CSV (comma delimited)' (or similar). It is recommended to save it in the same folder as the R project.

<img src="./images/save3.PNG" width="100%" style="display: block; margin: auto auto auto 0;" />

Finally click `Save`. You may then get a warning that you are saving only one of your sheets, which is normal. You just want to save the data in the active tab.


If your data comes from another statistical software like SAS, SPSS, STATA, or from an SQL database, then, your data is already in a nice format for importation.


*Question: download the following Excel file containing data from an on station experiment and try to save it as a csv file, following the steps above. Call this file Fallow.csv*
[Fallow.xlsx](https://github.com/stats4sd/R4CCRP_04_import/raw/main/Fallow.xlsx)





## Importing data


### Have your R Markdown file ready

To start with, you should be on your project folder and have a new empty R Markdown file opened. To create a new R Markdown file go to `File -> New file -> R Markdown...` 

<img src="./images/rmarkdown.PNG" width="80%" style="display: block; margin: auto auto auto 0;" />

To make it empty, simply click `Create Empty Document` at the bottom left of the next window.

<img src="./images/rmarkdown2.PNG" width="60%" style="display: block; margin: auto auto auto 0;" />



### Importing your file

R can import data from many different format and we will not cover all of them here. In particular, we will not see how to retrieve data from an SQL database, as it is slightly more advanced than the scope of this course. The following documentation  <a href="https://db.rstudio.com" target="_blank">here </a> should be a good starting point though. If you have any question related to it, don't hesitate to post it in the "Out of scope questions" forum. 

For data coming from SAS, SPSS or STATA, you will have to use an external package to import your file into R. There are multiple options, but we recommend you use the package `haven`, which is another package included in tidyverse. What's nice with this package is that it is embedded in the RStudio importation menu, and so the method to import data works the same way as with a csv file. That is:


From Rstudio, click on the `import dataset` menu. It is located at the top right of your screen if you haven't changed the default organisation of the Rstudio windows.
<img src="./images/import1.PNG" width="100%" style="display: block; margin: auto auto auto 0;" />

You can see that you have several options to choose from. If you were importing data from SAS, SPSS or STATA, you would use the relevant option at the bottom. This requires the package Haven to be installed, but as said before, it is part of tidyverse, so if tidyverse is installed, it should work well. You can also see the option "From Excel...". So importing data directly from Excel is possible via the menu as well. But as said earlier, it is not uncommon to have unexpected issue when importing data directly from Excel, so we recommend to stick to an importation via csv file. And if your data is saved as a csv file, you should just click on the first option `From Text (base)`
<img src="./images/import2.PNG" width="70%" style="display: block; margin: auto auto auto 0;" />


Locate your csv file
<img src="./images/import3.PNG" width="70%" style="display: block; margin: auto auto auto 0;" />

Check in the preview window that the importation seems to work well. If you see some issues like weird column names, weird rows or columns, play with the parameters on the left to fix the issues. Click `Import`
<img src="./images/import4.PNG" width="80%" style="display: block; margin: auto auto auto 0;" />


Check your environment window for the number of rows and columns of your new object.
<img src="./images/import5.PNG" width="60%" style="display: block; margin: auto auto auto 0;" />

Click on the triangle next to the name of your object to have an overview of the column types. Check that the columns that should be numeric are not listed as character variables (chr). If you find such issue, it probably means that there is some non-numerical character(s) somewhere in your original data that prevented R to consider the column as numeric.
<img src="./images/import6bis.PNG" width="60%" style="display: block; margin: auto auto auto 0;" />

Copy the command that R just wrote in the console panel (only the `read.csv()` command. The `View()` command is an interactive command that should not be on your scripts).
<img src="./images/import7.PNG" width="80%" style="display: block; margin: auto auto auto 0;" />

Insert a first R chunk at the top of your R Markdown file
<img src="./images/import8.PNG" width="50%" style="display: block; margin: auto auto auto 0;" />


Then paste the importing command inside the R chunk 
<img src="./images/import9.PNG" width="70%" style="display: block; margin: auto auto auto 0;" />

We are done with the importation step. We can now start working on this data. Don't forget to load the libraries that you will need and to write text outside the R chunks to document what you're doing.
<img src="./images/import10.PNG" width="100%" style="display: block; margin: auto auto auto 0;" />


Having the importation command in your R Markdown script file is important, so that the next time you open RStudio, you don't have to go through the importation process again. You can just run the relevant R chunk and your data will be imported!

Note: you can see that the importation command contains a path to your data file. So if you move your data, for example to place it in a specific data folder in your project, you'll have to change the path.


*Question: Follow the steps above to import the Fallow.csv file that you saved in the previous section. Have a look at the appendix to know more about this dataset*



## Quiz

*Question 1*


```{=html}
<div class="panel panel-default">
<div data-label="Q1" class="tutorial-question panel-body">
<div id="Q1-answer_container" class="shiny-html-output"></div>
<div id="Q1-message_container" class="shiny-html-output"></div>
<div id="Q1-action_button_container" class="shiny-html-output"></div>
<script>if (Tutorial.triggerMathJax) Tutorial.triggerMathJax()</script>
</div>
</div>
```




<img src="./images/packageQuestion.JPG" width="100%" style="display: block; margin: auto auto auto 0;" />


*Question 2*


```{=html}
<div class="panel panel-default">
<div data-label="Q2" class="tutorial-question panel-body">
<div id="Q2-answer_container" class="shiny-html-output"></div>
<div id="Q2-message_container" class="shiny-html-output"></div>
<div id="Q2-action_button_container" class="shiny-html-output"></div>
<script>if (Tutorial.triggerMathJax) Tutorial.triggerMathJax()</script>
</div>
</div>
```




<img src="./images/Quiz1.PNG" width="100%" style="display: block; margin: auto auto auto 0;" />


*Question 3*


```{=html}
<div class="panel panel-default">
<div data-label="Q3" class="tutorial-question panel-body">
<div id="Q3-answer_container" class="shiny-html-output"></div>
<div id="Q3-message_container" class="shiny-html-output"></div>
<div id="Q3-action_button_container" class="shiny-html-output"></div>
<script>if (Tutorial.triggerMathJax) Tutorial.triggerMathJax()</script>
</div>
</div>
```


*Question 4*


```{=html}
<div class="panel panel-default">
<div data-label="Q4" class="tutorial-question panel-body">
<div id="Q4-answer_container" class="shiny-html-output"></div>
<div id="Q4-message_container" class="shiny-html-output"></div>
<div id="Q4-action_button_container" class="shiny-html-output"></div>
<script>if (Tutorial.triggerMathJax) Tutorial.triggerMathJax()</script>
</div>
</div>
```




## Exercises


**Exercise 1: Now that you have imported the Fallow dataset into R – let’s do a quick exercise to recap what we learnt in Modules 1-3, but writing out the code entirely in RStudio instead of online.**



1.	Calculate the average yield and striga count for each treatment.
2.	Create  a subset of the dataset with only the rows where the striga count is greater than 0.
3.	Make a plot from the subset that you just created (or the full dataset if you failed to create the subset), showing the relationship between striga count and yield.
 

**Exercise 2: Download the file below that contains the BeanSurvey dataset and the solutions for the module 3 exercises. Save these in your project folder. Import the data using RStudio menu and go through the R Markdown file to reproduce the solutions in your own machine**

[Module-3-Data-and-Solutions.zip](https://github.com/stats4sd/r2020_04Quiz/raw/main/Module-3-Data-and-Solutions.zip)





## Appendix: 'Fallow' dataset 

The Fallow dataset comes from an on station RCBD experiment looking at the effect of crop cover treatments on maize yields and striga counts.

A summary of the columns in the dataset is below.


|Column |Description               |
|:------|:-------------------------|
|rep    |repetition                |
|plot   |plot                      |
|treat  |treatment                 |
|yield  |yield in tons per hectare |
|striga |striga counts             |

## Appendix: 'BeanSurvey' dataset 

The data we are using in this session is an extract of a survey conducted in Uganda from farmers identified as growing beans.

The dataset contains an extract of 50 responses to 23 of the survey questions, and has been imported to R as a data frame called `BeanSurvey`.

A summary of the columns in the dataset is below.


|Column            |Description                                      |
|:-----------------|:------------------------------------------------|
|ID                |Farmer ID                                        |
|VILLAGE           |Village name                                     |
|HHTYPE            |Household composition                            |
|GENDERHH          |Gender of Household Head                         |
|AGEHH             |Age of Household Head                            |
|OCCUHH            |Occupation of Household Head                     |
|ADULTS            |Number of Adults within the household            |
|CHILDREN          |Number of Children (<18) within the household    |
|MATOKE            |Do they grow matoke?                             |
|MAIZE             |Do they grow maize?                              |
|BEANS             |Do they grow beans?                              |
|BANANA            |Do they grow banana?                             |
|CASSAVA           |Do they grow cassava?                            |
|COFFEE            |Do they grow coffee?                             |
|LANDAREA          |Land area of farm (acres)                        |
|LABOR             |Labor usage                                      |
|INTERCROP         |Intercrops with beans                            |
|DECISIONS         |Household decision responsibility                |
|SELLBEANS         |Do they grow beans for sale?                     |
|BEANSPLANTED_LR   |Quantity of beans planted in long rain season    |
|BEANSPLANTED_SR   |Quantity of beans planted in short rain season   |
|BEANSHARVESTED_LR |Quantity of beans harvested in long rain season  |
|BEANSHARVESTED_SR |Quantity of beans harvested in short rain season |


Spend some time exploring the full dataset embedded below, to familiarise yourself with the columns and the type of data stored within each column. You may need to refer back to this data at times during this tutorial. Remember that R is case sensitive, so you will always have to refer to the variables in this dataset exactly as they are written in the data. There is a column in this data called "GENDERHH" but there is no column in this data called "GenderHH".


```{=html}
<div id="htmlwidget-1455afd4b7021a006de7" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-1455afd4b7021a006de7">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50"],[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50],["Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Kimbugu","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala","Lwala"],["Female headed, no husband","Female headed, no husband","Male headed one wife","Female headed, no husband","Single man","Single man","Female headed, no husband","Male headed one wife","Female headed, no husband","Male headed one wife","Male headed more than one wife","Male headed one wife","Male headed one wife","Male headed more than one wife","Female headed, no husband","Female headed, no husband","Other","Female headed, no husband","Male headed more than one wife","Female headed, no husband","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Female headed, no husband","Male headed one wife","Female headed, no husband","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Female headed, no husband","Male headed one wife","Female headed absentee husband","Female headed absentee husband","Female headed, no husband","Male headed more than one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Male headed one wife","Female headed absentee husband"],["female","female","male","female","male","male","female","male","female","male","male","male","male","male","female","female","male","female","male","female","male","male","male","male","male","male","male","male","male","female","male","female","male","male","male","male","female","male","female","female","female","male","male","male","male","male","male","male","male","female"],[32,57,20,55,78,42,28,49,41,54,65,63,32,29,43,68,53,39,25,44,23,47,32,26,25,29,44,23,58,69,26,65,75,51,38,24,35,29,37,45,50,23,60,32,70,43,51,28,65,33],["Farmer","Farmer","Farmer","Farmer","Trader","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Fisherman","Pitsawer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Teacher","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Farmer","Trader","Shop attendant","Farmer","Farmer","Farmer","Pitsawer","Farmer","Fisherman","Farmer","Farmer","Farmer","Fisherman"],[1,3,2,3,1,1,1,2,1,3,4,3,2,2,2,2,1,1,2,3,2,3,2,3,2,1,1,2,13,1,2,2,2,2,2,2,2,5,3,2,2,3,4,2,2,4,2,2,3,3],[2,3,4,4,0,0,1,4,1,3,0,2,3,2,3,1,2,1,2,6,2,4,2,2,2,1,1,1,3,5,5,1,0,3,3,2,3,2,2,4,3,3,2,3,2,4,2,0,2,1],["Yes","Yes","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes","Yes","No","Yes","No","No","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes"],["Yes","Yes","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes","No","Yes","No","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","No","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes","No","No","Yes","Yes","Yes","Yes","No","Yes"],["Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes"],["No","No","No","No","No","Yes","No","Yes","Yes","Yes","Yes","No","Yes","No","No","No","Yes","No","No","No","No","No","No","No","No","No","No","No","Yes","No","No","No","No","No","No","No","No","Yes","No","No","No","No","No","No","Yes","Yes","No","No","No","No"],["Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes"],["Yes","Yes","No","No","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","No","Yes","Yes","No","Yes","No","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes","Yes"],[0.75,0.75,3,0.75,0.75,10,2,1.25,2,2,1.25,3,1.25,0.75,0.75,6.5,2,3,4.25,4.25,2,10,3,2,1.25,2,0.75,3,4.25,0.75,1.25,0.75,0.75,6.5,1.25,0.375,1.25,10,1.25,4.25,0.375,1.25,0.75,6.5,0.75,2,1.25,0.375,1.25,2],["Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses hired labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses hired labor","Uses hired labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses hired labor","Uses hired labor","Uses neither hired or exchange labor","Uses hired labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses hired labor","Uses hired labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses both hired and exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses hired labor","Uses both hired and exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses both hired and exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor","Uses neither hired or exchange labor"],["2 or more crops","Cassava","Cassava","Maize","Maize","Sole crop","Sole crop","Sole crop","2 or more crops","2 or more crops","Sole crop","Sole crop","Cassava","2 or more crops","Maize","Maize","Sole crop","Cassava","Cassava","Maize","Cassava","2 or more crops","Sole crop","Bananas","Cassava","2 or more crops","Sole crop","Cassava","2 or more crops","Cassava","Cassava","Bananas","Cassava","Sole crop","Cassava","Maize","Maize","Maize","Cassava","2 or more crops","Cassava","2 or more crops","Cassava","2 or more crops","Other","Cassava","2 or more crops","Cassava","Cassava","Bananas"],["Female farmer only","Female farmer only","Female farmer only","Female farmer only","Male farmer only","Male farmer only","Female farmer only","Female farmer, consults male farmer","Female farmer only","Both male and female farmer equally","Male farmer only","Both male and female farmer equally","Female farmer only","Female farmer only","Female farmer only","Female farmer only","Male farmer only","Female farmer only","Female farmer only","Female farmer only","Both male and female farmer equally","Female farmer only","Female farmer only","Female farmer only","Female farmer only","Female farmer only","Both male and female farmer equally","Female farmer only","Female farmer only","Female farmer only","Female farmer only","Other","Female farmer, consults male farmer","Female farmer, consults male farmer","Female farmer only","Female farmer only","Female farmer only","Both male and female farmer equally","Female farmer only","Female farmer only","Female farmer only","Female farmer only","Both male and female farmer equally","Female farmer only","Both male and female farmer equally","Female farmer only","Male farmer, consults female farmer","Female farmer only","Female farmer only","Female farmer only"],["No","Yes","No","No","Yes","Yes","No","Yes","Yes","Yes","No","Yes","Yes","Yes","Yes","Yes","No","No","No","No","No","No","Yes","Yes","No","No","No","No","Yes","No","No","No","No","No","No","No","No","No","Yes","No","No","No","No","No","No","No","Yes","Yes","No","No"],[0,4,0,2,1.5,40,0,3,2,3,3,28,0,0,0,5,0,0,5,null,0,10,20,0,7,2.5,0,0,5,2,4.5,0,1,1,2,2,2.5,null,0,0,0,1.5,2,5,2.5,2,4,0,0.5,0],[0,4,0,0,2.5,40,3,0,2,0,2.5,0,1,0,0,3.5,0,0,0,16,2,5,4,3,4,0,1,3,0,3.25,0,0,0,0.75,0,2,2,3,8,0,4,0,0,0,0,0,0,8,0.5,2],[0,10,0,3,20,200,0,null,20,30,10,100,0,0,0,40,0,0,10,null,0,30,90,0,23,10,0,0,10,4,30,0,2,10,10,14,11.5,null,0,0,0,4,7,9,4,8,28,0,2.5,0],[0,0,0,0,13,100,0,0,5,0,15,0,2,0,0,5,0,0,0,50,4,10,20,50,0,0,3,20,0,5,0,0,0,3.75,0,20,4.5,null,18,0,15,0,0,0,0,0,0,100,2,5]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>ID<\/th>\n      <th>VILLAGE<\/th>\n      <th>HHTYPE<\/th>\n      <th>GENDERHH<\/th>\n      <th>AGEHH<\/th>\n      <th>OCCUHH<\/th>\n      <th>ADULTS<\/th>\n      <th>CHILDREN<\/th>\n      <th>MATOKE<\/th>\n      <th>MAIZE<\/th>\n      <th>BEANS<\/th>\n      <th>BANANA<\/th>\n      <th>CASSAVA<\/th>\n      <th>COFFEE<\/th>\n      <th>LANDAREA<\/th>\n      <th>LABOR<\/th>\n      <th>INTERCROP<\/th>\n      <th>DECISIONS<\/th>\n      <th>SELLBEANS<\/th>\n      <th>BEANSPLANTED_LR<\/th>\n      <th>BEANSPLANTED_SR<\/th>\n      <th>BEANSHARVESTED_LR<\/th>\n      <th>BEANSHARVESTED_SR<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,5,7,8,15,20,21,22,23]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script>
```

(You can use the arrow keys on your keyboard to scroll right in case the data table does not fit entirely on your screen)


## Appendix:  Useful reference links  


Illustrated presentation of 'tidy data': <a href="https://docs.google.com/presentation/d/1N7hKepabvl9OrHjvGJWPjUsfzVdB5xzV5AsFndgSwms/edit?usp=sharing" target="_blank">Make friends with tidy data </a> 

Video explaining the command to import text files into R - DataCamp:<a href="https://www.youtube.com/watch?v=Yy-ismDUkkQ" target="_blank">https://www.youtube.com/watch?v=Yy-ismDUkkQ   </a> 

Article on the RStudio support site showing how to import data from different files via the RStudio import menu:<a href="https://support.rstudio.com/hc/en-us/articles/218611977-Importing-Data-with-RStudio" target="_blank">Importing Data with RStudio</a> 


RStudio documentation on connecting to databases using R  <a href="https://db.rstudio.com" target="_blank">https://db.rstudio.com </a>


preserve81346156be68fd51
preservec9380bfbb3117e73
preservea4eb97d7a40093f8
preserveea55499fe28997d1
preserve5c915d1e506b0938
preserve59fce7390d8bcd5c
preservec7052c79693f06ab
<!--html_preserve-->
<script type="application/shiny-prerendered" data-context="dependencies">
{"type":"list","attributes":{},"value":[{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["header-attrs"]},{"type":"character","attributes":{},"value":["2.6"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/pandoc"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["header-attrs.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["jquery"]},{"type":"character","attributes":{},"value":["1.11.3"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/jquery"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["jquery.min.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["bootstrap"]},{"type":"character","attributes":{},"value":["3.3.5"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/bootstrap"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["viewport"]}},"value":[{"type":"character","attributes":{},"value":["width=device-width, initial-scale=1"]}]},{"type":"character","attributes":{},"value":["js/bootstrap.min.js","shim/html5shiv.min.js","shim/respond.min.js"]},{"type":"character","attributes":{},"value":["css/cerulean.min.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["highlightjs"]},{"type":"character","attributes":{},"value":["9.12.0"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/highlightjs"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["highlight.js"]},{"type":"character","attributes":{},"value":["textmate.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/tutorial"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial.js"]},{"type":"character","attributes":{},"value":["tutorial.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial-autocompletion"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/tutorial"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial-autocompletion.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial-diagnostics"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/tutorial"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial-diagnostics.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial-format"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmarkdown/templates/tutorial/resources"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial-format.js"]},{"type":"character","attributes":{},"value":["tutorial-format.css","rstudio-theme.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["jquery"]},{"type":"character","attributes":{},"value":["1.11.3"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/jquery"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["jquery.min.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["navigation"]},{"type":"character","attributes":{},"value":["1.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/navigation-1.1"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tabsets.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["highlightjs"]},{"type":"character","attributes":{},"value":["9.12.0"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/highlightjs"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["highlight.js"]},{"type":"character","attributes":{},"value":["default.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["jquery"]},{"type":"character","attributes":{},"value":["1.11.3"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/jquery"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["jquery.min.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["font-awesome"]},{"type":"character","attributes":{},"value":["5.1.0"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["rmd/h/fontawesome"]}]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["css/all.css","css/v4-shims.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["rmarkdown"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["2.6"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["bootbox"]},{"type":"character","attributes":{},"value":["4.4.0"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/bootbox"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["bootbox.min.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["idb-keyvalue"]},{"type":"character","attributes":{},"value":["3.2.0"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/idb-keyval"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["idb-keyval-iife-compat.min.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[false]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/tutorial"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial.js"]},{"type":"character","attributes":{},"value":["tutorial.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial-autocompletion"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/tutorial"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial-autocompletion.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["tutorial-diagnostics"]},{"type":"character","attributes":{},"value":["0.10.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/tutorial"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["tutorial-diagnostics.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["learnr"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.10.1"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["htmlwidgets"]},{"type":"character","attributes":{},"value":["1.5.3"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["www"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["htmlwidgets.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["htmlwidgets"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["1.5.3"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["jquery"]},{"type":"character","attributes":{},"value":["3.5.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["lib/jquery"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["jquery.min.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["crosstalk"]},{"type":"logical","attributes":{},"value":[true]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["datatables-css"]},{"type":"character","attributes":{},"value":["0.0.0"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["htmlwidgets/css"]}]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["datatables-crosstalk.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["DT"]},{"type":"logical","attributes":{},"value":[true]},{"type":"character","attributes":{},"value":["0.17"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["datatables-binding"]},{"type":"character","attributes":{},"value":["0.17"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["htmlwidgets"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["datatables.js"]},{"type":"NULL"},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["DT"]},{"type":"logical","attributes":{},"value":[false]},{"type":"character","attributes":{},"value":["0.17"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files","pkgVersion"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["dt-core"]},{"type":"character","attributes":{},"value":["1.10.20"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["htmlwidgets/lib/datatables"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["js/jquery.dataTables.min.js"]},{"type":"character","attributes":{},"value":["css/jquery.dataTables.min.css","css/jquery.dataTables.extra.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["DT"]},{"type":"logical","attributes":{},"value":[false]},{"type":"character","attributes":{},"value":["0.17"]}]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["name","version","src","meta","script","stylesheet","head","attachment","package","all_files"]},"class":{"type":"character","attributes":{},"value":["html_dependency"]}},"value":[{"type":"character","attributes":{},"value":["crosstalk"]},{"type":"character","attributes":{},"value":["1.1.1"]},{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["file"]}},"value":[{"type":"character","attributes":{},"value":["www"]}]},{"type":"NULL"},{"type":"character","attributes":{},"value":["js/crosstalk.min.js"]},{"type":"character","attributes":{},"value":["css/crosstalk.css"]},{"type":"NULL"},{"type":"NULL"},{"type":"character","attributes":{},"value":["crosstalk"]},{"type":"logical","attributes":{},"value":[true]}]}]}
</script>
<!--/html_preserve-->
<!--html_preserve-->
<script type="application/shiny-prerendered" data-context="execution_dependencies">
{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["packages"]}},"value":[{"type":"list","attributes":{"names":{"type":"character","attributes":{},"value":["packages","version"]},"class":{"type":"character","attributes":{},"value":["data.frame"]},"row.names":{"type":"integer","attributes":{},"value":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,70,71,72,73,74,75,76,77,78,79,80]}},"value":[{"type":"character","attributes":{},"value":["assertthat","backports","base","broom","cellranger","checkmate","cli","colorspace","compiler","crayon","crosstalk","datasets","DBI","dbplyr","digest","dplyr","DT","ellipsis","evaluate","fastmap","forcats","fs","generics","ggplot2","glue","graphics","grDevices","grid","gtable","haven","highr","hms","htmltools","htmlwidgets","httpuv","httr","jsonlite","knitr","later","learnr","lifecycle","lubridate","magrittr","markdown","methods","mime","modelr","munsell","pillar","pkgconfig","promises","purrr","R6","Rcpp","readr","readxl","renv","reprex","rlang","rmarkdown","rprojroot","rstudioapi","rvest","scales","shiny","stats","stringi","stringr","tibble","tidyr","tidyselect","tidyverse","tools","utils","vctrs","withr","xfun","xml2","xtable","yaml"]},{"type":"character","attributes":{},"value":["0.2.1","1.2.1","4.0.3","0.7.4","1.1.0","2.0.0","2.3.0","2.0-0","4.0.3","1.4.1","1.1.1","4.0.3","1.1.1","2.1.0","0.6.27","1.0.4","0.17","0.3.1","0.14","1.1.0","0.5.1","1.5.0","0.1.0","3.3.3","1.4.2","4.0.3","4.0.3","4.0.3","0.3.0","2.3.1","0.8","1.0.0","0.5.1.1","1.5.3","1.5.5","1.4.2","1.7.2","1.31","1.1.0.1","0.10.1","0.2.0","1.7.9.2","2.0.1","1.1","4.0.3","0.9","0.1.8","0.5.0","1.4.7","2.0.3","1.2.0.1","0.3.4","2.5.0","1.0.6","1.4.0","1.3.1","0.12.0","1.0.0","0.4.10","2.6","2.0.2","0.13","0.3.6","1.1.1","1.6.0","4.0.3","1.5.3","1.4.0","3.0.6","1.1.2","1.1.0","1.3.0","4.0.3","4.0.3","0.3.6","2.4.1","0.21","1.3.2","1.8-4","2.2.1"]}]}]}
</script>
<!--/html_preserve-->