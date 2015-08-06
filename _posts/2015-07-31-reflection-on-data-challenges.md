---
layout: post
title: Reflection on Data Challenges
permalink: reflection-on-data-challenges
---

I've done 3 data challenges so far for Data Science/Analyst positions in the past few weeks. Below are a few things I've learned from experience; I hope they can be of help to others who are starting the data science interview process:

- **Start early.** Even if the main task/prompt doesn't seem that challenging, reading in the data and cleaning up the data may take a long time, especially if the format is unfamiliar or the file size is large. 
- **Code matters...** This may be kind of obvious, but you're being judged on the quality of your code as well as the depth/originality of your analysis. This means - comments where necessary, watch the number of temp variables you use, wrap commands you use repeatedly into functions, be aware of efficiency...etc. Even though the code that you write won't be reused, it's still important to write it as if it were going to be. Plus, clean code helps with debugging. 
- **...and so does the presentation.** Again, might be obvious. I do data cleanup/processing in Python, and then analysis with R in [RStudio](https://www.rstudio.com/) (I had used RGUI for the longest time but finally made the switch to RStudio...it's so much better). I use [knitr](http://yihui.name/knitr/) to turn my R code into a report. 
- **Have a plan/timeline.** For me, I sometimes get overexcited about certain packages or concepts that I encounter along the way, but really do not have much to do with the challenge itself, so I have to force myself to not get sidetracked. You will generally be given about a week for the assignment, and although that seems like a lot, you still have to be disciplined and treat it like a timed assignment. 
- **Test functions.** Unit tests are pretty important to writing quality, bug-free code. I think developers know this, but I don't think this is really stressed for data scientists. Doing so does take extra time, and your potential employer won't see the effort you put into building your test suite, but it ensures the accuracy of your analysis. A naive analysis is still better than getting the wrong results, no matter how elegant the analysis procedures are. 

Overall, I think practice is the best way to get better. I wasn't able to clear those data challenge rounds, so I took the last few weeks to improve. I recently redid one of the data challenges I sent in about a month ago and the differences in terms of accuracy, quality/efficiency, and readability between the one I submitted and [the redo](https://github.com/melodyyin/etc/blob/master/xdcp.md) were startling. 

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin@u.northwestern.edu. Thank you!</p>