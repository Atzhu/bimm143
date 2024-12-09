Section 4: Population Scale Analysis \[HOMEWORK\]

> Q13: Read this file into R and determine the sample size for each
> genotype and their corresponding median expression levels for each of
> these genotypes.

    expr<-read.table("rs.txt")
    head(expr)

    ##    sample geno      exp
    ## 1 HG00367  A/G 28.96038
    ## 2 NA20768  A/G 20.24449
    ## 3 HG00361  A/A 31.32628
    ## 4 HG00135  A/A 34.11169
    ## 5 NA18870  G/G 18.25141
    ## 6 NA11993  A/A 32.89721

> Number of samples:

    nrow(expr)

    ## [1] 462

> sample size for each genotype:

    table(expr$geno)

    ## 
    ## A/A A/G G/G 
    ## 108 233 121

> Expression levels medians(looked at stackoverflow):

    library(dplyr)

    ## 
    ## 载入程序包：'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    median_genotype_exp <- expr %>%
      group_by(geno) %>%
      summarize(Median_express = median(exp,na.rm = TRUE))

    median_exp<- table(median_genotype_exp$Median_express)

    print(median_exp)

    ## 
    ##  20.07363  25.06486 31.248475 
    ##         1         1         1

respectively for G/G A/G A/A .

> Q14: Generate a boxplot with a box per genotype, what could you infer
> from the relative expression value between A/A and G/G displayed in
> this plot? Does the SNP effect the expression of ORMDL3?

> ANS: The SNP affects the expression. Clearly the G/G genotype leads to
> reduced gene expression compared to the A/A genotype. The A/G genotype
> leads to an expression level between the two. This shows how the
> having the G SNP leads to reduction in expression.

    library(ggplot2)

Lets make a boxplot

    ggplot(expr)+aes(x=geno,y=exp,fill=geno)+geom_boxplot(notch=TRUE)

![](Class12HW_files/figure-markdown_strict/unnamed-chunk-7-1.png)
