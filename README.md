# MATSimNetworks
Trying to learn how to generate MATSim Networks from scratch

## 6th July 2022

Farnoosh sent me a nicely curated collection of MATSim resources and pointed out a good starting place. 

It is  slide 177 of the first slide deck of the following link
simunto.com/matsim/tutorials/eifer2019/
The series of slides provides different methods to create a network. 

###GOAL A: I will start from the beginning.  Create a basic network.xml file and then visualize it on VIA. 

First, opened Via and refreshed memory regarding how to add data source, and add layer to visualize a network. 
Then made an XML file using Notepad using the simple network provided in the slide above. 

```js
<network>
<nodes>
<node id="1" x="2000" y="1000"/>
<node id="2" x="4000" y="1500"/>
<node id="3" x="3000" y="3000"/>
</nodes>
<links capperiod="01:00:00">
<link id="1" from="1" to="2" length="3000.0" capacity="1800" freespeed="13.88" permlanes="1" modes="car"/>
<link id="2" from="2" to="1" length="3000.0" capacity="1800" freespeed="13.88" permlanes="1" modes="car"/>
<link id="3" from="2" to="3" length="5000.0" capacity="3500" freespeed="22.22" permlanes="2" modes="car"/>
<link id="4" from="3" to="2" length="5000.0" capacity="1800" freespeed="22.22" permlanes="1" modes="car"/>
</links>
</network>
```

(Used this link to  recall how to make the codeblock above https://www.freecodecamp.org/news/how-to-format-code-in-markdown/#:~:text=There%20are%20two%20ways%20to,will%20apply%20syntax%20highlighting%20to.)


## 7th July 2022

So, yesterday,  I just created the network1.xml file and visualized it on VIA.  It gives a V-shape shifted about  90 degrees.  Basically, it represents two road segments. If we match it with the code, MATSim is expecting us to define this shape as three nodes and 2 edges  - but each edge will have a seperate link defined for each direction.  That means,  direction of road section matters. 

_If a road section is two-way, it must be defined by two links_
