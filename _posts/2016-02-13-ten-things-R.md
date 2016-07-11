---
layout: post
title: 10 Things I Wish I Knew Sooner About R
permalink: ten-things-R
---

**1. Use RStudio** I was introduced to R in a regression course in my junior year of college. The professor used RGUI, so that's what I used as well. I didn't hear about [RStudio](https://www.rstudio.com/products/rstudio/download/) until the following year in Statistical Computing - but being the skeptic I am, I thought it was just a bulkier version of RGUI. It stuns me to think that I went through nearly 2 years of being a useR (including an internship where my main tool was R) before I downloaded RStudio. There are so many advantages of RStudio I won't list them here, but if you haven't made the switch.... DO IT NOW!!! Their newest release (v0.99.879) also contains significant improvements! 

**2. Use knitr** I can't be the only one who was either (1) attaching raw R code along with my graphs and written reports, which I usually created in (gasp) Word or (2) copying and pasting screenshots of code in reports when the person reading it is liteRate. Not only were these reports ugly and a hassle to make, but they were difficult for people to read as well as for me to review. Thankfully, I now use [knitr](http://yihui.name/knitr/) to generate reports and presentations (using [ioslides](http://rmarkdown.rstudio.com/ioslides_presentation_format.html)), so those problems are no more! Additionally, writing reproducible code has made me a better analyst.

**3. Use dplyr** What was I doing before [dplyr](https://cran.r-project.org/web/packages/dplyr/index.html)? I load this package at the start of every script I write. I have the laptop sticker. Exploratory analysis is so much more efficient (and readable) using this package vs. the base functions. Every analyst needs to use this. 

**4. Use ggplot2 properly** I also have this laptop sticker. I have to admit, for the longest time I was just throwing ggplot code together and hoping for the best, making visualizing results much more troublesome than it really should have been. Reading [the docs](http://docs.ggplot2.org/current/) is super helpful, and I do think the authors tried to make things as straightforward as possible. A realization that helped me better understand the package is that it *works in layers*. Every function you `+` to the ggplot() call is another layer you are placing on your graph. 

4b. Incorporate [xkcd-style graphs](http://docs.ggplot2.org/current/) in reports! [This is why](https://www.chrisstucchio.com/blog/2014/why_xkcd_style_graphs_are_important.html). Also they're fun.

**5. How to select columns by name** Not sure if this is something I should've learned long ago, but I never knew how to select a column within a dataframe by the (string) name. I've always done `df$my_column` or `df[,col_position_of_my_column]`. Recently, I learned that you can also do `df[[str_name_of_my_column]]`. I feel better now. 

**6. Declare default parameters in functions** Pretty self-explanatory. I like that this keeps your code clean and helps debugging. For example: 

{% highlight r %}
some_function = function(train=training_set, test=testing_set, res=data.frame()) {
	# do something
	return(res)
}

# I call this normally 
x = some_function() 

# but I can also do this if I want to test on a subset of the training/testing set
x = some_function(training_subset, testing_subset) 
{% endhighlight %}

**7. Debug** Breakpoints are really useful when I know the general area where the bug is occurring and want to check out the relevant variables at that point in the code. I've also been adding `stopifnot` statements in scripts, and doing this has been tremendously helpful in helping me catch mistakes that would otherwise go undetected (well, that is, until my manager gets back to me... :)). At some point, I want to check out the [testthat](https://cran.r-project.org/web/packages/testthat/index.html) package too. 

**8. xapply functions, do.call** xapply becomes really important when working with large datasets, and they're much more concise than repeating code or writing loops. An useful application is calling `sapply(df, is.numeric)` when you want to find the numeric columns... very handy for cleaning training data with many predictors. I haven't had much practice working with `mapply` or `Map`, but they're in the toolbox... 

I think of `do.call` as the opposite of `lapply`. While `do.call` sends your list into the specified function, `lapply` distributes your function to each element in the list. 

**9. Dealing with NAs** The datasets provided in university courses are always cleaned, so you never really have to deal with missing values or do data integrity checks. However, these issues are almost always present in datasets you'd encounter in another setting. I now always use the `na` parameter (in the [readr](https://cran.r-project.org/web/packages/readr/index.html) package) when reading in data. I also use `anyNA` for doing quick checks and `replace_na` (in the [tidyr](https://cran.r-project.org/web/packages/tidyr/index.html) package) and `na.omit` for handling NAs. 

**10. Git locally** THIS IS AWESOME. I didn't know version control was possible without pushing to a public repo until recently. No more saving R files with the dates at the end... or scrolling through a script trying to remember which line I changed last week... The interface RStudio provides is actually super straightforward - it doesn't require any knowledge of git commands. All you need to do is check your files, write a commit message, and press a button! 

I consider myself proficient in R but there's still a lot for me to learn. Looking forward, I want to build a Shiny app, create a package, and become more involved in the useR community here in the Bay Area. I've definitely had my share of frustrations working with these tools/packages/functionalities, so to all the R beginners out there who were in my position: don't give up!!!

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin18@gmail.com. Thank you!</p>