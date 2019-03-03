# InteractiveMapping #
## **Reflective Analysis** ##
- - - -


### **Target Audience**

Community gardens not only allow people to connect with nature, but it can also contribute to the sustainability of the food system by providing local food sources. However, the lack of accessible and transparent information on the location and size of community gardens have created a barrier for environmentally conscious and garden-loving Vancouverites to engage in community gardening. To address this gap, I decided to create a map that can showcase garden and help maps users locate the most accessible garden(s) to them.

### **Design Process**
Before delving into the coding of this map, I asked myself a couple of guiding questions to start the design process: why do I need to customize this mapping experience? What is the purpose of this map? How, where, and why will our users interact with this mapping experience?<sup>1</sup> The last question concerns about User Interface and User Experience (UI/UX) design and their applications in cartography. Adopting UX/UI’s concepts, guidelines, and workflows are crucial to engage map users as they inform effective and two-way interface design and interactions. In the light of that, I followed Norman’s seven stages of interaction for UX developers to try to understand how users may interactive with my map and structure the map accordingly.<sup>2</sup> The table below detailed the design process of the map.


|   Stage     | Scenario 1: |
| ------------- | ------------- |
|   Forming the Goal   | “I want to start gardening in my neighbourhood.”|
|   Forming the Intention | “I will start by looking for the nearest community garden from my home.”|
|   Specifying an Action | “I will use the search box to locate my home.”|
|   Executing the Action | “I type my address into the search box.”|
|   Perceiving the System State | “I see that the pop-up window of a garden opens up.”|
|   Interpreting the System State | “I think this means it is the closest community garden from my home.”|
|   Evaluating the Outcome | “I can now decide whether to visit that community garden and start gardening there or not.”|


### **Interactivity**
This map has several elements of interactivity supported by a variaty of interaction primitives:

![Emily Screenshot](LayerSwitcher_1.JPG)

First, the map ‘flies’ to a community garden when the user clicks on an icon on the map or a garden name on the sidebar. The name of the selected garden on the sidebar will also be highlighted when an icon is clicked. This allows users to quickly locate a community garden that interests them. 

Second, a pop-up window with the garden’s name and the number of plots opens when either of the abovementioned actions is triggered. These windows provide additional information that may help users decide whether to visit that garden or not. 

Third, map users can search for a location (e.g. their address) and look for the closest community garden. To facilitate users’ interaction with the interface, the message in the search box is customized to tell users what to type there. This acts as a strong affordance that signals the user about how to interact with the map.<sup>3</sup> Besides, only locations within Vancouver BC can be searched up as a bounding box is set to that area to avoid confusion with another place of the same name. Once a location is specified, the distances between the searched location and all the gardens are calculated by turf.js. The gardens are then sorted from the closest to the farthest to the search location on the sidebar. At the same time, the pop-up window of the closest garden will open to inform users that is the most accessible garden. 

Fourth, users can switch between two map styles: Street and Satellite. I picked Street as the primary map style as it provides clear and comprehensive representations of road networks and points of interest,<sup>4</sup> two elements vital for navigating through the city. However, users also have the option to look at how these garden look (at least from bird eyes view) in real life using the satellite style. As shown in the images below, satellite imagery is more accurate in showing the arrangement, size, and the state of a garden. 

![Emily Screenshot](LayerSwitcher_1.JPG)

Fifth, the map can be zoomed back out to Vancouver after users examined a specific garden by clicking “Back to Overview”. This saves users’ time in zooming out the map and allows for smoother interaction with the map.

### **Choices of data and cartographic stylings**
Only one data set, community garden data from the City of Vancouver, was used for this map as the Street base map is sufficient for providing context to this data for users to locate the gardens, such as road and transit networks.

In terms of cartography styling, colour and icon are two key components. The colour palette of the base map was adjusted to create a more harmonious interface. It is achieved by changing the colours on the base map, such as picking a milder orange for highways and a lighter shade of green for parks. The muted and earth background also helps establish a visual hierarchy which highlights the vibrant and saturated green markers for the gardens.<sup>5</sup> Most features, such as the sidebar, icons, pop-up window header, and the checkboxes for map styles, were all styled in different shades green to create a more cohesive map.

![Emily Screenshot](LayerSwitcher_1.JPG)

Icons used in this map are widely recognizable and easy to understand A sprout image was used for gardens and a ‘You are here’ icon was used to indicate map user’s search location. The latter also provides visual feedback for users and facilitate strong feedback that signals to users about what happened as a result of their interaction (search for a location). <sup>6</sup> 

### **Limitations**
I recognized that this map is flawed in a number of ways.  First, the sizes of the makers do not change according to the different zoom levels. It is because the code used for adding a marker to the map does not contain a size parameter. Maker size is defined in CSS so it is less flexible and responsive to zoom level changes. As a result, the You Are Here symbol may seem too big on the overview scale, while the leaves for gardens are too small when zoomed in. 

Second, the satellite map view does not necessarily provide an accurate representation of the gardens. Mapbox uses MODIS imagery from 2012–2013, Landsat imagery 5 & 7 from 2010-2011, USDA’s NAIP 2011–2013 to compose this map style. Gardens that were built after 2013 are not presented in this map view. 

Third, only the default Mapbox map styles can be specified in the map style switcher. When users select Street on the switcher, the base map will be that with a high-contrast colour system instead of the one I had modified with a visual hierarchy in mind. Unfortunately, the checkboxes cannot be unchecked, and the only way to get back to the original base map is to reload the page.

Finally, I was hoping to add a filter for the gardens data based on their ‘Jurisdiction’ property values. This property is important as it indicates whether the gardens are owned by the city, park board, TransLink, or private property (i.e. whether may users are allowed to garden there or not). However, it was not possible to extract property information from the customer markers so I was not able to create those filters.<sup>7</sup> 


##**Map Critique**

I did a map critique with Kiyomi, Mychelle and Louisa. They gave some helpful advices such as customizing the search box from ‘Search’ to ‘Enter your address here’ and choosing milder colors for the base to enhance visual hierarchy. I also contributed to the map critique for Kiyomi about making larger circle for crimes and Louisa about having a more vibrant base map to catch map users’ attention.

Below are the tutorials and examples I followed to produced this map. I have added notes in my code to indicate where I used these resources.

Build a garden locator: https://docs.mapbox.com/help/tutorials/building-a-store-locator/ 

Change a map style: https://docs.mapbox.com/mapbox-gl-js/example/setstyle/

Create Back to Overview button: https://docs.mapbox.com/mapbox-gl-js/example/flyto/

Add custom markers: https://docs.mapbox.com/mapbox-gl-js/example/custom-marker-icons/

Add a geocoder: https://docs.mapbox.com/mapbox-gl-js/example/mapbox-gl-geocoder/

Limit geocoder search to Vancouver: https://docs.mapbox.com/mapbox-gl-js/example/mapbox-gl-geocoder-limit-region/

Change placeholder for the search box: https://github.com/mapbox/mapbox-gl-geocoder

Style map with CSS: https://www.w3schools.com/

## **Link to Map**

https://emilyl3117.github.io/WebMapping/PipelineIncidents.html

## **Data Source**
The community Garden data was obtained from the City of Vancouver Open Data Catalogue website:https://data.vancouver.ca/datacatalogue/index.htm


## **Footnote**
<sup>1</sup> “The Guide to Map Design,” Mapbox, accessed January 30, 2019 https://www.mapbox.com/resources/guide-to-map-design-part-1a.pdf, 5

<sup>2</sup> UCGIS, “CV-13 - User Interface and User Experience (UI/UX) Design,” University Consortium for Geographic Information, Science	https://gistbok.ucgis.org/bok-topics/user-interface-and-user-experience-uiux-design 

<sup>3</sup> UCGIS

<sup>4</sup> “The Guide to Map Design,” 98

<sup>5</sup> “The Guide to Map Design,” 19

<sup>6</sup> UCGIS

<sup>7</sup>I tried following this tutorial to create the filter: https://docs.mapbox.com/mapbox-gl-js/example/filter-markers/
