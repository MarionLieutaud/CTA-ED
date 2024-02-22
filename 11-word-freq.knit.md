# Exercise 1: Word frequency analysis

## Introduction

In this tutorial, you will learn how to summarise, aggregate, and analyze text in R:

* How to tokenize and filter text
* How to clean and preprocess text
* How to visualize results with ggplot
* How to perform automated gender assignment from name data (and think about possible biases these methods may enclose)

## Setup 

To practice these skills, we will use a dataset that I have already collected from the Edinburgh Festivals Listings API.  The API provides open access to the listings of Edinburgh's 11 major festivals, including the data for the Edinburgh International Book Festival which we will be using. 

You can try this out yourself too: to obtain these data, you must first obtain a free API key. You can do this by [registering for an account on the Edinburgh Festivals Listings API](https://api.edinburghfestivalcity.com/login).

##  Load data and packages 

Before proceeding, we'll load the remaining packages we will need for this tutorial.
