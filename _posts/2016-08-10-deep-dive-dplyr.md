---
layout: post
title: Deep Dive dplyr
permalink: deep-dive-dplyr
---

dplyr is my most used R package, so I'm very familiar with the common verbs like `group_by`, `summarise`, `mutate`, `join`, `rename`, `dplyr::select`...etc. These functions have been tremendously valuable to me as an analyst, so I decided to take a closer look at its features to see if there's any useful functions I don't yet know about! 

And here are ones I'll definitely be adding to the toolbox: 

* `min_rank`, `top_n` - Previously, if I had wanted to extract the top `x` rows, I had just used `arrange` and `filter`ed on the rows with `row_number`. This worked fine when I didn't need to handle ties, but dplyr and base R also has additional ranking functions when you do need to. You can use `min_rank` when you want to display all tied rows, and you can use the parameter within base R's `rank` function to get even more granular. Similarly, `top_n` returns rows using `min_rank`. 

* `cume_dist` - Now that I think about it, dividing each row's `cumsum` with the group's total sum is quite awkward. I like that with this function you can quickly grab rows that hold the top/bottom `x`% of some value. 

* `order_by` - Essentially the same thing as `arrange`, but you're able to perform actions that require sorted rows without actually sorting. 

* `cumany`, `cumall` - Again, these are functions that are dependent on sorting. With `cumany`, you're able to grab the first row where a given condition is true as well as the rest that come after it and with `cumall`, you're able to keep grabbing rows as long as they satisfy the condition. They are sort of like OR and AND because `cumany` keeps on looking for that first T whereas `cumall` gives up after seeing the first F. 

* `intersect`, `union`, `setdiff` - I've mainly relied on using base R's `%in%` and `which` for my set operations, which works but gets a bit wordy, so I'm happy to see substitutes in dplyr. Also worth mentioning is base R's `setequal`, which compares the equality of the values in 2 vectors (what's the alternative? ``all(x %in% y)`?) Something to note is that `setdiff(x,y)` is not the same as `setdiff(y, x)`.

* `distinct` - Didn't know this function existed! This way avoids the awkward `ungroup` that would need to happen with my original method, which was to `group_by` then `filter`ing on `row_number`. 

* `do` - *THIS FUNCTION!!!* I'm pretty sure I was just subsetting and writing a lot of duplicate code to deal with each df partition previously. This function allows you to apply actions to each group and outputs the results to a data frame. The grouping remains after this call so you can extract the needed components afterwards. Gamechanger.

* `last` - More succinct way of selecting the last element by `length`

* `case_when` - More succint way of doing multiple if-else statements (odd syntax)


Here are the resources I used: 

* [Window Functions](https://cran.r-project.org/web/packages/dplyr/vignettes/window-functions.html)
* [Two-Table Verbs](https://cran.r-project.org/web/packages/dplyr/vignettes/two-table.html)
* [dplyr reference manual](https://cran.r-project.org/web/packages/dplyr/dplyr.pdf)

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin18@gmail.com. Thank you!</p>