# Capstone Project - GOAT Talk

## Technical Report
**********************************************************************************************************************************


## The Problem
Basketball is my favorite sport.  If you know where that line came from, then kudos to you.  I have been around the game in some form or fashion all of my life.  I grew up watching the Lakers vs Celtics playoff battles, which is what drew me into the Los Angeles Lakers. #Showtime #LakeShow  I watched Dominique Wilkins get **ROBBED** of a Slam Dunk Championship by Michael Jordan and the foot-on-the-free-throw-line "Free Throw Line" dunk that he's famous for.  But the thing that always gets discussed is who the Greatest Player of All Time is.  Is it the NBA career scoring leader, Kareem Abdul-Jabbar?  Is it the Point God and template for what brought the NBA into the must-see ticket of 1980's?  Michael Jordan....His Airness?  Or could it truly be the self-crowned King, Lebron James?  For the longest time, most of the takes were opinion based.  Some were off of the numbers, but hard to dictate which players were more important than others.  The goal is to use the
many facets of data science to determine who the best player of all time truly is.

## "Take That For Data" - David Fizdale
The most important piece of this project is of course, the data.  But in order to get proper data, I had figure out who I would be looking for and what exactly I would need to find for each person.  So, I came up initially with a list of 11 players who would be considered the best of ALL TIME!!!!  This list is as follows: Kareem Abdul-Jabbar, Earvin "Magic" Johnson, Larry Bird, Isiah Thomas, Michael Jordan, Hakeem Olajuwon, Shaquille O'Neal, Kobe Bryant (my personal pick for GOAT, but I wouldn't allow personal bias to affect data), Tim Duncan, Lebron James, and Kevin Durant.

Now, I had to pick where to find the proper information needed could be obtained.  First thought, was https://stats.nba.com and searching for each player that way.  I ended up going with https://basketball-reference.com for all of my NBA data.  Next was deciding what statistics to pull.  I started with the basic Per Game statistics: Age, Games Played, Minutes, Field Goal % (Made and Attempted #), 3-Point FG % (Made and Attempted #), 2-Point FG % (Made and Attempted #), Effective FG %, Free Throw % (Made and Attempted #), Offensive Rebounds, Defensive Rebounds, Total Rebounds, Assists, Steals, Blocks, Turnovers, Player Fouls, and Points.  After that, I wanted stats that required a bit more of a formulaic approach.  So I went to the Advanced section and looked for the following: Player Efficiency Rating (PER), True Shooting %, Total Rebounding %, Assist %, Steal %, Block %, Turnover %, Usage %, Win Shares, Offensive Box +/-, Defensive Box +/-, Overall Box +/-, and Value Over Replacement Player (VORP).

With most NBA statistics websites not having an API or an easy way to grab the data, a method to grab the data was needed.  My first plan was to use web scraping, but the Advanced section was not allowing a basic pull through Requests and BeautifulSoup.  So, I did a little researching and learned about Selenium.  Because the extra data was located within comments section of the html file, and Requests and BeautifulSoup could not pull it themselves, Selenium was able to grab any and all data within the table requested.  Once the Per Game and Advanced data was scraped, collected, and placed into data frames, I decided I wanted to add a little more to the dataset.  I added the seasons played, MVP info (when did they win MVP, where did they place in the voting, what shares of votes did they receive), playoff appearances, NBA Championships won, and All-Star game appearances.  Once this was added and the appropriate columns were created, I had to take the scraped data and convert from string to an integer or float format.

Then, it was merge the Pre Game with the Advanced, and that gave me the Player Data.

Next, cleaning the data.

As I started with Kareem's info, I could see that there were some major issues.  The major issue with Kareem's stats was that stats like Steals, Blocks, Offensive Rebounds, and Defensive Rebounds were not an official tallied statistic until the 1973-1974 season. Also, Turnovers were not tallied until the 1977-1978 season. Much of his data will be skewed in these 5 categories. Luckily, there was no 3-Point line until the 1979-1980 season, so we can leave that as 0 in all categories. With so many columns full of inconclusive data, my only option would be to fill in with either false data from averages. So, I decided to leave him off of my comparison and use other players that could be considered all-time greats.

I wanted to pick players that matched similar playoff appearances, MVP voting shares, etc. I included Allen Iverson, Dirk Nowitzki, Dwyane Wade, and Stephen Curry.  I followed the same procedure that I did with the previous 11.

Once they were in the proper format, I checked each player for any null values.  Most were from 3-Point where they had no makes or attempts, but the value was not filled in for percentage as 0.00.  After completing, I added their nicknames as identifiers to use for indexing and then saved the cleaned data as .csv for later use.

I opened another Notebook and strictly used this for EDA purposes.  I merged all of the .csv into 1 dataframe.  Then I narrowed down some of the data gathered for the modeling.

There were 214 rows of data collected between 14 NBA players to start with.  I narrowed it down to those who played at least half of a 82-game season and that dropped our data from 214 to 202 rows.  Then I wanted only the PER scores that were above the league average of 15.  That took the data from 202 to 196.  From there, it was adjusting some of the percentage stats into decimal format (25% = .25).  After that, nothing left to do but some graphing and plotting to see what the data looks like amongst each other.


## "I am not a Role Model" - Charles Barkley
The easiest way to compare was simply by using graphs and plotting from Age to some of the other features.  Option 2 was to run regression modeling and use PCA to combine the features and try to keep from overfitting.

## Evaluation
Linear Regression appeared to have the best score and the predictions were not far off