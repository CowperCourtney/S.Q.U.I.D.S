# S.Q.U.I.D.S

Ongoing outline of Tasks to Complete Project Strategic Quantification of Unregulated Illegal Darkfleet Subterfuge

I am studying how China's fishing practices influence the population of Japanese Flying Squid (JFS) which is both an economically and biologically important species for a number of reasons. What is most concerning is I have found not only are they over fishing and participating in IUU (illegal, unreported, unregluated) fishing but they are not afraid to be aggressive and enter economic exclusive zones. https://www.nbcnews.com/specials/china-illegal-fishing-fleet/

These activities have decimated the population making it much harder for small communities that depend on this species for everyday living. Fishing towns in North and South Korea as well as Japan have fished for the species for generation and it makes up a lot of their protein. These economies depend on this stock for survival, and many are struggling to get by and are willing to die to obtain their catch. These smaller fishing villages consist of smaller boats with less sophisticated equipment than what would be found in a Chinese long distance fleet vessel. These long distance Chinese vessels are able to catch, process, package and freeze hundreds of tons of fish in a matter of days without having to depend on other boats to haul a catch back for processing. Additionally, they are often run supplies from smaller fleet vessels so they can stay out longer. Due to this high level of efficiency China accounts for 50%-70% of the total worldwide catch of JFS. This has lead to dwindling numbers of squid for fisherman who do not have the capability to travel as far. With little gas, food and water, no bathrooms these smaller boats end up getting stuck out at sea. "Skeleton crews" are found on the shores of Japan, empty boats with deceased crew believed to have died from starvation, dehydration and/or overexposure to the elements. Hundreds of these boats wash up on the shores of Japan each year as travel too far out in search of squid.

Chinese vessels often do not adhere to worldwide agreed upon fishing regulation. Transponders are switched off although law requires they be on at all times, ships are often marked poorly or not at all and multiple vessels have been observed working under a single license which is also a violation. This has given them the nickname "the dark fleet", since they are nearly invisible. Luckily, satellites are able to track movement well and especially those with powerful light traps used for squid fishing at night. Global Fishing Watch provides free map data as a way to see what kind of ships are out there and their various activities. I was able to put together some images of their activities. I have reason to believe that due to the nature of this short lived species, they have every reason to migrate more north in search of cooler waters as temperatures rise.

https://globalfishingwatch.org/map/workspace/udw-v2-9b6ea9b6-9117-4644-8f49-508c2690f34e

The above link is activity of fishing effort from specifically Chinese ships in the Sea of Japan over the last few years. I am looking to compare it to migratory patterns of squid in the same area as illustrated in this study here: https://www.mdpi.com/2072-4292/8/11/921/htm (see figure 5 below) What I was hoping to do, was build an empirical dynamic model using a single species https://www.youtube.com/watch?v=pbTl752pyyMto show how their numbers might be affected in the future, and I am hoping to use a similar model to show where they will go next. https://cran.r-project.org/web/packages/rEDM/vignettes/rEDM-tutorial.pdf This method being used on short lived species in the past has shown potential in determining an accurate population model when compared to traditional methods . https://www.youtube.com/watch?v=IsIOIYc3CUA

This particular species is hard to track since they live very short lives and getting an accurate population count is difficult due to that. However, based on what I have been able to observe thus far I feel the stocks estimated maximum sustainable yield is inaccurate and needs updating. Many fisheries depend on reported data from fisherman in order to be able to estimate what the population looks like, but China has a habit of not sharing information with other states despite having advanced technology to share fisheries information between fleet members in order to maximize productivity. I want to use the satellite data to estimate the catch rate of these ships and combine it with data from sources who do share their information in order to get a more accurate rate of consumption. In terms of migratory patterns, I would like to illustrate with a mapping tool where they have been going and where they are likely to go next. I have reason to believe they are going to start moving into other economic exclusive zones, such as those belonging to Russia and the US. Here is where I would like to create a predictive model, to show what the future holds should business continue as usual.

![image](https://user-images.githubusercontent.com/61677632/119078280-e532b900-b9c3-11eb-9b4d-65b6ac181106.png)

4/8/2021 I have started looking into different modeling strategies after receiving some positive feedback from Noam Ross in regards to project.

He Writes: Dear Courtney,

Sorry it has taken me a bit to respond to this. Thank you for the thorough background. A few thoughts on these approaches:

The EDM approach and similar attractor-based dynamic models are nice generalizable alternatives to more parametric fishery models. Their main drawback (which the parametric approaches share, too), is that they are primarily designed to capture the endogenous dynamics of a closed system. You'll need to incorporate time-series of fishing pressure, climate and other forcing variables as well to capture everything you consider part of the "closed" system. Another challenge with them is that since they are less widely used than other time-series models, there isn't as much tooling to do good performance comparison of them automatically. It would make sense to use an approach like time-series cross-validation (https://robjhyndman.com/hyndsight/tscvexample/) and put up a comparison against traditional ARIMA-type forecasting models to get a good sense of how well your EDM is performing.

Maxent is a solid tool for species distribution modeling - essentially mapping and predicting species observations in space. There's a nice wrapper for it called Wallace (https://wallaceecomod.github.io/), which helps walk through a lot of the data-processing and modeling decisions that need to be made along the way. The big challenge is that, if you want to do prediction into the future, you'll need to model based on variables that you have projections of future values for - e.g. climate variables (esp ocean climate/plankton), geographically-specific estimates of future fishing effort, etc. If those are what you feed in to a model predicting current squid distributions and you have value for these for future years, then you can use them for forecasting.

I myself prefer Generalized Additive Models to MaxEnt for these purposes but the core algorithm used is usually less important than data-processing decisions made. If you are dealing with trawl-observation type data rather than aggregate reported data, this example of GAMs may be useful: https://cdn.rawgit.com/noamross/mgcv-esa-2018/master/example-spatial-mexdolphins.html

These are two very different approaches that attempt to answer different questions. If you have good time-series data of the stock and relevant variables like climate and fishing effort and want to understand the feedbacks, EDM is likely useful. If you're looking to get a better handle of spatial distributions and potential spatial change, distribution modeling with MaxEnt or something will serve you well. Data limitations are your biggest challenge in most cases, and I'd caution against trying to take a very expansive approach that tries to capture time-series dynamics and space at the same time - the high-dimensionality of such a problem often runs into data sparsity and you need a good model of one or the other to expand into something larger.

I hope this is useful. Do let me know if you have more questions.

Best, Noam

After reviewing this feedback I decided to do some additional investigating on how to add a layer to the global fishing watch map in order to show change in ocean surface temperature over time.

https://github.com/Shyentist/fish-r-man/blob/main/fishRman_Handbook.pdf After some searching on Reddit I was able to find this neat tool from a Redditor who does things with global fishing watch data. They created a shiny app called fishRman that analyzes global fishing watch data without having to have prior knowledge on how to use R, SQL and BigQuery. I am collaborating with them at the moment on how best to put a ocean surface temperature layer into the tool but so far extracting the data has been a challenge. However, if I am able to succeed it will save me a lot of clean up time on the data itself.

State of the Ocean (nasa.gov) has the data available regarding ocean temperatures, I am currently working on a way to manage that more effectively because working with massive amounts of data is challenging when you cant just access a server with the data on it.

I have found some additional resources for learning the modeling I will require for this project. https://sites.google.com/site/thebantalab/tutorials https://www.youtube.com/watch?v=f9vwrZf6ncU

My next goals are just to keep working at entering this data as quickly and effectively as possible into their respective programs and hopefully it will tell an interesting story.

4/11/2021

After some troubleshooting I have managed to obtain data files of the select parameters I need. So far I have the csv files filtered (by year, flag, fishing hours and type of fishing gear) with just squid jigging as the type of gear so that the intended catch will be much more accurate. Although pair trawling is a way that squid are caught, they are used for a wide variety of other fish and therefore it would be too hard to estimate how many hours were put into squid fishing, if any at all by that vessel. I have started on some analysis of the fishing effort. So far (and I am still double checking to make sure I have this accurately calculated) in the 2016 year alone Chinese squid jigger vessels committed 1,131,838.2847 hours of fishing effort. Divided amongst 500 vessels that would be 2263.676 hours which is a litte over 40 hours a week per vessel of active fishing effort. These hours do not account for activities such as routine maintenance for the ship, gear care, refueling operations etc. I am eager to see how later years compare and based on the information I have in terms of annual catch rates for the squid and the active fishing effort, I can estimate the maximum sustainable yield based on the relationship between fishing effort and catch rate.

Adding temperature to the map will be done soon with the help from the Github user previously mentioned. I will be contacting him directly so that we can collaborate on how to add this data to the processing tool. It will allow his app to have more features in terms of analysis, and I will be able to show the fishing activity as a top layer so that movement in relation to temperature can be visualized. Some correspondence from earlier this week:

"Currently, there is a cap of 10 minutes of query to fishRman. This is because it relies on a limited amount of traffic, and I would prefer everyone to be able to use it without keeping it all for themselves.

Please remember that this is an SQL constructor, and it is the most useful when one only needs a portion of the dataset, while I believe you were trying to download global data for multiple years.

You can still do that, of course, but you need to download the code from GitHub and 'comment out' the lines of code in global.R. You will know which ones from the comments, but they are line 22 and 23. When you then start the code (you need to install the packages required first), it will prompt you to your own Google Account, so that you can tap on your own resources and have no 10 minutes limit.

I am working on making fishRman a standalone executable file so that the above passages will be automatic."

Lastly we discussed briefly another tool that might be more efficient at mapping the temperature data. They recommended using https://qgis.org/en/site/ but we will discuss options this week.

4/13/2021

I recently finished up getting the data I needed from the tool and had the following reply from the creator of fishRman:

Hi Courtney,

my name is Pasquale, but you can call me Pico, nice to meet you.

About your project, did you manage to actually retrieve the data from State of the Ocean? Would you be able to share a sample so that I can see how the dataframe is organized?

Apart from that, which will maybe require some tweaking, the process to do what you have in mind is the following, repeated for every year, one at a time. If you have managed to run fishRman code on your machine, it would be safer to use that instead of the online version, so that you can use your own specifics instead of the server's, avoiding possible timeouts and running out of memory.

Use fishRman to download GFW data, filtering by 'gear == squid jigger' and 'flag == CHN'. Remember to download both the csv and the converted gpkg file, so to have them ready without rerunning the app. Open QGIS and upload the layers from the gpkg file. In QGIS, also upload the temperature data (and here it is important to know the format) You can now move the layers on top of each other and change their transparencies and color pallettes, to obtain the intended effect.

If what you want is more than just the visual, and actually do quantitative analysis, it is going to be harder, and depends on the temperature data format.

Before making any inference about the results, I suggest you read (if you haven't yet) The Global Atlas of AIS-based fishing activity available at https://globalfishingwatch.org/fisheries/fao-atlas/, and other related works on the same site.

Best regards, Pico

After struggling to download the data in a file format I was familiar with from the NASA website I decided to use the suggestion of downloading QGIS to access ocean surface temperature data.

4/17/2021

So I am starting to put together my data and doing some visuals with it. I have to make sure I have the data correctly summarized before I can do so, and Pico is helping me with this by confirming a few questions I have in regards to using the tools. I am expecting a response by tomorrow or Monday. Our last correspondence was in relation to the mapping tool I was attempting to extract data from. This was his response:

I have a couple sources, and the most detailed is this, from NOAA data, with a huge BUT. It is very easy to use, one can query per specific days, latitudes and longitudes, and the resolution is very high (I think 0.05 degrees), BUT the files are, of course, bulky, since there is a reading for every day, for every 25 km2 square, globally. If one would download just the latest week, for the entire world, it would be a csv between 7 and 9 Gb!

Fishing data are a lot less bulky because, where there is no boat, the data is just not recorded nor stored, so not all squares are reported all the time, as it is the case with temperature.

Otherwise, I am told Copernicus also has the same kind of data, maybe more aggregated but still useful.

Unfortunately, although I plan on moving on to temperature data as well, I am not too knowledgeable about it as of now, and I hope you will inform me in case you find a better solution. In all honesty, the data you so kindly provided seems, in fact, very difficult to use/harvest, and I have no idea what is going on in those links.

Let me know if you need any help throughout your project, I’ll try to help.

Sincerely,

Pico

In the mean time as I am waiting for him to double check my numbers, I am working on extracting the other half of my visual which is the annual catch rates of the Japanese flying squid by year to be used to find an estimate for maximum sustainable yield. I have been able to compile a couple of interesting resources. So catch rates are one thing, but how they are being caught, what kind of environment and size is another aspect. https://www.reuters.com/investigates/special-report/ocean-shock-squid/ is one such article that provides an interesting look into Japanese harvest of these squid. While the loss of this culturally important food source is tragic, a few things have been mentioned that Have caught my attention. Firstly, over many articles throughout this project there has been talk pertaining to the rise in temperature around Japan. This of course was teh inspiration for the temperature mapping itself. Further evidence supports the theory I have where these squid are spreading to different colder water areas. So it is noted in many cases that local squid is often much smaller than it has been in recent years. A possible reason as to why that is could be that fewer and fewer full grown adults are coming to these warmer waters. While it is true that the squid do return to the same warm waters they were born in to spawn and then die, as they grow into adults they search out colder waters to search for food. My theory is theyre not getting as many adults as they used to. They are reveiving squid that have not had the chance to migrate yet because they are being caught in the colder northern waters before they have the chance to make it back to spawn.

Japan in 2011 was bringing in 200,000 tons annually, but in 2017 Japan only brought in 53,000 tons which was the lowest recorded over the last 30 years. I am hoping to use the combination of these different intakes to really paint a detailed picture of the true rate of consumption this species is experiencing.

As for the mapping, I am going to try reaching out to other sources in order to find more reliable temperature illustrations. Even if I am unable to animate it, perhaps I can find some updated illustrations of fishing activity going northwards to illustrate the migratory pattern of these squid and thus fishing fleets.

4/21/2021

I have completed gathering data files for 2015-2020 of Chinese fishing vessels using squid jigging equipment. fish-r-man-main.zip

![image](https://user-images.githubusercontent.com/61677632/119078348-ff6c9700-b9c3-11eb-83d4-9666f257db22.png)


Now that I have it saved to my computer I was able to run some analysis on the data itself in terms of total fishing hours.

2015-2016 data pic 2016-2017 data pic

![image](https://user-images.githubusercontent.com/61677632/119078372-0f847680-b9c4-11eb-8893-9d1922510ba5.png)
![image](https://user-images.githubusercontent.com/61677632/119078380-14492a80-b9c4-11eb-939b-76df77858f49.png)


As you can see from my example, Chinese squid jiggers (at least those with AIS) have fished, during 2015, for a total of 443167.7 hours, with a mean of 0.7182412 hours. The respective measurements in hours (meaning the vessel transiting, loading/unloading, and other operations that are not fishing in themselves) are “Total: 1479917 hours” and “Mean: 2.398498 hours”.

It took awhile for me to download this data because as I started getting into 2017 and onward, the file sizes were getting larger and larger. By the time 2020 comes around, an entire years worth of active fishing hours is accomplished in a few months in years 2017 to 2020. My next step is to illustrate to the relationship between fishing effort and total annual catch to show if this is simply a demand increase or the effort is needing to be increased in order to acheive the same supply. This will give insight partially into the health of the stock in terms of showing maximum sustainable yield. As effort increases, catch should increase as well. This will happen until we reach a point where we are essentially taking more out than can be replaced. The area where we are able to take the max amount and the population stays relatively the same every year is what the maximum sustainable yield is. If we are taking more than can be replenished there is obviously the issue of the species going extinct but additionally in order to meet the demand of consumers more and more resources need to be dedicated to catching the same amount of squid. THis means an increase in cost not just for man hours but additional technology needing to be used in this case being distant water fleets. Countries like Japan and South Korea have already reported signigicant decreases in their local catch rate abd local communities are unable to dedicate the resources to seek these squid elsewhere. This behavior suggests there could be signigicant evidence to suggest revisiting the stock and reevaluating its threat level.

4/21/2021

2020 953976.6

Year 2019 Fishing hours 753955.8

2018 fishing 700491.5

2017 575223.7

I have been running into some issues finding exact numbers for annual catch rates over the last 5 years. I keep finding rough estimations over time. I am hoping that if I cannot find exact numbers that this information will be enough. The issue I am running into is since the late 90s the catch rate has remained relatively the same, only in the last three years have I found a reported jump in annual catch rates. The time spent fishing for China alone has increased by 100k hours each year. It does support the theory that although fishing effort has increased, the annual catch seems to remain pretty constant which is an indicator that the population is declining faster than it can replace itself. 

![image](https://user-images.githubusercontent.com/61677632/119078422-2925be00-b9c4-11eb-8176-2c7b5d377787.png)


I also was able to create an updated species range map since the one I had created for my presentation was a bit cut off and I wanted to make sure I had it for illustration purposes come my next presentation.

![image](https://user-images.githubusercontent.com/61677632/119078437-304ccc00-b9c4-11eb-8c9a-b4b341e4720a.png)

I am looking into accessing the data provided for me from a source by instatlling a program called FishStatJ that FAO uses to share their fishing data so that is exciting.

4/27/2021

Got the FishStatJ software up and running. I was able to narrow the data down into Cephalopods that China harvested:

![image](https://user-images.githubusercontent.com/61677632/119078451-3a6eca80-b9c4-11eb-8f7e-800e16d9f00d.png)

The only downside to that is as you can see only up until 2018 is reported, not 2018 or 2019.

![image](https://user-images.githubusercontent.com/61677632/119078474-45c1f600-b9c4-11eb-90de-5e62467f754c.png)

I have been working to create the visuals I need. These are the most recent years of fishing activity, and it is very obvious Chinas fishing activity is steadily creeping towards the US/Canada

2019 fishing activity 2020 fishing activity april 2021 fishing activity

![image](https://user-images.githubusercontent.com/61677632/119078505-52dee500-b9c4-11eb-8dfc-3f93f4ce6b9c.png)
![image](https://user-images.githubusercontent.com/61677632/119078514-57a39900-b9c4-11eb-9e57-afbdaafc0038.png)

![image](https://user-images.githubusercontent.com/61677632/119078528-5e321080-b9c4-11eb-81d3-1b19ffedec98.png)

The above images are 2019, 2020, and 2021 from top to bottom. They are captured during the warm mid year months, and the 2021 frame specifically was the activity tracked in early April 2021.


![image](https://user-images.githubusercontent.com/61677632/119078576-786bee80-b9c4-11eb-8c97-94015305ef2c.png)


This is the temp map for April 2021 and this activity is happening in the temperature gradient that is in this animals distribution range.

Currently creating a maximum sustainable yield model using some tutorials.

https://github.com/laurieKell/COM/blob/main/README.md https://www.youtube.com/watch?v=x8YvhC1d4kc

4/28/2021

A MODEL HAS BEEN BORN...sorta

In theory it works but in order for this to create a more accurate idea of MSY and also a more accurate model of the future I need more points.

![image](https://user-images.githubusercontent.com/61677632/119078610-8752a100-b9c4-11eb-853b-915f9b85e0ec.png)


image

Above is the theory of more effort = less catch over time in mathematical terms. At least I have math and a trendline to go with what I am saying, But I am going to need all of the years of data for this to be more effective.

2012 59437.34 2013 178831.6 2014 308657.2

5/2/2021

I DID IIIIIIIIIIT

So here is my forecast for the next 5 years

![image](https://user-images.githubusercontent.com/61677632/119078640-946f9000-b9c4-11eb-94df-dbb28604c956.png)

![image](https://user-images.githubusercontent.com/61677632/119078654-9b969e00-b9c4-11eb-983f-6302f57689bc.png)

Using excels forecasting tool this is the forecast of how much annual catch China will receive in the next 5 years based on previous catch data.

I also have another forecast in regards to fishing effort

![image](https://user-images.githubusercontent.com/61677632/119078672-a5b89c80-b9c4-11eb-8f95-8c30a59be115.png)

![image](https://user-images.githubusercontent.com/61677632/119078683-ad784100-b9c4-11eb-9011-1c8d3a9c5fdb.png)


I decided to compare the results of this forecast to actual data I had to show how accurate this forecast is.

Shown above are the forecasted values for 2019 and 2020. The actual values of effort for 2019 and 2020 are 1121.9 and 1419.6. This is a difference of 69.8102 from the forecast value for 2010 and 23.23 from the upper bound for 2020. This forecast is fairly accurate, within the bounds of the forecast and the upper limit which suggests if something is not done, the species will move close to extinction.

Currently exploring effort cost vs catch rate. So the market rate for this species is between $500 and $1000 per metric ton.

![image](https://user-images.githubusercontent.com/61677632/119078714-bb2dc680-b9c4-11eb-899b-a86e919c137e.png)

The only other issue I am running into is the volume of catch. The original estimation of total catch has been retracted from https://www.mcsuk.org/goodfishguide/fish/784#:~:text=Stock%20information-,The%20Japanese%20flying%20squid%20fishery%20is%20one%20of%20the%20most,to%20500%2C000%20t%20per%20year.

this data although being the very first Google result when searching for how much Japanese Flying Squid is caught each year, the website states the data is being reviewed and lists nothing for the species.

This is further complicated by Japans national quota being 60,000 tons, when their annual catch rate the last few years is around 40,000 t obviously way below their allowed catch. China is said to account for 50 to 70% of total squid caught which is reported by a number of journalistic sources, which does make sense if we consider the possibility of unregulated fishing.

To run it through some simple math in terms of worth, I found a few current stock prices from Chinese veondors. The estimate is between $500 and $1000 per ton. Lets assume its $1000 per ton for arguments sake.

FAO states China reports 41854 tons for 2018, and GFW data shows that year for squid jiggers the fishing effort (total hours spent actively fishing, does not include transit time, gear maintaining, offloading catch etc.) was 700491.5 hours.

The total catch was worth $41,854,000. This means ships made roughly $59.75 an hour for fishing time. A large scale squid jigger can have around 30 crew members. if we assume half is taken for upkeep that would mean crew would only be making $1 an hour of active fishing effort (no gear care, maintaining etc.)

5/6/2021

![image](https://user-images.githubusercontent.com/61677632/119078745-caad0f80-b9c4-11eb-86ec-3f02411d10c3.png)
![image](https://user-images.githubusercontent.com/61677632/119078761-d3054a80-b9c4-11eb-8596-f79c56bbb37c.png)
![image](https://user-images.githubusercontent.com/61677632/119078775-d993c200-b9c4-11eb-8872-f1eb728de7cd.png)


Above are my completed maps for the last few years showing a trend in shift of warming seas and steady movement East towards the USA.

![image](https://user-images.githubusercontent.com/61677632/119078784-de587600-b9c4-11eb-85fd-a63ae3e5c485.png)
![image](https://user-images.githubusercontent.com/61677632/119078806-e6b0b100-b9c4-11eb-913f-4485046abe1d.png)
![image](https://user-images.githubusercontent.com/61677632/119078831-f29c7300-b9c4-11eb-8c55-abab2c604c62.png)



Above are the data snapshots I took from the FAO database of a few different countries regional to the Japanese Flying Squid. Even the Russian Federation who takes very little still reports the specific species "Japanese Flying Squid".

Over the last few years 2012 all of these countries including China Korea Japan and Russia have all been taking a steep downturn in Squid catch. The biggest difference between all of them is everyone except China is reporting the specific species catch number which is required by the United Nations agreement. China reports partial information such as mollusk catch or cephalopod catch. They report "Jumbo Squid" but that is the common name for Humboldt squid.

I look into the effort because they put in a massive amount compared to the actual cash that they get. In terms of fishing hours tryna is only getting less than a dollar an Hour of Revenue. Even though at its highest the catch is worth about 45 million dollars per year it would be very difficult to pay wages and pay maintenance and fuel for these vessels. This opens up the idea of slave labor on the ships but also the fact that I think they are hiding their numbers and Reporting them incorrectly. So not all mollusks are cephalopods but all cephalopods are mollusk. I think what's happening based on the amount of Revenue they're not receiving, the hours of effort spent, and the reported numbers from all countries showing the same steady decline in catch rate all falling around 40 to 45 thousand tons, I think China is reporting their catches incorrectly so that it appears they are suffering from the same decline of catch as the other countries because their catch rate annually for mollusk are in the hundreds of thousands of tons. These include a wide variety of species including octopus, bivalves, and sea snails. Of course they do catch these as well it is a popular stock but it is easy to hide numbers by reporting them in this manner

Basically no matter what change needs to happen. This species is being taken faster than it can be replenished. However, if China continues to report their catches incorrectly and regulation is put in place worldwide to limit these catches; because China is not reporting specific species they could still continue to fish at the rate that they do while reporting it as something else, such as a general "mollusk" or even a different species like the Jumbo Squid.

That would mean as the other countries are cooperating and taking far less than they normally would, this squid is being sold at a premium by China because of the regulation and they would never feel the economic loss because the entire time it was reported as a mollusk catch and sale.

I have significant evidence to suggest that China not being held to the same reporting standard as these other countries puts every country at a direct economic and resource disadvantage. Additionally, they are willing to go to great lengths to ensure this growth continues including aggressive behavior, secretive tactics, uncooperate fisheries management, invasion of economic exclusive zones, and now they are slowly but surely moving their way East in search of their next catch.
