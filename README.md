# Starbucks_Capstone
Starbuck's Capstone Challenge

Purpose:
Starbucks is the largest coffee chain in the world. They are constantly innovating new ways for consumers to spend more money. In this data analysis, I will be analyzing Starbucks databases on customers and their spending habits. From analyzing the data, I will provide some visualizations and recommendations based upon the results.


Data Set Overview:

The program used to create the data simulates how people make purchasing decisions and how those decisions are influenced by promotional offers.
Each person in the simulation has some hidden traits that influence their purchasing patterns and are associated with their observable traits. People produce various events, including receiving offers, opening offers, and making purchases.
As a simplification, there are no explicit products to track. Only the amounts of each transaction or offer are recorded.
There are three types of offers that can be sent: buy-one-get-one (BOGO), discount, and informational. In a BOGO offer, a user needs to spend a certain amount to get a reward equal to that threshold amount. In a discount, a user gains a reward equal to a fraction of the amount spent. In an informational offer, there is no reward, but neither is there a requisite amount that the user is expected to spend. Offers can be delivered via multiple channels.
The basic task is to use the data to identify which groups of people are most responsive to each type of offer, and how best to present each type of offer.


Data:
profile.json
Rewards program users (17000 users x 5 fields)
gender: (categorical) M, F, O, or null
age: (numeric) missing value encoded as 118
id: (string/hash)
became_member_on: (date) format YYYYMMDD
income: (numeric)
portfolio.json
Offers sent during 30-day test period (10 offers x 6 fields)
reward: (numeric) money awarded for the amount spent
channels: (list) web, email, mobile, social
difficulty: (numeric) money required to be spent to receive reward
duration: (numeric) time for offer to be open, in days
offer_type: (string) bogo, discount, informational
id: (string/hash)
transcript.json
Event log (306648 events x 4 fields)
person: (string/hash)
event: (string) offer received, offer viewed, transaction, offer completed
value: (dictionary) different values depending on event type
offer id: (string/hash) not associated with any "transaction"
amount: (numeric) money spent in "transaction"
reward: (numeric) money gained from "offer completed"
time: (numeric) hours after start of test
Method
I will be using the following methods to analyze the data to determine the spending habits of Starbucks customers
Data Cleaning
Data Analysis
Data Interpretation and Visualization
Data Cleaning:
The first spend to clean the data. We will start off with the portfolio.json file. 

The channels column will be broken down into individual columns. The offer id code will be converted to an assigned integer value for ease of viewing the data. The offer_type column will also be broken down into individual columns. The result is the following dataframe.


Next is the profile.json file.

For this data, we will convert all age 118 to NaN values. Customer id will be converted to an assigned integer value for ease of viewing. Became_member_on will be converted to a datetime value and converted to the number of years they have been members. All rows with NaN will be dropped.  The following is the result.



Last is the transcript.json file. 


For this data, I will take the customer’s id from the person column and assign an integer value for ease of viewing. The result will be the following.


Data Analysis:

To understand the data, we will need to analyze it. The first process is to break the transcript into two separate dataframe. The first is offers and the second is transactions.

Offer dataframe all event columns with the offer received, offer viewed, and offer completed events. Then, I will take the value column and extract the offer id and convert it to an assigned integer from the data cleaning process. Then, I will merge that dataframe with the clean portfolio and profile dataframe and the result is the following. 


I will do the same with the transaction dataframe, except we will filter only the event with a transaction. The transaction doesn’t have an offer id associated with it, but instead, I will extract the transaction amount from the value column. The result will be the following. 


Data Interpretation:

From the data analysis and visualization, I made the following observations on the customers spending habits. 
Females spend the most per transaction, spending an average of $17.50, while males spend less than $12.
Females spends about 50% more than males and Others spend 25% more
For total sales, Males and Females are roughly the same. This is due to having more Male customers and them making more transactions. Males make about 50% more transactions than females.
The middle income are the ones that spend the most in terms of total spent at Starbucks ($60k−$80k), but the upper class spends more per transaction.
There is no correlations between the success of a promotion and income, age, or member_length
Discount offer #4 and Information offer #2 both failed with zero completions
Because I don't have further information on the promotion, I could not determine why it failed
Bogo #3 was the most successful out of all the promotions
Overall, both Bogo and Discount promotion have about the same number of completions. Bogo had 10,156 completions, while Discount had 10,170 completions. Both had a completion of 38%.
There is no visible correlations between the success of the promotion and difficulty, duration, or reward
 
Recommendations:
The two target groups are females and upper income groups. They spend more per visit but they visit less than the other groups. If we could get them to visit more, the revenues will increase.
The largest customer group are middle income males, but they send less per visit. Suggest finding ways to increase spending per visit for this group.
Because there is no correlations between Income, Age, and Member Length, it is recommended not to target a particular customer profile
Since both promotion results are almost identical and with a completion of 38%, it is recommended to continue with both promotions.
If we could find why the offer discount #4 did not get any completion, Discount promotion might have the edge, since #4 dragged down the numbers.
 

