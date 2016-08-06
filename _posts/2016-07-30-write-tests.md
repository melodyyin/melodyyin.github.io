---
layout: post
title: Write Tests!
permalink: write-tests
---

In the second quarter of my Master's program, I had a professor who _really_ emphasized the importance of writing modular code and testing each function that you write. The way he graded our weekly assignments was by running each function with every type of input your function should be able to handle. So, it was in our best interests to make sure that every branch of our functions worked correctly. As a result, [I wrote a lot of tests](https://github.com/melodyyin/coursework/blob/master/basics.rkt). 

After his class ended, I often thought about writing test statements, but doing so was never required again in any of my other classes, and from the lack of online literature surrounding testing for data science, I had just assumed that it wasn't something data scientists do. Sure, I would casually test the output of functions at the console after writing them to ensure they worked as expected, and I would throw in `stopifnot` statements on occasion, but I had never been disciplined about it. Until now. 

Since the compatibility quiz was fresh on my mind, I decided to supplement tests for this short script using the [testthat](https://cran.r-project.org/web/packages/testthat/index.html) package. I used [this guide](https://journal.r-project.org/archive/2011-1/RJournal_2011-1_Wickham.pdf) to get started, and I used [the tests he wrote for dplyr](https://github.com/hadley/dplyr/tree/master/tests/testthat) as another reference. 

The recommended style is to not have all of your tests in one test file, but since my script was pretty short, I felt it was fine to do. The workflow that I am going to start trying out is to write tests in separate tabs as I am working on the actual code for the analysis/model. The test file is just composed of a series of related `test_that` statements. For example, here is one of my test statements:  

{% highlight r %}
test_that("to_sentiment_score returns the correct word count", {
  expect_is(to_sentiment_score("something"), "integer")
  expect_equal(to_sentiment_score("something or another"), 3)
  expect_equal(to_sentiment_score(NA), -1)
})
{% endhighlight %}

I saved this in a folder called `tests` (make sure to start the name your file with `test`) and I run all of my test statements using `test_dir("tests/")`. That's all! Super simple to get going. 

While I was creating the test suite, I noticed that I had already written a few error messages within my functions. I think it's worthwhile to have both - one as an intermediate check and one to as a final check on the output. Also, for a few of the statements, I felt they were kind of redundant as I was writing them, especially since I had already seen the result. However, then I realized that testing is not just to guarantee the accuracy of your code _at the time_, but it's also to ensure your future changes don't affect the integrity of your results. 

All in all, I'm surprised that testing is not more recommended in data science, especially since errors are just as, if not more likely, to creep up when dealing with numbers in this field than in engineering, where testing is an integral part of development. I wish I could go back in time and tell my past self to do this, but since that's impossible, I hope this post has encouraged you to get started with testing! 

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin18@gmail.com. Thank you!</p>