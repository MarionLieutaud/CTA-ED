# Week 5 Demo

## Setup
First, we'll load the packages we'll be using in this week's brief demo. 


``` r
#devtools::install_github("conjugateprior/austin")
library(austin)
library(quanteda)
library(quanteda.textstats)
```

## Wordscores

We can inspect the function for the wordscores model by @laver_extracting_2003 in the following way:


``` r
classic.wordscores
```

```
## function (wfm, scores) 
## {
##     if (!is.wfm(wfm)) 
##         stop("Function not applicable to this object")
##     if (length(scores) != length(docs(wfm))) 
##         stop("There are not the same number of documents as scores")
##     if (any(is.na(scores))) 
##         stop("One of the reference document scores is NA\nFit the model with known scores and use 'predict' to get virgin score estimates")
##     thecall <- match.call()
##     C.all <- as.worddoc(wfm)
##     C <- C.all[rowSums(C.all) > 0, ]
##     F <- scale(C, center = FALSE, scale = colSums(C))
##     ws <- apply(F, 1, function(x) {
##         sum(scores * x)
##     })/rowSums(F)
##     pi <- matrix(ws, nrow = length(ws))
##     rownames(pi) <- rownames(C)
##     colnames(pi) <- c("Score")
##     val <- list(pi = pi, theta = scores, data = wfm, call = thecall)
##     class(val) <- c("classic.wordscores", "wordscores", class(val))
##     return(val)
## }
## <bytecode: 0x116d4c2f0>
## <environment: namespace:austin>
```

We can then take some example data included in the `austin` package.


``` r
data(lbg)
ref <- getdocs(lbg, 1:5)
```

And here our reference documents are all those documents marked with an "R" for reference; i.e., columns one to five.


``` r
ref
```

```
##      docs
## words  R1  R2  R3  R4  R5
##    A    2   0   0   0   0
##    B    3   0   0   0   0
##    C   10   0   0   0   0
##    D   22   0   0   0   0
##    E   45   0   0   0   0
##    F   78   2   0   0   0
##    G  115   3   0   0   0
##    H  146  10   0   0   0
##    I  158  22   0   0   0
##    J  146  45   0   0   0
##    K  115  78   2   0   0
##    L   78 115   3   0   0
##    M   45 146  10   0   0
##    N   22 158  22   0   0
##    O   10 146  45   0   0
##    P    3 115  78   2   0
##    Q    2  78 115   3   0
##    R    0  45 146  10   0
##    S    0  22 158  22   0
##    T    0  10 146  45   0
##    U    0   3 115  78   2
##    V    0   2  78 115   3
##    W    0   0  45 146  10
##    X    0   0  22 158  22
##    Y    0   0  10 146  45
##    Z    0   0   3 115  78
##    ZA   0   0   2  78 115
##    ZB   0   0   0  45 146
##    ZC   0   0   0  22 158
##    ZD   0   0   0  10 146
##    ZE   0   0   0   3 115
##    ZF   0   0   0   2  78
##    ZG   0   0   0   0  45
##    ZH   0   0   0   0  22
##    ZI   0   0   0   0  10
##    ZJ   0   0   0   0   3
##    ZK   0   0   0   0   2
```

This matrix is simply a series of words (here: letters) and reference texts with word counts for each of them. 

We can then look at the wordscores for each of the words, calculated using the reference dimensions for each of the reference documents.


``` r
ws <- classic.wordscores(ref, scores=seq(-1.5,1.5,by=0.75))
ws
```

```
## $pi
##         Score
## A  -1.5000000
## B  -1.5000000
## C  -1.5000000
## D  -1.5000000
## E  -1.5000000
## F  -1.4812500
## G  -1.4809322
## H  -1.4519231
## I  -1.4083333
## J  -1.3232984
## K  -1.1846154
## L  -1.0369898
## M  -0.8805970
## N  -0.7500000
## O  -0.6194030
## P  -0.4507576
## Q  -0.2992424
## R  -0.1305970
## S   0.0000000
## T   0.1305970
## U   0.2992424
## V   0.4507576
## W   0.6194030
## X   0.7500000
## Y   0.8805970
## Z   1.0369898
## ZA  1.1846154
## ZB  1.3232984
## ZC  1.4083333
## ZD  1.4519231
## ZE  1.4809322
## ZF  1.4812500
## ZG  1.5000000
## ZH  1.5000000
## ZI  1.5000000
## ZJ  1.5000000
## ZK  1.5000000
## 
## $theta
## [1] -1.50 -0.75  0.00  0.75  1.50
## 
## $data
##      docs
## words  R1  R2  R3  R4  R5
##    A    2   0   0   0   0
##    B    3   0   0   0   0
##    C   10   0   0   0   0
##    D   22   0   0   0   0
##    E   45   0   0   0   0
##    F   78   2   0   0   0
##    G  115   3   0   0   0
##    H  146  10   0   0   0
##    I  158  22   0   0   0
##    J  146  45   0   0   0
##    K  115  78   2   0   0
##    L   78 115   3   0   0
##    M   45 146  10   0   0
##    N   22 158  22   0   0
##    O   10 146  45   0   0
##    P    3 115  78   2   0
##    Q    2  78 115   3   0
##    R    0  45 146  10   0
##    S    0  22 158  22   0
##    T    0  10 146  45   0
##    U    0   3 115  78   2
##    V    0   2  78 115   3
##    W    0   0  45 146  10
##    X    0   0  22 158  22
##    Y    0   0  10 146  45
##    Z    0   0   3 115  78
##    ZA   0   0   2  78 115
##    ZB   0   0   0  45 146
##    ZC   0   0   0  22 158
##    ZD   0   0   0  10 146
##    ZE   0   0   0   3 115
##    ZF   0   0   0   2  78
##    ZG   0   0   0   0  45
##    ZH   0   0   0   0  22
##    ZI   0   0   0   0  10
##    ZJ   0   0   0   0   3
##    ZK   0   0   0   0   2
## 
## $call
## classic.wordscores(wfm = ref, scores = seq(-1.5, 1.5, by = 0.75))
## 
## attr(,"class")
## [1] "classic.wordscores" "wordscores"         "list"
```

And here we see the thetas contained in this wordscores object, i.e., the reference dimensions for each of the reference documents and the pis, i.e., the estimated wordscores for each word. 

We can now use these to score the so-called "virgin" texts as follows. 


``` r
#get "virgin" documents
vir <- getdocs(lbg, 'V1')
vir
```

```
##      docs
## words  V1
##    A    0
##    B    0
##    C    0
##    D    0
##    E    0
##    F    0
##    G    0
##    H    2
##    I    3
##    J   10
##    K   22
##    L   45
##    M   78
##    N  115
##    O  146
##    P  158
##    Q  146
##    R  115
##    S   78
##    T   45
##    U   22
##    V   10
##    W    3
##    X    2
##    Y    0
##    Z    0
##    ZA   0
##    ZB   0
##    ZC   0
##    ZD   0
##    ZE   0
##    ZF   0
##    ZG   0
##    ZH   0
##    ZI   0
##    ZJ   0
##    ZK   0
```

``` r
# predict textscores for the virgin documents
predict(ws, newdata=vir)
```

```
## 37 of 37 words (100%) are scorable
## 
##     Score Std. Err. Rescaled  Lower  Upper
## V1 -0.448    0.0119   -0.448 -0.459 -0.437
```

## Wordfish


If we wish, we can inspect the function for the wordscores model by @slapin_scaling_2008 in the following way. This is a much more complex algorithm, which is not printed here, but you can inspect on your own devices. 



``` r
wordfish
```

We can then simulate some data, formatted appropriately for wordfiash estimation in the following way:


``` r
dd <- sim.wordfish()

dd
```

```
## $Y
##      docs
## words D01 D02 D03 D04 D05 D06 D07 D08 D09 D10
##   W01  28  19  19  17  15  15   7   6   3   3
##   W02  20  18  19   9  25  18   5   6   6   5
##   W03  18  13  21  16  16  12   9   9  13   6
##   W04  24  23  21  18  10  14  15  11   3   6
##   W05  20  15  14  19  17  16  12   8   8   2
##   W06   4   4   5  12  12  12  11   8  19  21
##   W07   4   9   9  10  15  10  11  17  12  29
##   W08   5   5   7   6  12  12  19  21  20  23
##   W09   3   5   8   8  18  11  15  15  16  26
##   W10   6   8   7  10  11  11  17  24  16  16
##   W11  56  56  51  40  26  31  23  21  23  12
##   W12  70  55  54  46  39  37  35  23  14  11
##   W13  66  55  47  53  32  30  35  24  17  13
##   W14  57  56  53  38  45  24  24  20  25  12
##   W15  65  59  50  43  38  38  26  21  16  20
##   W16  11   9  20  34  40  38  33  54  70  56
##   W17  20  25  29  23  30  49  57  50  50  67
##   W18  12  27  18  37  33  47  50  48  54  62
##   W19   4  18  26  33  33  41  41  55  60  66
##   W20   7  21  22  28  33  34  55  59  55  44
## 
## $theta
##  [1] -1.4863011 -1.1560120 -0.8257228 -0.4954337 -0.1651446  0.1651446
##  [7]  0.4954337  0.8257228  1.1560120  1.4863011
## 
## $doclen
## D01 D02 D03 D04 D05 D06 D07 D08 D09 D10 
## 500 500 500 500 500 500 500 500 500 500 
## 
## $psi
##  [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1
## 
## $beta
##  [1] 0 0 0 0 0 1 1 1 1 1 0 0 0 0 0 1 1 1 1 1
## 
## attr(,"class")
## [1] "wordfish.simdata" "list"
```

Here we can see the document and word-level FEs, as well as the specified range of the thetas to be estimates. 

Then estimating the document positions is simply a matter of implementing this algorithm.


``` r
wf <- wordfish(dd$Y)
summary(wf)
```

```
## Call:
## 	wordfish(wfm = dd$Y)
## 
## Document Positions:
##     Estimate Std. Error    Lower    Upper
## D01 -1.69510    0.12089 -1.93203 -1.45817
## D02 -1.03074    0.09938 -1.22552 -0.83597
## D03 -0.80504    0.09462 -0.99050 -0.61959
## D04 -0.37623    0.08888 -0.55042 -0.20203
## D05 -0.07543    0.08732 -0.24658  0.09572
## D06  0.11443    0.08738 -0.05683  0.28568
## D07  0.45522    0.08947  0.27985  0.63059
## D08  0.84380    0.09508  0.65746  1.03015
## D09  1.08842    0.10043  0.89157  1.28526
## D10  1.47995    0.11213  1.26018  1.69971
```

## Using `quanteda`

We can also use `quanteda` to implement the same scaling techniques, as demonstrated in Exercise 4. 

