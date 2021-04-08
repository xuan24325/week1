# week1
The Battle of Neighborhoods (Washington State)

#### Introduction/Business problem
Washington State, where I live in. For tourists, finding the right place to eat can be a challenge. This is just one motive for giving tourists a good overview about what to eat where.

Thus, the goal I want to reach with this exercise is to give a simple recommendation to tourists in WA. In which county of the state will you find a large number or even concentration of which types of restaurants? Where to eat seafood, where to find Mexico food, where to get fast food? The target audience are foreign tourists.

#### Description of the data
I will, as requested by the assignment task, use foursquare data about restaurants in WA. Foursquare is a US tech company from New York focusing on location data. Their technology and data powers apps such as Apple's Maps, Uber, Twitter and many other household names. I will use foursquare data such as the restaurant name, ID, location and category of food.

Also, I will use the overview of districts/city parts of WA from Wikipedia: https://en.wikipedia.org/wiki/List_of_counties_in_Washington


Here, you will find a table "County" which shows the 39 counties and its neighborhoods parts. I will use these counties and the data about restaurants in these districts from foursquare to show the density of restaurants in them.

#### Methodology
In this section, I will describe the data analysis and how I used the data to yield the results.

Starting out, I scraped data from Wikipedia to create a dataframe. For this, I used the pandas read function. I had to clean the resulting data frame in terms of unnecessary information or data that could not be handled in a data frame, such as picture data of the coat of arms of each district. The result is a nice data frame.

Then, I enabled geopy functions. I used the nominatim function to add geospatial data to the data frame, that is the latitude and the longitude seen on the right side of the following table.

Using the folium package and my data frame, I then created a map with counties on it.

Now, foursquare data comes into play. I first did a view try-outs for the district "Innenstadt", which I know pretty well, to see if the venues retrieved from foursquare seem reasonable and correct. That was the case.

Then, retrieved the foursquare data for all venues on foursquare with a distance of less than 3000 meters from each center of each county, as indicated as blue dots in the map above. The result was a list of 217 venues all over WA. Out of these 217 venues, 14 unique categories of restaurants.

I plotted a bar chart with the frequency of the 10 most frequently occuring restaurants, using seaborn/matplotlib packages. We can see that American, seafood and Mexican restaurants are the most frequently occuring restaurants in WA, which seems pretty reasonable, as Washington State is a coastal area.

To find clusters of restaurant types in the different city districts, I first transformed the data frame with the restaurant venues, associated to city districts, by one-hot encoding (0/1).
Next, I used grouping to show the frequency of each category of restaurants in each city district.
I used this information to create a data frame in which you can see the most common restaurant venue types for each county district.

Now, with all this data, I could finally run an unsupervised machine learning algorithm, more specifically, a k-means clustering algorithm from the scikit-learn package. One could use the ellbow method to systematically define the k value, but I simply chose k to be 5.

#### Results
What we see are the counties and their most common venues, and they now have been assigned five different cluster labels from 0 to 4.
We can now use the cluster labels to show the city districts marked with a cluster-specific color on a map, again using folium:

You will see 6 bubbles for the 6 counties, with five different colors for the five different clusters.

Now, what is the final result of this exercise? We now can show five clusters of restaurant type concentrations for WA, which I named according to the restaurant concentration the data shows.

Cluster 1 - the general restaurant cluster(northeast).

Cluster 2 - the Chinese Restaurant cluster(central).

Cluster 3 - the American & seafood Restaurant cluster(norhtwest).

Cluster 4 - the Mexican Restaurant cluster(south).

Cluster 5 -  the American & Asian Restaurant cluster(southwest).

Interestingly, it is really possible to define clusters of certain cuisines in WA. People living in WA will probably agree that these clusters sound pretty reasonable and are not too far away from what you would have expected.

#### Discussion
If I reflect the work necessary to create these results, what comes to my mind is that for typical ways of scraping, cleaning, handling, transforming and visualizing data, all the tools are simply there. We just have to get to know the available open source packages and learn how to use them. What I find fantastic is that nearly all of them are free of charge. Also, a simple notebook computer is enough. All the rest is concentrated, creative, interesting, sometimes hard work and searching for hints, tips, examples, explanations etc. in the web. With these tools, many exciting data science use cases can be created, for all kinds of useful purposes.

#### Conclusion
We achieved the goal presented at the outset of this blogpost: tourists can see in the results which  districts best match their food desires. This is just one example of fantastic data science uses cases one can realize applying technology which is available for free today! What a time to be alive.

