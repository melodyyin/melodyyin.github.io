---
layout: post
title: Patient Activity Detection Using Kinect for Windows v2 (part 2)
permalink: patient-activity-detection-using-kinect-2
---
This is the second part of my review on the patient tracking system project. You can read part one [here](/patient-activity-detection-using-kinect). 

At the end of my eight weeks working on the project, I spoke with the postdoc and professor about returning in the following academic quarter, and they agreed! So, after spring break, I resumed my position in the lab. 

###Due diligence
Much like working in a startup, working on a project solo has its perks as well as issues. In the first eight weeks, I enjoyed the flexibility and autonomy it allowed. However, after I returned to the project, I felt the weight of having to do everything myself when a lot of the less stimulating work needed to be done. An additional Kinect sensor was added, so now there were suddenly twice as many clips to label. Additionally, I encountered problems with VGB that wiped out hours of work; at one point, building the database failed repeatedly due to memory overflow. These problems were really frustrating because they were not *at all* difficult, but were extremely time-consuming to fix. 

Around this time, the postdoc also suggested that I should be implementing robustness checks. As in, we knew that the angle and height of the sensor affected results somewhat, but we didn't know how much. Without going into too much detail, I found that setting the Kinect at different configurations had a dramatic effect on accuracy rate. However, the database which contained all of the clips as well as the database with the testing clip's configuration had similar performances. 

###MLE vs. MAP
The sample code had originally returned all of the activities with a confidence value greater than 0 for each frame. In other words, it was highly likely that each frame was labelled with multiple gestures and start/end times overlapped. This didn't make sense for my purposes, since all of the gestures I was working with were distinct. So, I changed the code to reflect a maximum likelihood estimation (MLE) approach by finding the gesture with the greatest confidence level per frame and attaching the result to the frame if the confidence exceeded the threshold. Then, I started to think about how I could extend this further. I knew that although finding the optimal thresholds would increase the accuracy, they would need to be readjusted once new training clips were added. But, I realized that there were some gestures that could not be in sequence. For example, a person has to get into the bed before he/she moves around in the bed. Disallowing moving in bed to be triggered unless the previous gesture was itself, laying in bed or getting into bed seemed like a good idea until the professor advised that the Kinect may not be turned on all the time (e.g., the first gesture may actually be Moving in Bed). However, even though absolute restrictions could not be applied, I could still make probabilistic assumptions about the gesture sequence. That is, there are plenty of claims I could make for `P(next gesture|current gesture)`. 

This realization led to the creation of a transition matrix. At first, I tried assigning probabilities to each gesture so that `P(ALL GESTURES|current gesture)` would sum up to one. After I implemented this, I realized that now using one threshold for all gestures did not produce the expected results. Then, I tried penalizing only the gestures that were unlikely, and this approach seemed to work well. So, I set up three "bins": one for likely gestures, one for probable and one for impossible. Those in the likely bin receive no penalty and are triggered when their confidence values exceed the threshold. Gestures in the probable category get a 50% penalty, so their confidence values have to be `2*threshold` to be triggered. Lastly, the impossible gestures have to exhibit a confidence value of `~4*threshold` to be triggered; the reason that they were not eliminated completely is due to the possibility that the previous gesture was mislabelled. 

To summarize, here is an example of what the transition matrix looked like:

|    | G1   | G2  | G3   | ...  |
|----|------|-----|------|------|
| G1 | 1    | 0.5 | 0.23 | ...  |
| G2 | 0.5  | 1   | 0.5  | ...  |
| G3 | 0.23 | 1   | 1    | ...  |
| ... | ... | ... | ...  | ...  |

Depending on the previous and current gesture, the appropriate transition value was applied to the raw confidence value. Since there is no reason to expect one gesture over any other to be the first in the sequence, MLE is used when the previous gesture has not been defined. Unlike thresholds, the transition values remain the same even after new training clips are added. 

###Results 
This approach gave pretty good results, and outperformed MLE because it dramatically reduced the number of false positives. Previously, there had been some noise in the detection results. For example, if a gesture lasted 50 frames, while the majority would be tagged as the correct gesture, a few of those were incorrect. A common pattern I observed before the transitions were implemented was Sit, Moving in Bed, Sit, Moving in Bed,...etc. Implementing transitions eliminated these types of errors. 

However, when a frame was mislabeled, this affected all of the following classifications. The wrong gesture could block all of the (correct) labels that the detector tries to make, because they would be penalized by the transitions. To counter this effect, I allowed the gesture sequence to restart if no activity had been detected for a certain number of frames. This helped to restore the correct state after a mistake had been made. Here is an example of how this works: 

- Before: G1, ___ , ___ , ___ , ___ , ... 
- Ground truth: G2, G3, G2, G3, G2, G3
- After: G1, ___ , ___ , ___ , G2, G3

Finally, the detector was evaluated on various testing clips. Solid results were achieved across the entire gesture database, and both the precision and recall for all gestures were much higher than they were when I turned in the project report last quarter. Notably, lifts, walking and bed movements had near-perfect performance. Sit and fall were satisfactory, with ~80% precision and ~70% recall. Getting into bed and out of bed did not perform as well. When I looked at the raw confidence levels for the sequence of frames where these two gestures were occurring, I saw that either the confidence was very low or the gestures were not triggered at all. This result suggests that these two gesture databases are insufficient, so it's possible that the range of training examples was too limited.

###Discussion
Although VGB is a great solution for those who want to use the Kinect for gesture recognition, a major disadvantage of the tool is that it doesn't allow features to be extracted. VGB calculates 38 different features from the training clips, but the developer is not able to access these values or the coefficients for the predictors. It does show what the features are, and which ones are the top contributors to the final gesture classifier, but not much more detail is provided. Therefore, adding additional training clips or applying post hoc methods is really the only way to get better results. I would have liked to compare performances of various learning algorithms against AdaBoost, VGB's default, if not for any accuracy gains then for my own learning purposes. The postdoc and I did spend a few hours going through the AdaBoost algorithm to make sure we fully understood (or at least, had a good guess for) what was going on behind the scenes, but having some official documentation would have been appreciated. 

Looking back on the project from the finish line, I feel a lot of gratitute towards the professor and postdoc who worked with me, and I also feel proud of the work I have done. I do wish I could have spent more time developing the interface in the second round, but improving the accuracy was more important. This project was truly one of the highlights of the past year I spent as a graduate student, and I am excited about the possibility of making more contributions in the healthcare field in the not-too-distant future! 

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin@u.northwestern.edu. Thank you!</p>