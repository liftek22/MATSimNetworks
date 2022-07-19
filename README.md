# MATSimNetworks
Trying to learn how to generate MATSim Networks from scratch

## 6th July 2022

Farnoosh sent me a nicely curated collection of MATSim resources and pointed out a good starting place. 

It is  slide 177 of the first slide deck of the following link

simunto.com/matsim/tutorials/eifer2019/

The series of slides provides different methods to create a network. 

### GOAL A: I will start from the beginning.  Create a basic network.xml file and then visualize it on VIA. 

First, opened Via and refreshed memory regarding how to add data source, and add layer to visualize a network. 
Then made an XML file using Notepad using the simple network provided in the slide above. 

```js
<?xml	version="1.0"	encoding="utf-8"?>
<!DOCTYPE	network	SYSTEM	"http://www.matsim.org/files/dtd/network_v2.dtd">
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

_If a road section is two-way, it must be defined by two links._



So what does this 
``` <?xml version="1.0" encoding="utf-8"?>```
mean? 

Here's an answer: https://stackoverflow.com/questions/13743250/meaning-of-xml-version-1-0-encoding-utf-8

Also, DOCTYPE could be HTML as shown in example in the link above. Here we have MATSim. 


- Link length unit is meters
- Link capacity unit is vehicles/hour
- Link freespeed unit is meter/second

Those lengths, do I always have to calculate the Euclidean distance between the actual nodes ( as I know their positions)? 


## 8th July 2022

Trying find some explanation on the `capperiod` attribute.  The Book and the Manual didn't even have the word.  Google yields a few results but it is mentioned without explanation.  Looks like it's a 'timestep' value. 

Was looking at `permlanes`.  Interestingly one link is one way of course, but it can have several lanes that way. Hence my understanding above (yesterday) is mistaken.  In fact, this network1.xml define a roadway  with two road segment.  One road segment has two lanes in opposing direction traffic flow.  The second road segment actually has three lanes.  Two has traffic in one direction, while the other has traffic in anoter direction. 

How would I have assigned each of the permlane with a different mode? 

By the way, no matter how much you break down a link into permlanes, there will be once capacity per link.  MATSim doesn't differentiate between capacity of lanes in a link. Considers the _n_ number of lanes together for capacity. 


## 11th July 2022

Nodes can have attributes. That means, you can define an arbitrary attribute and assign a value to it. 

The example showed a node having the attribute _signalized_ which takes in a boolean variable. And assigned it to _true_

Same thing for links.  The example defined three attributes for a link

An attribute called _name_ which takes in a string variable. Assigned it _Main Street_
An attribute called _isTunnel_ which takes in a boolean variable. Assigned it _false_
An attribute called _category_ which takes in an integer variable. Assigned it _3_


_Signalized, name, isTunnel, Category_ are all just examples and have no meaning in MATSim 


```ja
<?xml	version="1.0"	encoding="utf-8"?>
<!DOCTYPE network SYSTEM"http://www.matsim.org/files/dtd/network_v2.dtd">
<network>
 <nodes>
  <node id="1" x="2000" y="1000">
	<attributes>
	<attribute name="signalized" class="java.lang.Boolean">true</attribute>
	</attributes>
  </node>
	...
  </nodes>
 <links capperiod="01:00:00">
  <link id="1" from="1" to="2" length="3000.0" capacity="1800" freespeed="13.88" permlanes="1" modes="car">
	<attributes>
	 <attribute name="name" class="java.lang.String">Main	Street</attribute>
	 <attribute name="isTunnel" class="java.lang.Boolean">false</attribute>
	 <attribute name="category" class="java.lang.Integer">3</attribute>
	</attributes>
 </link>
...
</links>
</network>
```


## 15th July 2022

We can create network.xml files by hand like above, if we have small networks. 

We can also convert data from OpenStreetMap and create an XML file. 

Several things given in the slides. 

But let's Google how to convert OSM data into network.xml file for MATSim. 

1) We can extract stuff from OSM and convert to XML using MATSim API
2) We can download JOSM for OSM and use it to generate an XML file. 


## 17th July 2022

Let's learn the JOSM way to generate XML file.  Seems most flexible and can be used for small or large networks. 


First need to download JOSM. 

Found this site: https://learnosm.org/en/  So nice and friendly! 

1. Read 'Beginner's Guide' Landing page.
2. Read 'Beginner's Guide > Introduction' page.
	Summary:  Information is powerful, can help us make good decisions and improve our lives.  Maps are one way to convey information.  But if I draw a map by hand, it isn't very helpful as only I'll have a copy and it may not have standardized marks.  Making digitals maps allow us to overcome these problems.  OSM is a tool to make and access digital maps. 
3. Read 'Beginner's Guide'> openstreetmap.org 
       Comment: Was checking out different Layers.   Metrotech area shows all layers.  Bashundhara doesn't even have a transportation layer :(   
        TODO:  We must contribute. 
	
	Ok, so I signed up.  Went for Public Domain because I want Bangladesh to be benefitted as much as possible  :heartpulse:


Some basic lingo: 
		
		
		An editor is a program or website you can use to edit the map.

		A node is a point on the map, like a single restaurant or a tree.

		A way is a line or area, like a road, stream, lake or building.

		A tag is a bit of data about a node or way, like a restaurant's name or a road's speed limit.
		

Going through the walkthrough

Map _features_ are represented using _points, lines or areas_.  _points_ are _nodes_, _lines_ are _ways_. 



Added my first point on OSM! Yay!!  Did that for Aksaray! :D   Entered the restaurant's name and several info about it. 



Signed up for OSM Bangladesh mailing list.  Based on the archive, they seem to have some good activity. 



---- 

 Now starting the JOSM part. 
 
 
 
1. Read 'JOSM- Detailed Editing' landing page
2. Read 'JOSM-Detailed Editing'> 'Getting Started with JOSM'

     Downloaded JOSM. 
     Played around with the sample file. 
     Deleted it. 
     

## 18th July 2022

1. Read 'JOSM-Detailed Editing'> 'The JOSM editing process'
 
    Editing OSM using JOSM. Download -> Edit -> Upload.  Edit using GPS, personal notes, field papers, satellite imagery etc. 
    
     Imagery for OSM is provided by Microsoft Bing
     
     It doesn't say 'Bing Sat' per tutorial, but rather 'Bing Aerial Imagery'. 
     
     
     Added 'Grand Market Halal' name on downloaded region in OSM. But cannot remove previous tags.  I could use green grocer preset. 
     Uploaded this change. 
     
     
2. Read 'JOSM-Detailed Editing'> 'Editing Field Data'
3. Read 'JOSM-Detailed Editing'> 'JOSM Editing Tools'
4. Read 'JOSM-Detailed Editing'> 'Plugins'
		
		
	Added the MATSim Plugin. And Restarted.  MATSim option shows up as well as stuff like capacity etc.  
	
Now how to I download as an xml file?
		
Ah, so you just select the region (you will see all capacity , permlanes etc info), right click on the layer and save as xml file. 


And I used that file to visualize the King's Highway area on VIA! :3 
