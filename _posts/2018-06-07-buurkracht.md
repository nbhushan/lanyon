---
layout: post
title: Why do people join local energy initiatives?
categories: energy-transition psychology data-science
---
---

 Question | What drives membership in Buurkracht?
 :--- | :---:
 Role   | Internal consultant, researcher, data scientist
 Data | Survey data from 386 households (members & non-members)
 Tools | R, causal search methods
 Deliverables |  Code & report ([link](https://doi.org/10.3389/fpsyg.2019.01050))

---

## Case description
To mitigate the effects of climate change and global warming, households across the world need to reduce their fossil energy consumption. To this end, environmental community energy initiatives, characterized by bottom-up local initiatives; predominantly driven by volunteers have been emerging across many towns in the Netherlands and beyond. Such initiatives  are collective approaches where individuals (or households) form or join a local initiative to pursue a common goal.

Buurkracht is a prominent example of a a community energy initiative in the Netherlands. The goal of Buurkracht is to stimulate local communities to self-organize into energy-saving clusters. In particular, Buurkracht targets energy efficiency and increased use of renewable energy resources.

A question of particular interest to applied psychologists and policy-makers is how to motivate citizens to be part of such local energy initiatives. Answering this question requires understanding the relationships between psychological factors leading to membership in such initiatives.

The key question I focus on is: **What are the key psychological factors driving membership in Buurkracht?**

* * *

## Case analysis
In order to understand why do people join Buurkracht, I applied a search method, the *PC algorithm* on data from Buurkracht members and non-members to gain insight into the factors that drive membership in such initiatives.

![Gaussian graphical model  ]({{ site.github.repo }}/assets/buurPC.png){: .center-image }

The model indicates that factors related to the social context forms a distinct causal path leading to membership in the initiative. Furthermore, environmental neighborhood identity is a key variable which links variables from distinct categories such as personal factors, social factors, and membership. In addition, it seems that initiative involvement intentions directly leads to membership, while communal sustainable energy intentions leads to membership via initiative involvement intentions.

These results can be used to further improve initiatives such as Buurkracht, in addition to leading to new theories to be tested by environmental psychologists.

These models and more can be found at <a href="https://nbhushan.shinyapps.io/slimDashboard/" target="_blank">slimDashboard</a>
This is an interactive dashboard built using R-shiny which enables users to **load/explore/model/understand** energy consumption of Buurkracht members.
