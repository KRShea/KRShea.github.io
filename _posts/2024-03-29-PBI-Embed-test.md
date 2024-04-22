---
title: WIP Power BI Embed Test
date: 2024-03-29
tags: [PowerBI, Test]
published: true
image:
  path: https://krshea.github.io/assets/post_files/costco_analysis/post_thumbnail.png
---

<style>
  .red-square {
    color: red; /* Changes the color of the square to red */
    font-size: 25px; /* Adjusts the size of the square */
  }
  #panel-wrapper {
    position: relative;
    left: 500px; /* Move right by 100 pixels */
  }
  body {
    font: 15px/1.5 arial, helvetica, sans-serif;
  }  

p:first-of-type:first-letter {
    float: left;
    font-size: 45px;
    line-height: 1;
    font-weight: bold;
    margin-right: 5px;
}
</style>


## Introduction

Few retailers evoke as much loyalty and passion as Costco Wholesale Club.  With members renewal rates between 86% and 93% since since beginning to report this information in 2003, some members display fanatical devotion to the wholesale giant. Members have been known to host birthday parties at Costco stores, wear Kirkland branded clothing, and buying their pets Costco themed pet toys.  Sam’s Club, Costco’s largest direct competitor, while arguably just as good in many areas and better in some (technology for example) lacks any notable fanbase. 

Costco (and Sam’s) sell products in bulk quantities to members who pay for the privilege to shop there, though technically wholesale clubs both have managed to buck the trend of the dying department store.  While the few remaining Sears stores are ghost towns and Macy’s is closing 150 stores Costco continues to post strong growth in stores, revenue, and members.

The age of the department store is over, the age of the Warehouse club is here.  Where else can members purchase groceries, clothes, tires (or the whole car with the Costco auto program), fine wines, gold bars, and family vacations.


## A brief history

The first Costco opened in 1976 as Price Club and with the exception of 1979 and 1980 has opened multiple stores every year since.  Costco hasn’t opened less than 10 stores in a year since 1994 and openings peaked in 2001 and 2013 with 41 stores opened.  On average Costco has opened 18.5 stores every year since 1976.

Costco is a primarily US based retailer but began its international expansion in 1994 with its first store in Mexico and later in Canada.  

As of 2023 Costco operates 872 stores total with 601 stores in the US, 108 in Canada, 40 in Mexico, and 123 other stores in Asia, Oceania, and Europe.

Costco’s expansion has generally remained US focused, however some years have seen more international growth than in the US.  1994, and 1995 both saw Mexican and Canadian openings outnumber US store openings, while 2013 was notably the first and only time a single country (Mexico) had more openings than the US.  2023 was the first time that expansion in Asia and Oceania drove Costco’s new store center of gravity, a measurement of the average latitude and longitude of new stores off the continent of North America.

The interactive graphic below shows store openings by year as well as a three year moving new store center of gravity line in orange.

<iframe title="COSTCO Analysis pre_final" width="800" height="1500" src="https://app.powerbi.com/view?r=eyJrIjoiYmRiNDI0MjUtNjMyYi00YmI2LTk4NWMtMTI2YTIwMjliZjVhIiwidCI6ImRiOTA3NTYwLTZhNDktNDk2Ni1hNzgwLTY5ZDMyODg4NGYwYiIsImMiOjJ9&pageName=ReportSection5ccecb01ea7477038ba1" frameborder="0" allowFullScreen="true"></iframe>


## Amazing membership and revenue growth but members aren’t spending more

With impressive growth in stores comes even more impressive growth in revenue.  Costco’s revenues have grown to over 240 Billion annually as of 2023.  Revenue growth is obviously driven by new stores in part, but interestingly membership growth has outpaced new store growth by a wide margin.  Costco now has 70 million members.  If you’ve felt Costco is more crowded than it used to be, you aren’t imagining it.   The number of members per Costco has nearly doubled since the 90’s from around 40,000 members per store to over 80,000 members per store.

Some of the growth in membership is driven by affiliates of business members, but affiliate memberships are paid for just like any other membership.  These figures exclude free household cards.

Gold-Star members, Costco’s basic membership, pay an annual fee of $60, however members who pay $120 annually get to be Executive members.  The primary benefit of executive membership is a 2% rebate at the end of the year on Costco purchases.  The breakeven spending for an executive membership is $3,000 a year or just $250 a month as Gold-Star members are frequently reminded during upsell attempts by Costco cashiers.

Likely much to the chagrin of management, despite the upselling, on average Costco members aren’t spending more.  Adjusting for inflation, revenue per member peaked in the early 2000’s but has stayed essentially flat since the Great Recession of the mid 2000’s.


 <img src="./assets/post_files/costco_analysis/chart_more_crowded_stores.png" alt="Excel1" width="500"/>


## Demographics of a Costco county

So how does Costco decide where to place a store anyways?

Conventional wisdom says that Costco tends to target more affluent areas than does Sam’s club.  This appears to be true for the most part, the median income of counties in the United States in 2023 was $60,451, the median income of counties with a Costco was $79,826 while Sam’s was $68,014.

Costco has three stores in Puerto Rican municipios with median incomes under $30,000 though.  Puerto Rico is however one of the densest territories in the world, San-Juan municipio has over 7,000 people per square mile well above the US county median of 551 people per square mile.

Costco counties also appear to be on average slightly more educated and slightly younger  than non-Costco counties. 


 <img src="./assets/post_files/costco_analysis/demographic_summary.png" alt="Excel1" width="800"/>

What about more “average” cities?

Multiple cities have started facebook pages to convince Costco to open in their neighborhoods and even signed change.com petitions.

Social media discussions abound about what a city needs to do to get a Costco.  Redditors in high income Asheville, North Carolina (Buncombe County) posit that Costco doesn’t build a store in their town because there are no plots of land big enough, but Sam’s Club is there with a similarly sized store.  Maybe Costco said “this town ain’t big enough for the two of us”.

Or perhaps you may be curious why Albermale County, home of the University of Virginia, has a Costco while Alachua County, home of the University of Florida does not. Both are similarly sized College towns.   

The interactive map and tables below detail some of these findings.  Counties in the map are shaded according to a machine learning model which scored a county’s suitability for a Costco according to some of the variables highlighted above.


<iframe title="COSTCO Analysis pre_final" width="1150" height="2500" src="https://app.powerbi.com/view?r=eyJrIjoiYmRiNDI0MjUtNjMyYi00YmI2LTk4NWMtMTI2YTIwMjliZjVhIiwidCI6ImRiOTA3NTYwLTZhNDktNDk2Ni1hNzgwLTY5ZDMyODg4NGYwYiIsImMiOjJ9&pageName=ReportSectioncaa6a21065a7a30ec4be" frameborder="0" allowFullScreen="true"></iframe>


## Conclusion

Costco still has lots of room to grow in the United States and there are plenty of suitable counties for Costco to continue its expansion.  The real question is if Costco will make a come to Costco facebook owning American city rejoice or continue its inroads into Europe, Asia, and Oceania.<span class="red-square">&#9632;</span>






## Links
https://www.reddit.com/r/asheville/comments/kodlka/whats_stopping_costco_from_coming_to_the/