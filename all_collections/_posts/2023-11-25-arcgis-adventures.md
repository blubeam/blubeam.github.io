---
layout: post
title: ArcGIS Adventures
date: 2023-11-25
thumbnail: "assets/images/arcgis-adventures/thumb.jpg"
---

After reading this [article](https://www.audubon.org/feature/aerial-odysseys-bird-migration-americas) and seeing opportunities to contribute towards conservation I have decided to learn ArcGIS

and what better to do that than to map my five favourite local birds!

So looking for data online I came across nbnatlas.org which is a wonderful resource!

now the hardest part of it all is to select my top 5 birds to show (in no particular order):

* Osprey
* Peregrine Falcon
* Puffin
* Pied Wagtail
* Raven

![screenshot of nbnatlas.org website](/assets/images/arcgis-adventures/1-downloading-data.PNG)

this gave us a nice csv file of all the occurrences in 2022.

Using ArcMap 10.7.1

Now I created a map and chose the satellite imagery without road markings, as birds do not follow them neither shall we

![adding the basemap](/assets/images/arcgis-adventures/2-add-basemap.PNG)

this was then cropped to show only the relevant land masses

![cropping the map](/assets/images/arcgis-adventures/3-cropping-map.PNG)

the data taken from nbnatlas was then imported into ArcMap, for the x and y coordinates to be plotted correctly their coordinate system was set to [WGS1984](https://en.wikipedia.org/wiki/World_Geodetic_System) 

to provide clear analysis the symbol colour of each record is determined by the Species ID (designated by nbnatlas) and then Common Name later.

![Differentiating symbols](/assets/images/arcgis-adventures/4-different-symbols.PNG)

ArcMap contains an amazing feature called HTMLPopup which displays the data point in a table for the user to read. After selecting the relevent fields this is how it looked:

![Selecting relevent data fields](/assets/images/arcgis-adventures/5-selected-fields.PNG)

For the map user to have access to the data provider and dataset from nbnatlas the HTMLPopup can be edited using xslt to provide links to them (REWORD)

following is a code snippet which was inserted toward the end of the default xsl file (line 145)

```xml
<xsl:when test="FieldName[starts-with(.,'Dataset ID')] or FieldName[starts-with(.,'Data Provider ID')]">
    <a target="_blank"> 
        <xsl:attribute name="href">
            https://registry.nbnatlas.org/public/show/<xsl:value-of select="FieldValue"/>
        </xsl:attribute>
        <xsl:value-of select="FieldValue"/>
    </a>
</xsl:when>
```

Say the dataset ID is: 'dr478' the code above converts this to a [link](https://registry.nbnatlas.org/public/show/dr478) for the RSPB Annual Reserve Avian Monitoring on the nbnatlas website. This also functions the same for data providers, such as the RSPB.

Here we can see this visualised in a HTMLPopup

![HTMLPopup example with link to source](/assets/images/arcgis-adventures/6-link-to-source.PNG)

To enhance the data displayed the xsl code was further modified to retrieve beautiful images of birds kindly provided by the [RSPB](https://rspb.org.uk). Originally I had planned to attach the image files to the document, but thought that having an agile approach was more fitting to the modern web. The xls file has been included [here.](https://github.com/blubeam/blubeam.github.io/blob/main/assets/files/html-pop-up.xlst)

![HTMLPopup with embedded image](/assets/images/arcgis-adventures/7-embedded-image.PNG)

Each data point contains a field named "Coordinate Uncertainty" which is measured in meters. The radius of the symbol for each data point can be made to scale proportionally to this value. Additionally this can be done with an accurate scale, to give proper perspective to where the bird was spotted. 

![Proportionally sizing the symbols](/assets/images/arcgis-adventures/8-proportional-size.PNG)

There is so much to explore in ArcGIS, I've barely scratched the surface of what is possible and I am excited to keep on learning what that software can achieve.

The next set of data with time stamps I would like to map summer/autumn migrations over many years. 

I expected that python scripting would be necessary to complete most of what I was looking to do, this was not true as the xls engine is very powerful.
