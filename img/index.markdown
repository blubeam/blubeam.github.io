---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

After reading this article: https://www.audubon.org/feature/aerial-odysseys-bird-migration-americas and seeing opportunities to contribute towards conservation I have decided to learn ArcGIS

and what better to do that than to map my five favourate local birds!

So looking for data online I came across nbnatlas.org which is a wonderful resource!

now the hardest part of it all is to select my top 5 birds to show (in no particular order):

Osprey
Peregrine Falcon
Puffin
Pied Wagtail
Raven

~~~ INSERT NBNATLAS SCREENSHOT 4 ~~~

this gave us a nice csv file of all the occurences in 2022.

Using ArcMap 10.7.1

Now I created a map and chose the sattelite imagery without road markings, as birds do not follow them neither shall we

~~~ INSERT IMAGE 2 ~~~

this was then cropped to show only the relevant land masses

~~~ INSERT IMAGE 3 ~~~~

the data taken from nbnatlas was then imported into ArcMap, for the x and y coordinates to be plotted correctly thier coordinate system was set to [WGS1984](https://en.wikipedia.org/wiki/World_Geodetic_System) 

to provide clear analysis the symbol colour of each record is determined by the Species ID (designated by nbnatlas) and then Common name later.


~~~ INSERT IMAGE 5 ~~~~

ArcMap contains an amazing feature called HTMLPopup which displays the data point in a table for the user to read. After selecting the relevent fields this is how it looked:

~~~ INSERT IMAGE 6 ~~~~

For the map user to have access to the data provider and dataset from nbnatlas the HTMLPopup can be edited using xslt to provide links to them (REWORD)

following is a code snippet which was inserted toward the end of the default xsl file (line 145)

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<xsl:when test="FieldName[starts-with(.,'Dataset ID')] or FieldName[starts-with(.,'Data Provider ID')]">
	<a target="_blank">	
		<xsl:attribute name="href">
			https://registry.nbnatlas.org/public/show/<xsl:value-of select="FieldValue"/>
		</xsl:attribute>
		<xsl:value-of select="FieldValue"/>
	</a>
</xsl:when>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Say the dataset ID is: 'dr478' the code above converts this to a [link](https://registry.nbnatlas.org/public/show/dr478) for the RSPB Annual Reserve Avian Monitoring on the nbnatlas website. This also functions the same for data providers, such as the RSPB.

Here we can see this visualised in a HTMLPopup

~~~ INSERT IMAGE 7 ~~~

To enhance the data displayed the xsl code was further modified to retrieve beautiful images of birds kindly provided by the [RSPB](https://rspb.org.uk). Originally I had planned to attach the image files to the document, but thought that having an agile approach was more fitting to the modern web. The xls file has been included in this repo on github.

~~~ INSERT IMAGE 8 ~~~

Each data point contains a field named "Coordinate Uncertainty" which is measured in meters. The radius of symbol of each data point can be made to s


