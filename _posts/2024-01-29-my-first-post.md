---
title: Napoleon's March to Moscow in Power BI (via Vega-Lite)
date: 2024-01-29
tags: [PowerBI, Vega-Lite, Minard]
image:
  path: /assets/post_files/Napoleons_March/post_thumbnail.png
---

# This is my first post!

If you just want to skip ahead and download the Power BI file, [here it is](/assets/post_files/Napoleons_March/Napoleons_March_PBI_Vega-Lite.pbix).  

If you care about what I have to say please proceed:

I have thought about starting a data analysis blog for years, and never gotten around to it.  Currently I am doing an independent study in data visualization at the University of Miami which has two requirements (among others):
  - Start a data visualization blog (you are here)
  - Learn something new
	
So here's where the rubber hits the rode I suppose!

## Learning Something New
To cover the learn something new requirement I've decided to focus on learning the Vega and Vega-Lite languages, which are abstractions on top of D3.js, allowing users to use a declarative language.  As a primarily Power BI user, I've had Tableau envy for years over the more flexible and custom way Tableau visuals can be built.  Power BI has its advantages though, and since the release of the Deneb visual which allows embedding Vega visuals I've been seeing more and more development of some amazing visuals in Power BI using the Deneb visual and Vega language.

## Why not ggplot?
Power BI has had the ability to display ggplot visuals for years now, but as far as I currently know, to display tool tips and allow interaction ggplot visuals require development as actual custom visuals that need to be imported.  With the Deneb visual the interaction and tooltips only need to be declared in Vega.  I will admit that though, when comparing the 100+ lines of code I had to write to create the graphic in this post, to the 15 or so lines ggplot needed to produce comparable graphics, I had thoughts of starting over.  The JSON structure is not nearly as friendly as ggplot's syntax as well.  I'm hard-headed though, and really admire some of the work I've seen done in Vega.  Maybe this will be my gateway drug to D3.

## Inspiration 
I'm currently reading the Visual Display of Quantitative Information by Edward Tufte, more on that another time, but among the first few pages Tufte sings the praises of Charles Joseph Minard's figurative map of Napoleon's Invasion of Russia.  I've always had enjoyed looking at maps, add a time-series on it and now you've got my attention:

![Minards Original1](/assets/post_files/Napoleons_March/minard_original.png "Minards Original2")


After searching the around the interwebs I even found a ['contest'](https://www.datavis.ca/gallery/re-minard.php)
 to re-vision this classic graphic.  Since I didn't see any entry using Vega, I decided that this might be a great way to get my feet wet with the language.



## Connected Scatter
A great place to start for creating visuals is the [Vega examples gallery](https://vega.github.io/vega-lite/examples/).  Though I should have known better, scrolling through the examples my first thought on tackling this challenge was to use a connected scatter plot: 

![CS1](/assets/post_files/Napoleons_March/connected_scatter.png "CS2")


## Trail Mark
Looking at the connected scatter, we are obviously not encoding for the number of soldiers variable.  Reviewing some of the revisioning Minard contest entries (specifically the ggplot entry) I realized I needed something akin to the path mark, Vega has this but calls it a trail mark:

![TR1](/assets/post_files/Napoleons_March/trail_mark.png "TR2")



## Adding the Map 
Unfortunately Power BI does not allow Deneb to connect to any external data sources, which makes maps a bit more challenging.  Browsing the Vega galleries, you can see that the topojson file for a US map is simply linked.  Thanks to [David Bacci's Covid Map](https://github.com/PBI-David/Deneb-Showcase/tree/main/Covid%20Map) I was able to figure out the the topojson needs to be added in line.  

![tpjsn](/assets/post_files/Napoleons_March/topojson_link.png "tpjs")

Navigating to https://vega.github.io/vega/data/world-110m.json I was able to find the appropriate topojson for the project.

and add it in line to my code:

![tpjsnl](/assets/post_files/Napoleons_March/topojson_inline.png "tpjsl")

resulting in a time series overlaid on a map!

![mr](/assets/post_files/Napoleons_March/map_result.png "mr")


## Refining

One feature I wanted my version of this map to have, was the troop counts in addition to the city names.

Adding two different text marks looks like this:

![dstm](/assets/post_files/Napoleons_March/display_survivors_too_many.png "dstm")

Too cluttered!  Since this is a Power BI and Vega Lite project I decided to use Power Query to come up with a solution.

The original troop count data series actually includes three distinct groups that joined together. I decided that I would try to show a text mark for at least the first data point for each group and others in a predetermined interval.

I created a group index in power query using the group by feature.

![gpid](/assets/post_files/Napoleons_March/group_index.png "gpid")

and then created a calculated column (this could have also been a DAX measure) to return the first data point for each group and then each 6 using the modulo operator.

![dsf](/assets/post_files/Napoleons_March/display_survivors_formula.png "dsf")

Passing this column to the dataset which Deneb uses, resulted in the graphic at the top of this page.

There is still some crowding around city names and survivor text marks which I would like to solve in a future update.

Country names are text boxes which I manually arranged.

## Degré Celsius and City Names
For now  I will be skipping over this portion of the graphic, unfortunately at this time I cannot find a way for Power BI to allow multiple data sources be passed to Deneb.  Given that this graphic is actually composed of three datasets: troop levels, temperatures, and city coordinates I had to hard code the city coordinates in the first graphic, and the temperature chart is a second visual which I lined up with the first.  I do believe it would be possible to combine all three datasets into a super data set and filter data at the mark level, however I'm not sure the juice would be worth the squeeze in this case.



