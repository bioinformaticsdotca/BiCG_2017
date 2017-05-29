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

### Reading Data In

We use `read.data` to read in data.

Commands like `head` and `tail` also work in R.  

### Data Types

Float

Factor


### Basic Plotting



### RStudio Notebooks






