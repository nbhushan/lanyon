---
layout: post
title: Buurkracht
categories: community-energy-initiatives
---

To mitigate the effects of climate change and global warming, households across the world need to reduce their fossil energy consumption. To this end, environmental community energy initiatives, characterised by bottom-up local initiatives; predominantly driven by volunteers have been emerging across many towns in the Netherlands and beyond. Such initiatives  are collective approaches where individuals (or households) form or join a local initiative to pursue a common goal.

Buurkracht is a prominent example of a a community energy initiative in the Netherlands. The goal of Buurkracht is to stimulate local communities to self-organize into energy-saving clusters. In particular, Buurkracht targets energy efficiency and increased use of renewable energy resources.

The key questions which I focus on are:
+ How do we gain insight into factors which predict membership in Buurkracht.
+ Does membership in Buurkracht affect other energy saving behaviours (spillover effects).

* * *

### Gain insight into factors which predict membership in Buurkracht
In order to understand why do people join Buurkracht, I applied a search method, the *PC algorithm* on data from Buurkracht members and non-members to gain insight into the factors that drive membership in such initiatives.

![Gaussian graphical model  ]({{ site.github.repo }}/assets/buurPC.png){: .center-image }

I found that factors related to the social context forms a distinct causal path leading to membership in the initiative. Furthermore, environmental neighbourhood identity is a key variable which links variables from distinct categories such as personal factors, social factors, and membership. In addition, it seems that initiative involvement intentions directly leads to membership, while communal sustainable energy intentions leads to membership via initiative involvement intentions.

These results can be used to further develop initiatives such as Buurkract, in addition to leading to new theories in environmental psychology.

### Explore spillover effects of being a Buurkracht member.
Reducing peak demand is a key aspect of climate change mitigation in the residential sector. This is because peak demand is often supplied with energy from fossil-powered sources such as natural gas and petroleum. High frequency smart meter data enable us to study how being a member of a pro-environmental initiative can influence the day-to-day dynamics of energy consumption such as peak demand behaviors.

Furthermore, every Buurkract member is provided with a smart meter. These meters measure electricity and gas consumption every 15min. The typical data from a smart meter can be visualised as a time-series.

![Gaussian graphical model  ]({{ site.github.repo }}/assets/spaghetti_timeSeries.png){: .center-image }

We can clearly see that energy consumption follows a seasonal pattern. There are time-of-day effects and weather effects which drive the dynamics of energy consumption. A typical daily consumption profile of a buurkracht neighbourhood in Groningen is shown below.

![Gaussian graphical model  ]({{ site.github.repo }}/assets/M1dailySmooth.jpg){: .center-image }

Recall that one of the key goals of Buurkract is to encourage adoption of renwable energy sources such as PV-panels (zonnepanelen). In the above figure, the blue line in the above figure represents the daily consumption profiles buurkracht members who invested in a PV panel; and the red line represents the daily profile of buurkract members who chose not to invest in a PV panel. We can now investigate difference in these two classes of Buurkract members.

![Gaussian graphical model  ]({{ site.github.repo }}/assets/M1dailydiff.jpg){: .center-image }

As the figure indicates, one would expect differences in daily energy consumption when the sun is shining (indicated by the portion highlighted in red). However, An interesting question is therefore: does investing in a PV-panel also affect how households consume energy during peak demand hours?

I answer this question using a non-linear general additive mixed model. The final model includes  smart meter data from **4865 households** and is run on a high performance computer cluster.

These models and more can be found at <a href="https://nbhushan.shinyapps.io/slimDashboard/" target="_blank">slimDashboard</a>
This is an interactive dashboard built using R-shiny which enables users to **load/explore/model/understand** energy consumption of Buurkract members.
