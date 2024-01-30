---
title: Napoleon's March to Moscow in Power BI (via Vega-Lite)
date: 2024-01-29
tags: [Python, PowerBI, Vega-Lite, Minard]
image:
  path: /assets/post_files/Napoleons_March/post_thumbnail.png
---

# This is my first post!

If you just want to skip ahead and download the Power BI file, [download the file here](/assets/post_files/Napoleons_March/Napoleons_March_PBI_Vega-Lite.pbix).  

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
Though I should have known better, scrolling through the [Vega examples gallery](https://vega.github.io/vega-lite/examples/) my first thought on tackling this challenge would be to use a connected scatter plot: 

![CS1](/assets/post_files/Napoleons_March/connected_scatter.png "CS2")



## Trail Mark
Looking at the connected scatter, we are obviously not encoding for the number of soldiers variable.  Reviewing some of the revisioning Minard contest entries (specifically the ggplot entry) I realized I needed something akin to the path mark, Vega has this but calls it a trail mark:

![TR1](/assets/post_files/Napoleons_March/trail_mark.png "TR2")



## Adding the Map 
Thanks to [David Bacci's Covid Map](https://github.com/PBI-David/Deneb-Showcase/tree/main/Covid%20Map) I was able to figure out the the topojson needs to be commented in line.


## Refining

To be expanded upon later, I used formulas within Power BI to change the frequency with which the number of survivors would display.

