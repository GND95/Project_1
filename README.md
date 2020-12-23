# **Likelihood of a Song's Success based on data from Spotify.com**

[Slide deck can be viewed here.](https://docs.google.com/presentation/d/1lfFaDlzlLJSnwwdW48frCWP-94sbd6hQf_a-5uC0Dzk/edit#slide=id.p)

## **Hypothesis:**
Using statistical analysis, we can predict some of the traits which can contribute to the overall success of a song in today’s market.

## **Motivation**
This year, while Spotify did take an early hit in revenue as lockdowns began, they quickly rebounded and returned to their pre-pandemic projected growth rate- quite a feat for a "non-essential" service at a time when money is tight for many users! [Source](https://variety.com/2020/digital/news/spotify-q1-2020-gains-6-million-subscribers-coronavirus-1234592814/) In many cases, streaming is an easy and cheap way for customers to keep their media libraries fresh and interesting in a time when we’re using those libraries more than ever, which means it’s a richer-than-ever data source to learn about the most current media trends. We were curious what we could learn about these trends from a very up-to-date dataset.

## **Questions examined:**
- What music genres are most popular right now?
- What genres are most popular across the last 10 decades?
- Does the number of performers on a song have an effect on the song's success?
- How many collaborators is the right number of collaborators on a song?

## **Source:**
[Spotify Dataset 1921-2020, 160k+ Tracks](https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks?select=data.csv) ([Yamaç Eren Ay](https://www.kaggle.com/yamaerenay)) 

*Note: While the title of this dataset says 160k+ songs are included, the dataset now actually contains over 170k songs, which is why 170k is mentioned in the presentation.*

## **DATA CLEANUP AND EXPLORATION**

This dataset is rich with information, but presents some unique challenges when examining artists and genre, which were two of our areas of focus.

To begin with, we realized that Garrett and Sarah's areas of study on genre required information from two separate .csv files, but those two files had very little in common. After some examination, Irene discovered that the files could be merged along the artist column and created a single .csv containing all the necessary information.

Before:
<br/> ![Screenshot of uncombined .csv files](/Resources/README_images/combine_csv_files.png)

After:
<br/> ![Screenshot of combined .csv files](/Resources/README_images/combine_csv_files2.png)

For Kelly's portion of the research, she needed to know the number of performers on each song in the dataset. Initially, she intended to use the len() function to get the value of each list of artists in the column and return the len() values to a new column; unfortunately, we quickly found out that while the artist column appears to be formatted as lists of artists, each entry is actually formatted with strings. After some attempts at converting the strings to lists, she decided that the simplest solution sometimes really is the best and realized that the artists themselves were separated by commas within the strings. By counting the number of commas in each artist string and adding 1, she could get a count of the total number of artists on a track.

Before:
<br/> ![Screenshot of file showing the "artist" column strings and the new column listing the number of collaborators](/Resources/README_images/collab_count.png)

Analyzing genre presented an especially daunting task, as the dataset categorizes most songs with several hyper-specific genre names rather than one overarching category. To solve this, Garrett realized that most of these subgenre names included the name of an overarching category within them:

<br/> ![Screenshot illustrating how a mode() search for the most common word in each song's "genre" list tends to return a valid, broad category](/Resources/README_images/genre_finder_explainer.png)

For most songs in the dataset, using the mode() function to deterimine the most-repeated word in the "genre" column would tell us the broad category to which the song belongs- but not for all of them. As you can see in the example above, some genre lists return no repeated words. In those cases, we initially defaulted the songs to an "Eclectic" category. However, further examination revealed that certain genres did appear in these "eclectic" songs more than others. To address this, Garrett used nested If/Else statements to test if a song belonged to one of these common categories before ultimately labeling anything as eclectic. Here is an illustration of how this function works:

<br/> ![Flowchart illustrating how the genre finder code functions to assign genre to songs in the dataset](/Resources/README_images/genre_function_flowchart.png)

Using this solution, Garrett was able to parse the genre trends within our dataset.

Within our dataset, Sarah primarily explored the relationship of the audio features of each track as defined by Spotify and their prominence over time by extensively charting linear regressions, some of which are pictured below.

<br/> ![A screenshot showing just a few of the linear regressions performed on audio features in this dataset](/Resources/README_images/linregress_examples.png)

## **DATA ANALYSIS & DISCUSSION**

Using the above listed methods, we were able to calculate and visualize trends demonstrated in this dataset, such as:

* Across all of our data, "rock" is easily the most popular of the defined genres.
* Given more time, more exploration could have been done into songs that landed in the "Eclectic" bucket to discover more specific genre and sub-genre trends.

<br/> ![Screenshot of charts showing "rock" as the most common defined genre within the dataset](/Resources/README_images/genre_trends.png)

* Nearly all of the audio features defined by Spotify have trended clearly and positively over the past 100 years of music releases (see linear regressions above)
* Notable exceptions to this trend include "instrumentalness", "explicitness", and, "speechiness". Speechiness's weak positive trend surprised all of us, as there has been such an explosion of rap and hip-hop over the past 30 years, and is something we would like to examine more closely given more time.

<br/> ![Screenshot of the surprises discovered during regression analysis of audio features](/Resources/README_images/audio_feature_surprises.png)

* Songs featuring more than one performer were more highly concentrated in the top 5% most popular songs in the chart than in the chart as a whole.
* In particular, duets are approximately 6% more concentrated in the 5% most popular songs in the dataset compared to the dataset as a whole
* This was surprising, as songs with more than one artist only make up about 20% of the dataset as a whole, and duets only make up around 14% of the dataset as a whole.
* This implies that, in the current market, there is less competition and more opportunity for success for duets than solo songs or songs with three or more credited artists.
* Given more time, I would be interested in studying the absolute and relative popularity of the artists performing these duets, as well as the effect of genre on duet popularity, to really hone in on what kind of duet has the best shot at success.

<br/> ![Screenshot of two pie charts illustrating the breakdown of solo, duet and 3+ performer songs in the dataset as a whole vs the top 5% most popular songs in the dataset](/Resources/README_images/collab_percentages.png)

## **POST MORTEM**
We experienced and successfully managed a number of challenges with our dataset, which are outlined in the sections above, along with some of the surprising discoveries we made along the way.