---
layout: tutorial_page
permalink: /bicg-2017-Unix_and_R
title: BiCG Unix and R Review
header1: Workshop Pages for Students
header2: Bioinformatics for Cancer Genomics
image: /site_images/CBW_cancerDNA_icon-16.jpg
home: https://bioinformaticsdotca.github.io/bicg_2017
---


# CBW BiCG Unix and R Review Session  

## Introduction

Welcome to the review for **Unix and R**! This lab will introduce you to the the command line and using R.

After this lab, you will be able to:

* use common commands in Unix
* read data into R
* produce basic plots in R

## Before We Begin

Read these [directions](http://bioinformaticsdotca.github.io/AWS_setup) for information on how to log in to your assigned Amazon node.

## Unix Review

Basic commands:

* ls: list the files in the directory  
* mkdir: make a new directory  
* cd: change directories  
* pwd: print working directory  
* echo: print what it typed  
* cat: print the contents of a file  
* curl: used to get contents from a URL  
* head and tail: get the beginning or end of a file  
* less and more: look at the contents of a file  
* cp: copy  
* mv: move  
* rm: remove  
* grep: pattern matching  
* man: get the manual explanation of a function

## R Review

### Connecting To RStudio

* Open an internet browser.  
* In the URL bar, enter *http://cbwxx.dyndns.info:8080* replacing *xx* with your provided student number.  
* Enter the supplied username and password.  

### RStudio Notebooks

### Getting Around

#### The Hard Way

```r
# get the current working directory:
getwd()
# set a new working directory:
setwd("C:/myPATH")
setwd("~/myPATH") # on Mac
setwd("/Users/david/myPATH") # on Mac
# list the files in the current working directory:
list.files()
# list objects in the current R session:
ls()
```

#### The Easy Way

In RStudio we can use the "Files" tab to navigate.  
  
### Data Types

#### Vectors

```r
numeric.vector <- c(1,2,3,4,5,6,2,1)
numeric.vector

character.vector <- c("Fred", "Barney", "Wilma", "Betty")
character.vector

logical.vector <- c(TRUE, TRUE, FALSE, TRUE)
logical.vector
```

To refer to elements in the vector:

```r
character.vector
character.vector[2]
character.vector[2:3]
character.vector[c(2,4)]
```

#### Matrices

You can create a 3x4 numeric matrix with:

```r
matrix.example <- matrix(1:12, nrow = 3, ncol=4, byrow = FALSE)
matrix.example

matrix.example <- matrix(1:12, nrow = 3, ncol=4, byrow = TRUE)
matrix.example
```

Alternatively, you can create a matrix by combining vectors:

```r
dataset.a <- c(1,22,3,4,5)
dataset.b <- c(10,11,13,14,15)
dataset.a
dataset.b

rbind.together <- rbind(dataset.a, dataset.b)
rbind.together

cbind.together <- cbind(dataset.a, dataset.b)
cbind.together
```
To get elements of the matrix:

```r
matrix.example[2,4]
matrix.example[2,]
matrix.example[,4]
```

You can add column and row names to the matrix and use the new names to get the elements of the matrix:

```r
colnames(matrix.example) <- c("Sample1","Sample2","Sample3","Sample4")
rownames(matrix.example) <- paste("gene",1:3,sep="_")
matrix.example

matrix.example[,"Sample2"]
matrix.example[1,"Sample2"]
matrix.example["gene_1","Sample2"]
```

Note that all columns in a matrix must have the same mode(numeric, character, etc.) and the same length.

#### Dataframes

Dataframes are similar to arrays but different columns can have different modes (numeric, character, factor, etc.).  

```r
people.summary <- data.frame(
                             age = c(30,29,25,25),
                             names = c("Fred", "Barney", "Wilma", "Betty"),
                             gender = c("m", "m", "f", "f")
                             )
people.summary
```

To get elements of the dataframe:

```r
people.summary[2,1]
people.summary[2,]
people.summary[,1]
people.summary$age
```

#### Lists

Lists gather together a collection of objects under one name.

```r
together.list <- list(
                      vector.example = dataset.a, 
                      matrix.example = matrix.example,
                      data.frame.example = people.summary
                      )
together.list
```

There are several ways to get elements of a list:

```r

together.list$matrix.example
together.list$matrix.example[,3]
together.list["matrix.example"]
together.list[["matrix.example"]]
together.list[["matrix.example"]][,2]
```

### Reading Data In

We use `read.data` to read in data.

Commands like `head` and `tail` also work in R.

### Basic Plotting



### RStudio Notebooks






