---
layout: post
title: Solving Lyft's Programming Challenge with NetLogo 
permalink: solving-lyfts-programming-challenge-with-netlogo
---

Lyft seems like a great company to work for. I checked out their job listing section to see if there were any matches, but all available openings in the Analytics department as well as their Data Scientist role were for more experienced candidates. There was a SWE position for new grads, so I clicked out of curiosity. At the bottom of the page, was this: 

<p class="message">Programming Challenge (Optional)
	<br>Calculate the detour distance between two different rides. Given four latitude / longitude pairs, where driver one is traveling from point A to point B and driver two is traveling from point C to point D, write a function (in your language of choice) to calculate the shorter of the detour distances the drivers would need to take to pick-up and drop-off the other driver.</br>
</p>

A pretty vague prompt; but it piqued my interest. I envisioned two cars driving in my mind, and immediately thought that this would be the perfect opportunity to use [NetLogo](https://ccl.northwestern.edu/netlogo/).

##Basic Model
The setup was straightforward: two origin points with a car at each of them and two destination points. The origins and destinations were patches (different colored and with their corresponding label), and the cars were turtles. Originally, all of them were turtles, but I realized that would have been a poor design choice since only cars move. The locations were set using sliders. The agents could be easily instantiated using `set <varname> self` as they were being created. The shorter detour could simply be determined by `ask`ing for the `distancexy` from origin to destination. 

##Extensions
In my model, I made the driver not operating the vehicle into a person figure, and this rider "climbs in to the car" by staying invisible while traveling with the driver. The rider becomes visible again once he is dropped off. The driver also morphs into a person figure once he reaches his destination and both persons turn green to signal that the detour has been completed. Getting the direction of movement is as simple as calling `face <target>`. `patch-here` and `turtles-here` are useful for determining whether a location has been reached. 

Here is what the start and end views look like: 
![basic](/etc/basic.png)

At this point, I had answered the prompt Lyft provided, but I wasn't satisfied. It was wildly unrealistic that the cars could travel anywhere, so I decided to implement a grid system to mirror the view that users see when hailing a Lyft. Since the cars can travel on the grid only, the Euclidean distance measure had to be changed to Manhattan distance. Also, the direction that the car travels can only be 0 90 180 270 or 360. I enforced this rule by rounding up the desired direction (i.e., the direction of the next stop) to the nearest multiple of 90. To prevent the car from cutting across the restricted areas, I reset the direction each time the patch ahead is not part of the grid. 

Here is what the start and end views look like with the grid enabled: 
![grid](/etc/grid.png)

The model can be found [here](https://github.com/melodyyin/etc/blob/master/lyft.nlogo). I have also uploaded [a demo](https://youtu.be/LEJxTB6SG0g) for this model.

##Case for NetLogo
Even though the challenge could be solved using pretty much any language, NetLogo is the best fit since the traffic system builds upon the collective behaviors of individuals. The built-in patch and turtle agents allow classes to be instantiated quickly and functions to be called easily. And of course, the visualization component is pretty superb for debugging and for a stronger understanding of the system behavior! I had a lot of fun building and extending upon the prompt given. 

There are several additional extensions that can be applied to this model. All can be implemented within NetLogo. 

* Traffic signals and other cars on the road
* One-ways and dead-ends
* Driver gets picked up enroute (i.e., not at the start position)
* Driver preferences (e.g., prefer to go straight rather than make turns, prefer highways over local roads, prefer furthest route once passenger is picked up but shortest when going to his/her own destination)

<p class="message">If you have any feedback or questions for me, please shoot me an email at melodyyin@u.northwestern.edu. Thank you!</p>
