# Assessment data

## Introduction

Below you will find a series of datasets. You can choose to use these for the summative assessment. Alternatively, you can contact me with a suggestion of a dataset and a relevant research question. See the [Course Overview](https://cjbarrie.github.io/CTA-ED/course-overview.html) page for full details of the assessment.

## @osnabrugge_playing_2021 data

We can access data from @osnabrugge_playing_2021 [here](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/QDTLYV)

To prepare these data, we can use the same code as used by the original authors:


``` r
library("ggplot2")
library("plyr")
library("gdata")
library("stringr")
library("data.table")
library("kableExtra")
library("tidyverse")
```



``` r
## Prep Osnabrugge et al. - after downloading the dataset (see instructions above), check where you have stored in on your computer and include the path to the data in the code below.
# I have given you the example with the path on my own computer, but you will need to change it.
data = fread("User/marionlieutaud/document/data/osnabrugge_uk_data.csv", encoding="UTF-8")


data$date = as.Date(data$date)


#Table 2: Examples: Emotive and neutral speeches
example1 = subset(data, id_speech==854597)
example1$emotive_rhetoric
example1$text

example2 = subset(data, id_speech==778143)
example2$emotive_rhetoric
example2$text

#Create time variable
data$time= NA
data$time[data$date>=as.Date("2001-01-01") & data$date<=as.Date("2001-06-30")] = "01/1"
data$time[data$date>=as.Date("2001-07-01") & data$date<=as.Date("2001-12-31")] = "01/2"
data$time[data$date>=as.Date("2002-01-01") & data$date<=as.Date("2002-06-30")] = "02/1"
data$time[data$date>=as.Date("2002-07-01") & data$date<=as.Date("2002-12-31")] = "02/2"
data$time[data$date>=as.Date("2003-01-01") & data$date<=as.Date("2003-06-30")] = "03/1"
data$time[data$date>=as.Date("2003-07-01") & data$date<=as.Date("2003-12-31")] = "03/2"
data$time[data$date>=as.Date("2004-01-01") & data$date<=as.Date("2004-06-30")] = "04/1"
data$time[data$date>=as.Date("2004-07-01") & data$date<=as.Date("2004-12-31")] = "04/2"
data$time[data$date>=as.Date("2005-01-01") & data$date<=as.Date("2005-06-30")] = "05/1"
data$time[data$date>=as.Date("2005-07-01") & data$date<=as.Date("2005-12-31")] = "05/2"
data$time[data$date>=as.Date("2006-01-01") & data$date<=as.Date("2006-06-30")] = "06/1"
data$time[data$date>=as.Date("2006-07-01") & data$date<=as.Date("2006-12-31")] = "06/2"
data$time[data$date>=as.Date("2007-01-01") & data$date<=as.Date("2007-06-30")] = "07/1"
data$time[data$date>=as.Date("2007-07-01") & data$date<=as.Date("2007-12-31")] = "07/2"
data$time[data$date>=as.Date("2008-01-01") & data$date<=as.Date("2008-06-30")] = "08/1"
data$time[data$date>=as.Date("2008-07-01") & data$date<=as.Date("2008-12-31")] = "08/2"
data$time[data$date>=as.Date("2009-01-01") & data$date<=as.Date("2009-06-30")] = "09/1"
data$time[data$date>=as.Date("2009-07-01") & data$date<=as.Date("2009-12-31")] = "09/2"
data$time[data$date>=as.Date("2010-01-01") & data$date<=as.Date("2010-06-30")] = "10/1"
data$time[data$date>=as.Date("2010-07-01") & data$date<=as.Date("2010-12-31")] = "10/2"
data$time[data$date>=as.Date("2011-01-01") & data$date<=as.Date("2011-06-30")] = "11/1"
data$time[data$date>=as.Date("2011-07-01") & data$date<=as.Date("2011-12-31")] = "11/2"
data$time[data$date>=as.Date("2012-01-01") & data$date<=as.Date("2012-06-30")] = "12/1"
data$time[data$date>=as.Date("2012-07-01") & data$date<=as.Date("2012-12-31")] = "12/2"
data$time[data$date>=as.Date("2013-01-01") & data$date<=as.Date("2013-06-30")] = "13/1"
data$time[data$date>=as.Date("2013-07-01") & data$date<=as.Date("2013-12-31")] = "13/2"
data$time[data$date>=as.Date("2014-01-01") & data$date<=as.Date("2014-06-30")] = "14/1"
data$time[data$date>=as.Date("2014-07-01") & data$date<=as.Date("2014-12-31")] = "14/2"
data$time[data$date>=as.Date("2015-01-01") & data$date<=as.Date("2015-06-30")] = "15/1"
data$time[data$date>=as.Date("2015-07-01") & data$date<=as.Date("2015-12-31")] = "15/2"
data$time[data$date>=as.Date("2016-01-01") & data$date<=as.Date("2016-06-30")] = "16/1"
data$time[data$date>=as.Date("2016-07-01") & data$date<=as.Date("2016-12-31")] = "16/2"
data$time[data$date>=as.Date("2017-01-01") & data$date<=as.Date("2017-06-30")] = "17/1"
data$time[data$date>=as.Date("2017-07-01") & data$date<=as.Date("2017-12-31")] = "17/2"
data$time[data$date>=as.Date("2018-01-01") & data$date<=as.Date("2018-06-30")] = "18/1"
data$time[data$date>=as.Date("2018-07-01") & data$date<=as.Date("2018-12-31")] = "18/2"
data$time[data$date>=as.Date("2019-01-01") & data$date<=as.Date("2019-06-30")] = "19/1"
data$time[data$date>=as.Date("2019-07-01") & data$date<=as.Date("2019-12-31")] = "19/2"

data$time2 = data$time
data$time2 = str_replace(data$time2, "/", "_")

data$stage = 0
data$stage[data$m_questions==1]= 1
data$stage[data$u_questions==1]= 2
data$stage[data$queen_debate_others==1]= 3
data$stage[data$queen_debate_day1==1]= 4
data$stage[data$pm_questions==1]= 5
```

Below, I display a sample of these data.



<table class="table table-striped" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> id_speech </th>
   <th style="text-align:left;"> text </th>
   <th style="text-align:left;"> last_name </th>
   <th style="text-align:left;"> first_name </th>
   <th style="text-align:left;"> date </th>
   <th style="text-align:right;"> government </th>
   <th style="text-align:right;"> female </th>
   <th style="text-align:right;"> age </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 937638 </td>
   <td style="text-align:left;"> I am afraid I simply do not accept that the latter point is true This Parliament voted by a majority of nearly 300 to give the go ahead to a project that I personally believe is of key strategic importance to the United Kingdom over the coming decades I think that says it all </td>
   <td style="text-align:left;"> grayling </td>
   <td style="text-align:left;"> chris </td>
   <td style="text-align:left;"> 2019-06-13 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 57 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 11670 </td>
   <td style="text-align:left;"> Yes Madam Deputy Speaker On 25 October  I asked a parliamentary question on the very same subject when the risk assessment would be published and received a holding reply on 30 October  Although I have heard no more from the Minister since on Monday morning I was amazed to read in The Daily Telegraph an extensive briefing which turns out to be extensively correct on precisely what would happen when the risk assessment was received I have still not received any response from the Minister to my perfectly legitimate question on the risk assessment That seems to be clear evidence that as my hon Friend the Member for Mid Worcestershire Mr Luff has correctly said the Government are more determined to spin the story in the press than to inform hon Members Is that not disgraceful </td>
   <td style="text-align:left;"> gray </td>
   <td style="text-align:left;"> james </td>
   <td style="text-align:left;"> 2001-11-15 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 47 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 251110 </td>
   <td style="text-align:left;"> Does the hon Gentleman agree that although the Minister mentioned that the Government had allocated an extra 21 million that equates to 30 000 per constituency Does he also agree that that does not nearly cover the additional burden that has been placed on electoral registration officers over the past five years More particularly that money is not ring fenced so we do not even know whether it will be spent on that purpose </td>
   <td style="text-align:left;"> binley </td>
   <td style="text-align:left;"> brian </td>
   <td style="text-align:left;"> 2007-02-26 </td>
   <td style="text-align:right;"> 1 </td>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 65 </td>
  </tr>
</tbody>
</table>

If the full dataset is too large for your machines, you can easily take a sample of it with:


``` r
data_samp <- data %>%
  sample_n(10000)
```

## Twitter Transparency data

Select a dataset/datasets of interest from the Twitter Transparency archive [here](https://transparency.twitter.com/en/reports/information-operations.html). These are datasets that have been flagged for "information operations" activity; that is, activity designed to distort, often through automated messaging, the information landscape to the benefit of a given entity (normally a government).

The datasets are all listed and downloadable in ".csv" format if you scroll down to "03. Download Archive." Here, you will just be asked to enter your email address as agreement to Terms of Use.

## @waller2021

You can download embeddings and online community scores used in this article the Github repo linked [here](https://github.com/CSSLab/social-dimensions).

To get the community embeddings data in usable format we can do:


``` r
embeddings <- read.table("https://raw.githubusercontent.com/CSSLab/social-dimensions/main/data/embedding-vectors.tsv")

embeddings_metadata <- data.table:::fread("https://raw.githubusercontent.com/CSSLab/social-dimensions/main/data/embedding-metadata.tsv")

embeddings_scores <- read.csv("https://raw.githubusercontent.com/CSSLab/social-dimensions/main/data/scores.csv")
```

Then to add in information on what each vector of dimensions 150 (i.e., here: columns), we can add in the community information to the embeddings with:


``` r
communities <- embeddings_metadata$community

rownames(embeddings) <- communities
```

## R Markdown

You can access a template R Markdown response for your code from the Github repo for this book by clicking this [link](https://raw.githubusercontent.com/cjbarrie/CTA-ED/main/data/assessment/CTA_example.Rmd?raw=true) and download the word document it outputs by clicking this [link](https://github.com/cjbarrie/CTA-ED/blob/main/data/assessment/CTA_example.docx?raw=true).

Though you **should submit the R markdown output in word** you can also see what it looks like when generated as html [here](https://raw.githack.com/cjbarrie/CTA-ED/main/data/assessment/CTA_example.html).
