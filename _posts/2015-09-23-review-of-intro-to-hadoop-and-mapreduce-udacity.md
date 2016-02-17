---
layout: post
title: Review of Intro to Hadoop and MapReduce (Udacity)
permalink: review-of-intro-to-hadoop-and-mapreduce-udacity
---

Last night, I finished the final lesson of Udacity's [Hadoop/MapReduce course](https://www.udacity.com/course/intro-to-hadoop-and-mapreduce--ud617), built by Cloudera. This is the second Udacity course I have completed; the other one was [Intro to A/B Testing](https://www.udacity.com/course/ab-testing--ud257), created in collaboration with Google. 

## Overview
The course took me about five days to complete (note: I did not do the final project). The first 2 lessons are lectures that go over the basics of Big Data, HDFS and the MapReduce framework. Each lesson contained short quizzes as you go through the videos as well as a "Problem Set", which is a longer quiz reviewing the corresponding lesson's materials. Since I had zero knowledge of the Hadoop ecosystem, I learned a lot from this simple intro.  

Lesson 3 was about writing mappers and reducers. Cloudera provides a pseudo-distributed environment where you can run your code as well as the ability to code in Python instead of Java through Hadoop Streaming. The Project for this lesson contains 6 problems you will have to run on your virtual machine; starter code is provided. This part took me a few hours, but helped me to better understand how MapReduce works. Lesson 4 introduced filtering, summarization and structural design patterns as well as combiners, which can serve as an intermediate step between the mapper and reducer to reduce processing time. No project in this lesson, but there were 6 tasks that applied the patterns mentioned. 

## My Thoughts
All in all, I enjoyed taking the course and it was a good primer to working with Hadoop. Writing MapReduce code and testing on real(ish) datasets was a great learning experience. The only problem, which I observed in the A/B Testing course as well, is the vague/sometimes misleading directions and the lack of feedback for free users. Of course, one can't expect much (/any) support since the materials are already free, but the combination can cause a bit of frustration sometimes. For example, one of the problems asked for "the mean value of sales on Sunday", but what it actually wanted was the mean purchase value of a sale made on a Sunday. Also, I was about 2/3 of the way done with the A/B Testing final project, but there was this one question that did not accept any reasonable answers. This is why I chose not to spend time completing the final project for this course. 

There is a discussion board that people can ask questions, and I've used this a few times to help me decipher unclear directions, but the participation is *really* low. The front page of the Hadoop course boasts more than 80k students, but most of the discussion board posts only have around 100 views. This makes me wonder what the student engagement level is for these courses. 

## TLDR;
**Worth taking if...** you are completely new to Hadoop and/or writing MapReduce code  
**You will learn...** basics of HDFS and MapReduce framework, data processing in Python, working with the Linux command line  
**I recommend...** checking for syntax errors locally before running a job to save time

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin@u.northwestern.edu. Thank you!</p>