
# Wrangle and-Analyze DAND4
I will be gathering, assessing and cleaning three datasets about the WeRateDogs twitter account, I will then analyze and make visualizations on the datasets.

## WeRateDogs
Is a twitter account that posts images of dogs and rates them out of 10, but always gives them over 10, because well... they are dogs.
![ExampleTweet](https://user-images.githubusercontent.com/121340570/227718758-e3aa3cca-66f4-4805-80e4-813f370da45e.PNG)

## Data Gathering
The first and most vital step in a data related project is collect and gathering the data. I collected the twitter data in 3 different ways:
1. Manuelly downloaded the WeRateDogs Twitter archive.
1. Utilised the Python Requests library to programmatically download the image predictions file.
1. Used the Tweepy library to query additional data via the Twitter API 

## Data Assessment 
In this section I assessed the data to find the following quality and tidiness issues:
### Quality issues
1. There are 59 tweets with NaN values for expanded_urls, therefor not having hyperlinks, images, in the tweet.
1. The dog types and names columns have "None" string but instead should have NaN literal.
1. There are 109 incorrectly named dogs with 25 different names such as "officially", "actually" and "infuriating".
1. timestamp column in tweetDF is a string object, should be converted to datetime instead.
1. Values in the source column in the tweetDF all have their HTML tag, it is unnecessary.
1. There are 25 dog ratings which had a number greater than 20 on the rating_numerator, such as (749981277374128128) with a numerator of 1776, these are outliers and should be removed.
1. There are 3 tweets with rating_denominator less than 10, (835246439529840640) does not have a url, (810984652412424192) does not have a rating in the original tweet, and (666287406224695296) rating should be changed from 1/2 to 9/10
1. There are 20 tweets with rating_denominator more than 10, (716439118184652801) is rated 50/50 but is actually rated 11/10. (740373189193256964) is rated 9/11 but should be changed to 14/10. (722974582966214656) is rated 4/20 but should be changed to 13/10. (820690176645140481) is rated 84/70, inspecting the images I can see that there are 7 identical sibling dogs. (758467244762497024) and (709198395643068416) are rated 165/150 and 45/50 respectively, inspecting the images I see that the tweets have many dogs and their ratings are combined, it is impossible to tell how the ratings divide, they and the remaining tweets can be removed.
1. Tweet (775096608509886464) is a retweet of tweet (740373189193256964) and is identical to it, it has the same images and rating, retweets are redudant and should be removed, there are a total of 181 retweets.
1. There are 66 duplicated rows, in the predictDF.

### Tidiness issues
1. There doesnt seem to be a need for both the rating_numerator and rating_denominator columns, especially if the denominator is supposed to be 10.
1. The last four columns in tweetDF store the dogs 'stages', unless a dog can have more than one these types, they should be combined to one column
1. Only 3.3% of the tweets are replies, leaving the rest of the tweets with many null values in in_reply_to_user_id and in_reply_to_status_id, knowing the tweet is a reply doesn't tell us much and the two columns can be removed

I will then clean the data to finally be able to analyse it.

## Data Analysis
Finally I analyzed the cleaned data to come up with the following
Insights:
1. The average rating out of the dogs from the tweets is 10.5 out of 10.
1. The most puppolar dog type is pupper with a total of 202 dogs, followed by doggo with 63, then puppo at only 22, and finally, the cutest but least puppolar is floofer with only 7 dogs out of 1963 dogs.
1. The most common dog names are Charlie, Oliver, Cooper, Lucy, Tucker and Penny.
1. The tweets on average get 8880 favorites and 2754 retweets and the most retweeted tweet got 132810, the tweet that was favorited the most had 79515
1. The tweets are almost always sent from an iPhone, with 1925 tweets being from an iPhone, 28 from a computer, and 10 from TweetDeck, which is mostly used on computers.
