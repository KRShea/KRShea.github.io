---
title: (Making of) An Interactive History and Demographic Analysis of Costco
date: 2024-04-30
tags: [PowerBI, Vega, Python, Costco]
published: true
##image:
##path: https://krshea.github.io/assets/post_files/costco_analysis/post_thumbnail.png
---


## Introduction

The right tool should be used for the job.  When I started working on my Costco article and visual demographic analysis, I knew that Power BI and Vega would not be the best choice for what I wanted to do which was create a fully interactive scrollable infographic.  The demographic analysis page alone displays somewhere around 16,000 selectable data points and attempting to have everything on a single page simply overloaded Power BI.   

This project was very experimental and I really didn’t know how well everything would work out when I first started. If I could go back would I do it in Power BI again?  Yes, but only because of everything I've learned.  I feel like I leveled up my visualization skills 5 times while working on this project, I also learned a few new things in Power BI.  

My personal Power BI Pro license is costing me $10 a month though which I need to publish the report to web, a small sum, but if I had produced this 100% in Vega and html/css while hosting the data on github I'd pay nothing out of pocket.  Alternately if I had used Tableau public, I'd also be paying nothing out of pocket, though I am not sure everything I've done can be accomplished in Tableau.  Microsoft should really offer something similar to Tableau Public.

I could probably write a book about everything I've learned about Vega, Power BI (and Costco) over the last 4 months.  This article will touch on the creation of the key visuals and a few Power Bi techniques used in my Costco article and visual demographic analysis.


## Interactive globe

I have previously written about my inspiration to create this visualization which was a graphic from the Economist:


![image1](./assets/post_files/costco_making_of/image1.png)

I hypothesized that given Costco's international growth in Asia and Europe the center of gravity of all stores would move off the North American continent sometime in the 2010s.  Disappointingly it never does!  I really wanted to do something similar to the Economist so I adjusted my strategy to show the center of gravity of new stores only and a trail of the prior three years.  Unfortunately this too resulted in a line that only leaves the United States twice.  With a graphic focused on the world I feel that seeing a line bounce around the US for almost 50 years isn't the most interesting thing, but given the sunk cost of nights and weekend I worked on this I decided to leave it in.  Everything in this report is defined with easily updatable data pipelines so perhaps in a few years I'll get my wish for a line that traverses more countries.


![image2](./assets/post_files/costco_making_of/image2.png){:width="600px"}


Calculating the geocenters using world store data:

![image3](./assets/post_files/costco_making_of/image3.png){:width="600px"}



![image4](./assets/post_files/costco_making_of/image4.png){:width="600px"}



Two challenges I faced in producing this globe were 
- Forcing the globe to autorotate to predefined points of interest
- Store symbols being visible through the other side of the map

I was very dedicated to the idea of keeping this graphic as a globe rather than a world map, I simply like the aesthetic more, one issue that I ran into though was that for example when Costco's first European location opens I wanted the map to display Europe automatically.  As it turns out this was no easy feat.  I thought simply creating a table with predefined rotation parameters and passing those as signals would work.  Doing this caused a circular logic error in Vega however; creating a map projection with data from the dataset and plotting that data on the map just doesn't work.  After trying one hundred things that didn't work I figured out how to use an event to update the map rotation after creating the map.  The event in this case is based on a timer.  One millisecond after producing the map, the rotation is updated from my dataset.

![image5](./assets/post_files/costco_making_of/image5.png){:width="400px"}




The other challenge I faced in creating this map was that store locations were visible on the other side of the world when rotating the map.  

An example of North American stores appearing in the North Pole when rotating the map:
![image6](./assets/post_files/costco_making_of/image6.png){:width="600px"}



Shout out to my LinkedIn connection and Vega guru Andrzej Leszkiewicz for helping with the solution!  I encoded the opacity to be a function of the map rotation parameter.  If the points are not within 180 degrees of the rotation parameter they will be invisible.  Note that if I had brought the data in as geojson this step would not be necessary, but it seems that in Power BI/Deneb, this is not possible.
![image7](./assets/post_files/costco_making_of/image7.png){:width="400px"}



Auto rotation in action as seen in 1995:
![image8](./assets/post_files/costco_making_of/image8.png){:width="600px"}



## Costco score map

I have an entire blog post dedicated to my process for creating a choropleth map with points on it, so rather than rehash that I will be discussing some of my data gathering for making the Costco score map and the 

Map highlighting counties without Costco or Sam's Club and hovering over high "Costco score" Teton county:
![image9](./assets/post_files/costco_making_of/image9.png){:width="800px"}


Data used to create this map came from the US census API (this data is also used in the jitter charts in this project):
![image10](./assets/post_files/costco_making_of/image10.png){:width="600px"}


Using the data from the census (and Costco location data which I described reverse geocoding in another blog post) I created a logistic regression model to forecast a counties suitability (probability) for getting a Costco.  Given that there are hundreds of counties that would be suitable for a location but don't have one yet I used SMOTE (synthetic minority oversampling) to balance my dataset:
![image11](./assets/post_files/costco_making_of/image11.png){:width="600px"}

Model results:
<br>
![image12](./assets/post_files/costco_making_of/image12.png){:width="400px"}


One issue that I ran into when producing the map is that Connecticut recently redistributed all of their counties into "planning" regions.  The relationship of old counties to new planning areas is not one to one.  My topojson (map) file had the old county names while the latest census utilized the new planning areas.  In order to marry the two datasets I created mapping tables for each to the other, and using bi-directional cross filtering and an intermediate table I was able to fill Connecticut in my map with data from the Census.

See the crosswalk tables below:
![image13](./assets/post_files/costco_making_of/image13.png){:width="600px"}




## Jitter charts with median

What I am calling jitter charts went through multiple iterations to arrive at the charts seen below.  Though I am happy with the result, I believe that there is still room for improvement on color scheming and creating the spacing for the variables which require plotting on a log axis.

I wanted to take full advantage of Vega and Deneb's interaction capabilities in this project. Users can hover over any point any see what county they are looking at with a tool tip.  When investigating an outlier a click on the point will highlight it on the other charts as seen below.  This interaction carries over to the entire report.  Clicking a county on the map will high light it on the scatter charts and vice versa:
![image14](./assets/post_files/costco_making_of/image14.png){:width="600px"}


I was also able to make the legend interactive.  Clicking on one of the market groups highlights the associated points:
<br>
![image15](./assets/post_files/costco_making_of/image15.png){:width="600px"}


In Power BI core visuals cross-highlighting happens behind the scenes, in Deneb the hightlightStatus is made available to the user (note that Power BI core scatterplots do not support cross-highlighting at the time of this post).
<br>
![image16](./assets/post_files/costco_making_of/image16.png){:width="600px"}



Cross highlighting requires two layers and some conditional logic.  

Below is the base symbol layer, this layer has an opacity of just 10% as it provides a background image when other items are selected.  Note also that in "y" I am using a signal from the dataset to determine whether or not to plot on a log scale or linear scale this is based on user selection of variables:
![image17](./assets/post_files/costco_making_of/image17.png){:width="400px"}


Selected symbol layer (if an item is selected or highlighted by Power BI the opacity will increase as well as the stroke width):
<br>
![image18](./assets/post_files/costco_making_of/image18.png){:width="400px"}





My original attempt at creating the jitter charts was using a beeswarm chart template created by Kerry Kolosko.  I normalized all of the data between one and zero and plotted a sample of counties.  The math used to create beeswarm charts is somewhat complex and done inside the visual so once I unfiltered the data my computer crashed.

The second version I started on was using ggplot, this plotted every county in a split second, but unfortunately ggplot only creates static images so all of the interaction would have been lost.

In my third attempt I went back to the beeswarm idea, but I grouped similar counties together.  I thought it was a great idea at first, but the result looks clunky and some of the larger groupings are so big the displace other groups.

My fourth attempt is fairly close to my final version, at first I built these to look similar to sina plots.  In order to create these plots I preprocessed the data in python, calculating x offsets by data bins.  A snapshot of this code is included after the examples:

<table align="center" width="100%">
  <tr>
    <td style="text-align: center;">
      <img src="./assets/post_files/costco_making_of/jitter_attempt1.png" width="150" height="350" alt="Beeswarm First Attempt" />
      <br>
      <figcaption>Beeswarm First Attempt</figcaption>
    </td>
    <td style="text-align: center;">
      <img src="./assets/post_files/costco_making_of/jitter_attempt2.png" width="150" height="350" alt="GGPlot Version"/>
      <br>
      <figcaption>GGPlot Version</figcaption>
    </td>
    <td style="text-align: center;">
      <img src="./assets/post_files/costco_making_of/jitter_attempt3.png" width="150" height="350" alt="Clustered County Beeswarm"/>
      <br>
      <figcaption>Clustered County Beeswarm</figcaption>
    </td>
    <td style="text-align: center;">
      <img src="./assets/post_files/costco_making_of/jitter_attempt4.png" width="150" height="350" alt="Early Sina Style Version"/>
      <br>
      <figcaption>Early Sina Style Version</figcaption>
    </td>
  </tr>
</table>

Python code to create x offsets:
![jitter_py](./assets/post_files/costco_making_of/jitter_py.png){:width="600px"}








