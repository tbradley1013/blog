---
title: 'dragondown: A bookdown template for writing your thesis/dissertation at Drexel
  University in R'
author: Tyler Bradley
date: '2019-07-13'
slug: dragondown-thesis-dissertation-template-drexel-university
categories:
  - R
tags:
  - bookdown
  - thesisdown
  - gradschool
description: ''
topics: []
---



I am happy to introduce the [`dragondown`](https://github.com/tbradley1013/dragondown) R package. This package will allow for you to write your Drexel University Master's or PhD Thesis/Dissertation entirely in Rmarkdown without having to write it in LaTeX. This package is inspired by the [`thesisdown`](https://github.com/ismayc/thesisdown) package. 

## How it works

Using `dragondown` is fairly straightforward. `dragondown` (along with other Rmarkdown projects) are typically best when done in RStudio, so your first step is to install RStudio and R. You can find the latest version of R [here](https://www.r-project.org/) and RStudio [here](https://www.rstudio.com/products/rstudio/download/). Once you have R and RStudio installed, you will need to install a LaTeX distribution. Luckily for you, Yihui Xie has created the [`tinytex`](https://yihui.name/tinytex/) distribution which can be easily installed for using with R. You can install it as follows:

```
install.packages('tinytex')
tinytex::install_tinytex()
```

Once you have these prerequisites installed, you can now install the `bookdown` and the `dragondown` packages from GitHub. You can do this with the following code:

```
if (!require("remotes")) install.packages("remotes", repos = "http://cran.rstudio.org")
remotes::install_github("rstudio/bookdown")
remotes::install_github("tbradley1013/dragondown")
```

Now you can create a thesis project easily from RStudio. Select `File -> New File -> R Markdown` from the menu. When the pop-up opens, select "From Template" from the left hand side and then find the "Drexel Thesis" option from the list, as shown here:

![](/images/dragondown/thesis_rmd.png)

Please note, that your must use the name "index" so that your `index.Rmd` file is created correctly. One you select "OK", a new folder (also named index) will be created wherever you specify in the Location input. All of the template files will be created within the index folder that is created. Note that once the folder is created, you can rename the folder, as long as you do not rename the `index.Rmd` file within the folder. 

Now you are ready to get to work! You create a new Rmarkdown document for each chapter within your dissertation as shown in the example files that are generated when you create the project. If you add more chapters, or rename the existing ones, you will have to update your `_bookdown.yml` file to indicate the correct order for your files. 

Whenever you want to see what your current work looks like in the final format, you can open your `index.Rmd` file and select the "Knit" option at the top of the script. This will create the book from all of the files listed in the `_bookdown.yml` file. 

I recommend you look through some of the example chapters, as they demonstrate some of the capabilities of using `bookdown` to write your thesis. You can also see more functionality of the `bookdown` package [here](https://bookdown.org/)

You can see how other components of the `dragondown` template works by reading through the [Components](https://github.com/tbradley1013/dragondown#components) section of the GitHub README. You can see what the final product of the `dragondown` project looks like for the example thesis used in the template looks like [here](/dragondown_book/thesis.pdf).

### Thesis/Dissertation Approval Form
One important feature unique to the `dragondown` template, is the ability to include the required [thesis/dissertation approval form](https://drexel.edu/~/media/Files/graduatecollege/forms/Graduate%20Thesis-Dissertation%20Approval%20Form%20and%20Signature%20Page.ashx?la=en). This form is for your committee members to sign that they have approved of your thesis. In the original `drexel-thesis` LaTeX class, this page was created in pure LaTeX. However, the form as been updated since its implementation and unfortunately, I am not a LaTeX expert. So in this project, the approval form is added using a saved version of the form from the `docs` folder of your thesis project. When you create a new thesis project, a blank approval form is used. However, you can replace the existing form with a filled out form if you wish. If you decide to do this, you can use the existing file name or you can specify a new name. Please note, that if you use a different file name, you will need to specify the file location in your `index.Rmd` file using the `approvalform` YAML parameter:

```
approvalform: path/to/form.pdf
```

If you wish to exlude the approval form from your thesis rendering, you will need to open the `template.tex` file and remove the `approvalform` option from the `\documentclass` option on the first line. 

## Why should you use `dragondown`?

Writing your thesis/dissertation is hard enough, and worrying about the formatting and how to integrate your results with your text can make it that much more difficult. Inspired by other examples, the `dragondown` package will allow you to create a Rmarkdown book that conforms to the requirements given in the [Drexel Thesis Manual](https://drexel.edu/~/media/Files/graduatecollege/forms/Thesis%20Manual.ashx?la=en). There are three main reasons why you should want to use this package to create your thesis/dissertation:

  1. Easily integrate your text with your analyses
  2. Avoid having to work in raw LaTeX to include tables and figures in a clean format
  3. REPRODUCIBILITY!!
  
### 1. Easily integrate your text with your analyses. 

R and Rmarkdown allows you to easily integrate text and your analyses (in the form of R, python, or SQL code). The `dragondown` package then provides the required templates so that when your knit your Rmarkdown (in this case a [`bookdown`](https://bookdown.org/)) project it will conform to Drexel's various requirements for the formatting of a thesis/dissertation. This is incredibly powerful, and can save you a lot of time when you are trying to put the finishing touches on your project. Instead of having to spend a crazy amount of time making sure that every figure and table meets the right requirements and your front matter and back matter all meet the requirements, the `dragondwon` package takes care of that for you. This will allow you to spend your time on what you really care about, your work! 

For example, let's pretend that you have a data set named `diamonds.csv` (credit to the [`ggplot2`](https://ggplot2.tidyverse.org/)) package. You can easily load it in your Rmarkdown file directly with your text in a code chunk like below:


```r
library(dplyr)
library(readr)

diamonds <- read_csv("dragondown-files/diamonds.csv")

diamonds
```

```
## # A tibble: 53,940 x 10
##    carat cut       color clarity depth table price     x     y     z
##    <dbl> <chr>     <chr> <chr>   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
##  2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
##  3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
##  4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
##  5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
##  6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
##  7 0.24  Very Good I     VVS1     62.3    57   336  3.95  3.98  2.47
##  8 0.26  Very Good H     SI1      61.9    55   337  4.07  4.11  2.53
##  9 0.22  Fair      E     VS2      65.1    61   337  3.87  3.78  2.49
## 10 0.23  Very Good H     VS1      59.4    61   338  4     4.05  2.39
## # … with 53,930 more rows
```


Then you can include more code chunks that analyze the data set, create production quality table and figures, or anything else and they are easily integrated with your text. 

Are you a fan of python instead of R? No problem! With newer versions of RStudio and the [`reticulate`](https://rstudio.github.io/reticulate/) R package, you are able to [easily integrate python chunks directly into your Rmarkdown files](https://rstudio.github.io/reticulate/articles/r_markdown.html). 

### 2. Avoid having to work in raw LaTeX

Don't get me wrong, there are some people that LOVE LaTeX... but if we are honest, those people are likely few and far between. From the people I have spoken too, the knowledge that has been past down for using LaTeX to create the required formatting for Drexel's dissertations is something that gets lost between generations of grad students. Luckily, thanks to the work of several former students in the Physics department (namely [W. Trevor King](https://github.com/wking)), there is a [drexel-thesis LaTeX class](https://github.com/DrexelPhysics/drexel-thesis). Now, you could certainly go about building this class on your local machine and writing your thesis in LaTeX, but you will still have to worry about organization and actually using LaTeX. The `dragondown` package includes a slightly modified of the `.cls` class file from `drexel-thesis` and a LaTeX template that allows you to completely avoid LaTeX if you want. 

Just like in any Rmarkdown file being knit to a pdf, you can certainly add your own LaTeX on top of the template, but you only have to do this if you want! You can also modify the template yourself once you create your `dragondown` project. 

### 3. REPRODUCIBILITY

I am including this last, but in all honesty, this is by far the most important reason for why you should switch to using `dragondown` for your thesis. Using this package, or more specifically, R (or python) and Rmarkdown, will allow you to create a completely reproducible workflow!

What does this mean? Simple, you can press one button and your whole dissertation is regenerated with any changes that you may have made. 

**Did you find a mistake in your data?** No problem (assuming your conclusions didn't change, of course)! You can make the change and simply re-knit your dissertation and all of your results, tables, and figures will be completely re-rendered without you having to go through the painful process of remaking them all one by one and then copying and pasting them back into your manuscript!

**Did you decide you want to rearrange your chapters?** No Problem!! Simply edit your `_bookdown.yml` file to put them in the order that you want and re-knit!

In addition to the benefits that reproducibility provides for yourself, it also makes it so that you can easily share your work with others and they will be able to reproduce your results by simply compiling your thesis. This allows for more transparency in science, which is always a good thing!


## Conclusion

This package was generated to try and make the life of graduate students at Drexel University a little bit easier. While this package will not perform your research or write your thesis, hopefully it will allow you to not worry about the tedious task of meeting formatting guidelines and focus on the work you care about! If you have any questions and you find any issues with the package, feel free to file an issue at the [GitHub repo](https://github.com/tbradley1013/dragondown/issues). 

I would like to thank both W. Trevor King and his collaborators for their work on the `drexel-thesis` LaTeX class, as without that, this project would not have happened. I would also like to thank Yihui Xie for creating `Rmarkdown` and `bookdown` and Chester Ismay for the creation of `thesisdown`, which this package is largely based on. Without all of this work, the `dragondown` project would not exist, so thank you!
