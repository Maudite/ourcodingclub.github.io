---
layout: page
title: Frequently asked questions
date: 2015-03-26 00:00:00
author: Izzy Rich & Sam Kellerhals 
permalink: /faq/
---

<head>
   <style>
   
details {
    border: 1px solid #aaa;
  	background: #b1d0da;
    border-radius: 4px;
    padding: .5em .5em 0;
}

summary {
    font-weight: bold;
    margin: -.5em -.5em 0;
    padding: .5em;
}

details[open] {
    padding: .5em;
  	background: #fff;
}

details[open] summary {
  	background: #b1d0da;
    border-bottom: 1px solid #aaa;
    margin-bottom: .5em;
}

intro {
   padding: 0px 80px; 
}

intro .block h2 {
  padding-top: 15px;
  line-height: 27px;
  margin: 0;
}
   </style>
</head>


<!-- Slider -->
<section id="global-header">
    <div class="container">
        <div class="row">
            <div class="col-md-12">
                <div class="block">
                    <h1>Questions & Answers</h1>
                    <b><p><big>Here we have collated some of the questions we encounter most often during our workshops, plus their answers. We will continue expanding this page, so feel free to suggest additions to the content!</big></p></b>
                </div>
            </div>
        </div>
    </div>
</section>

{::options parse_block_html="true" /}

<div style="padding: 20px 100px;">

<!-- Basic skills -->

## Basic skills

<details>
   <summary markdown= "span"> Setting up your workspace </summary>

First of all, what is a working directory? This is the folder that R will look into to find data and save any plots or scripts. To find out where your working directory currently is and to change it see the code below.

```r
# Identify your current directory
getwd()

# Set your working directory
setwd("insert folder path")
```

Alternatively you can set it from the menu: _Session > Set Working Directory > Choose Directory_. For `setwd()`, inside the brackets you should input your file path as follows `setwd("C:/Documents/Directory")`

 </details> 
 <br>
 
 <details>
   <summary markdown= "span"> Loading data and packages </summary>
__Saving and loading your script again__

You should always be typing your code into a script file in order to produce a reproducible record of your analysis; if you only type in the console, R will not save your work! You should save your script often to avoid any problems. To save, click the icon at the top of your R Script to save as an .Rdata file. Here you will have to choose a file name. Try to avoid spaces and capital letters, as R can get confused by these! Save the file to your working directory so it will be easy to locate whenever you need it next. To load your script again, go to _File > Open File_ and choose your script. It should open on a new script tab in RStudio.

__Saving CSV files__

A CSV, or a comma-separated values file, contains values as a series of rows organised so that each column is separated by a comma. If your data is entered in Excel, you can save it as a CSV file by clicking on _Save As_ and then choosing CSV as your file extension. CSV files are often easier to work with in R.

__Loading packages__

R contains thousands of different packages which allow you to do many different things, ranging from mapping to machine learning to web scraping. The best way to find out about what packages may be helpful to you is to do a google search and/or search the <a href="https://cran.r-project.org/web/packages/" target="_blank"> CRAN website </a>. Once you have found your package, you must first install it on your machine and then call it in your script:

```r
# Load CSV file
objectname <- read.csv("filepath/file.csv")

# Installing dplyr package
install.packages("dplyr")

# Load package
library(dplyr)
```

 </details> 
 <br>
 
  <details>
   <summary markdown= "span"> Other tips and resources </summary>


__Writing clean code__

R code should be easy to  read, share and verify. Aim to keep your object naming conventions consistent across your script and make sure to comment your code using a hashtag. For extensive guidelines, please consult Google's R style guide <a href="https://google.github.io/styleguide/Rguide.xml" target="_blank">here</a>.

__Helpful tutorials__

   - <a href="https://ourcodingclub.github.io/2016/11/13/intro-to-r.html" target="_blank"> Introduction to R </a>
   
   - <a href="https://ourcodingclub.github.io/2016/11/15/troubleshooting.html" target="_blank"> Troubleshooting R </a>
   
   - <a href="https://ourcodingclub.github.io/2017/04/25/etiquette.html" target="_blank"> Coding Etiquette </a>

__Useful commands for RStudio__

In order to clean your global environment (all the objects, functions etc. you have created), you can execute the following command in your console: `rm(list=ls())`. To clear your console, you can execute this command `cat("\014")`. 

 </details> 
 <br>
 


<!-- Data manipulation  -->

## Data manipulation

  <details>
   <summary markdown= "span"> Structuring datasets </summary>

When working with data, it is very important to keep it in the correct format to allow for easy and effective analysis, data visualisation and ultimately, to find an answer to your research question! To become more effective at preparing and cleaning your data, it is important to familiarise yourself with the principles of "tidy data", which provide a standard way to organise data values within a dataset that allows for easy manipulation. The three main principles are listed below.

   1. Each variable forms a column.
   
   2. Each observation forms a row.
   
   3. Each type of observational unit forms a table.

Please see Hadley Wickham's <a href="http://vita.had.co.nz/papers/tidy-data.pdf" target="_blank">academic paper</a> or a <a href="https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html" target="_blank">condensed article</a> on tidy data and how to implement it. Below you will find some example code on how to convert messy data to tidy data, using functions from the `tidyr` and `dplyr` packages.

```r
# Loading required packages
library(tidyr)
library(dplyr)

# Loading dataframe
iris <- as.data.frame(iris)
```
<center> <img src="https://ourcodingclub.github.io/img/iris1.png" alt="Img" style="width: 500px;"/> </center>

```r
# Converting iris df to wide dataframe (messy data)
iris.wide <- iris %>%
select(Species, Petal.Width) %>% # Selecting only two columns
filter(Species == "setosa") %>% # Filtering column for one species
```
<center> <img src="https://ourcodingclub.github.io/img/iris2.png" alt="Img" style="width: 200px;"/> </center>

```r
 mutate(sample = row_number()) %>% # Adding row number identifier
spread(sample, Petal.Width) # Spreading data to wide format 
```
<center> <img src="https://ourcodingclub.github.io/img/iris3.png" alt="Img" style="width: 500px;"/> </center>

```r
 # Converting messy iris dataframe to tidy (long) dataframe
iris.long <- iris.wide %>%
gather(Species, Petal.Width) %>% # Gather wide data to long format
rename(Setosa.Sample = Species) # Rename to correct column name 
```

<center> <img src="https://ourcodingclub.github.io/img/iris4.png" alt="Img" style="width: 200px;"/> </center>


 </details> 
 <br>
 
  <details>
   <summary markdown= "span"> Selecting and filtering </summary>

There are a variety of ways to select columns and rows. This can be done by specifying the column/row name or index. However, unlike other programming languages, R starts counting at 1 instead of at 0, as is the case in Python. Other methods include the use of functions from the `dplyr` package.

```r
# Selecting single columns by name or by index (base R)
dataframe$columnName or dataframe[,1]

# Selecting rows in a column (base R)
dataframe$columnName[1:2,]

# Selecting multiple rows and columns (base R)
dataframe[1:2,4:6]

# Selecting columns using the select function (dplyr)
dplyr::select(dataframe, columnName1, columnName2)
```
You may also want to filter the dataset you are working with according to certain conditions. As an example, let's take the built-in `iris` dataset, which describes the petal width and length of different iris species ( _Iris Setosa_, _Iris Versicolour_, _Iris Virginica_). If you are interested to see how flower attributes vary in only one of the groups (species), you can easily do so by using the `filter` function from the `dplyr` package. This function will return a dataset that meets the conditions that you define. See the code below for examples.

```r
 # Loading packages
library(dplyr)

# Loading data and defining as an object
iris <- as.data.frame(iris)

# Filtering for a single condition
filter(iris, Species == "virginica")

# Filter for multiple conditions
filter(iris, Species %in% c("virginica","setosa"), Sepal.Length > 5)

# Other useful filter conditions

    == (equal to)
    < (less than)
    <= (less than or equal to)
    > (greater than)
    >= (greater than or equal to)
    & (and)
    | (or)
    ! (inverse, e.g. != stands for not equal to)

``` 
When dealing with larger datasets, you can use pipes (`%>%`) to apply multiple operations to your dataset, without needing to create multiple objects. This is demonstrated in the code below.

```r
newDataset <- iris %>%
select("Sepal.Length", "Species") %>%
filter(Species == "setosa") %>%
group_by(Species) %>%
summarise(meanSepalLength = mean(Sepal.Length)
``` 

 </details> 
 <br>


<details>
 <summary markdown= "span">Other tips and resources </summary>
   
__Helpful tutorials__

- <a href="https://ourcodingclub.github.io/2017/01/16/piping.html" target="_blank"> Data manipulation </a>
   
- <a href="https://ourcodingclub.github.io/2017/03/20/seecc.html" target="_blank"> Working with big data </a>

 </details>
 <br>
 


<!-- Data viz  -->

## Data visualisation

  <details>
   <summary markdown= "span"> Another question </summary>


 </details> 
 <br>
 
  <details>
   <summary markdown= "span"> Another question </summary>


 </details> 
 <br>


<details>
 <summary markdown= "span">Another question </summary>
    
 </details>
 <br>
 


<!-- Modelling  -->

## Modelling basics

  <details>
   <summary markdown= "span"> Another question </summary>


 </details> 
 <br>
 
  <details>
   <summary markdown= "span"> Another question </summary>


 </details> 
 <br>


<details>
 <summary markdown= "span">Another question </summary>
    
 </details>
 <br>
 


</div>

