# **Capstone: Topic modeling on Amazon customer support**

**Table of Content:**

- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Dataset](#Dataset)
- [Pre Processing](Pre_processing)
- [EDA](EDA)
- [Modelling](Modelling)
- [Conclusion and Recommendation](Conclusion and Recommendation)



# **Problem Statement**

Amazon is the one of the world's biggest e-commerce platform. Apart from its own platform, Amazon has different channels of customer support. Twitter is one of them. Amazon has a customer suport account on Twitter called @Amazonhlep. It is not surprise that the volume of customer requests is huge. In 2017 , there are nearly 100K tweets on AmazonHelp. With such a high volume, maintaining the quality of the customer support would be challenging.

This project aim at having a better allocation of customer support workforce by identifying the intent of customer. The intention of customer will be categorized into different topics and then we can restructure the customer support team into sub team based on these topics.  Ultimately, to triage and route the customer support reqeusts to appropriate sub team in order to provide a more efficient customer support.

# Executive Summary

No business can survive without customers. This reflects on the mission of Amazon, one of the world's biggest e-commerce platform, “to be Earth’s most customer-centric company" and the award-winning Customer Service team is an essential part of this mission. This is why maintaining the quality of the customer support is crucial to Amazon.

### Why Twitter?
Firstly, Twitter can be a big showcase for Amazon customer support. It is a globally well known social mdeia platform and it had more than 321 million monthly active users as of 2018. Unlike Amazon 's own customer support platform,  Everyone can see other people's compliant or request on AmazonHelp (Amazon's customer support on Twitter). Because Twitter's primary purpose is to connect people and allow people to share their thoughts with a big audience.If we can provide good quality and efficient customer support,it also facilitates to positive brand image.

Secondly, Twitter aims to create highly skimmable content for our tech-heavy, attention-deficit modern world. Thus, Tweets can be only up to 140 characters long. The short conversation is similar to live chat. Users contact customer support to have a specific problem solved, and the manifold of problems to be discussed is relatively small, especially compared to unconstrained conversational datasets like the reddit Corpus. Understanding the tweets pattern helps us to understand the talking pattern of the users nowaday. And this project explores Twitter as a pioneer porject. We can start from Twitter first and then explore to other customer support platform such as Facebook, email.

### Key findings

1. Presence of non English tweets such as Japanese, Spanish, German as AmazonHelp support foreign languages.
2. spam tweets, a single users contribute to 417 tweets alone. The tweets accross 2015-2017
3. 99% of the tweets are requested in 2017 
4. Oct,Nov and Dec has the most tweets. prioritize these three months.
5. The SLA(Service Level Agreement) of AmazonHelp is around 13 mins.It can be the baseline of SLA. And when the tweet volumn are high in Oct, Nov and Dec. The SLA should be shorter than 13 mins. 

# Dataset
The dataset  [Customer Support on Twitter](https://www.kaggle.com/thoughtvector/customer-support-on-twitter) is from Kaggle. It offers a large corpus of modern English (mostly) conversations between consumers and customer support agents on Twitter.

The dataset consists of the tweets refer to 108 different companies. AmazonHelp has the highest number of tweets. In this project, I will only focus on @AmazonHelp 's tweets. 



### Data Dictionary

| Features                  | Description                                                  |
| ------------------------- | ------------------------------------------------------------ |
| `tweet_id`                | A unique, anonymized ID for the Tweet. Referenced by `response_tweet_id` and `in_response_to_tweet_id`. |
| `author_id`               | A unique, anonymized user ID. [@s](https://www.kaggle.com/s) in the dataset have been replaced with their associated anonymized user ID. |
| `inbound`                 | Whether the tweet is "inbound" to a company doing customer support on Twitter. This feature is useful when re-organizing data for training conversational models. |
| `created_at`              | Date and time when the tweet was sent.                       |
| `text`                    | Tweet content. Sensitive information like phone numbers and email addresses are replaced with mask values like `__email__`. |
| `response_tweet_id`       | IDs of tweets that are responses to this tweet, comma-separated. |
| `in_response_to_tweet_id` | ID of the tweet this tweet is in response to, if any.        |



# Pre Processing 

We do the data cleaning  by removing :

- contractions e.g 'wasn't' will be changed to 'was not'
- uppercase letter
- html
- punctuation
- filtering non English tweets

Three pre-processing with different libraries after the data cleaning 

1.SpaCy custom pipelines

2.NLTK and bigram/trigram by gensim

3.a function `tweet_cleaning` defined specially to deal with the tweets chating pattern.



# EDA

EDA includes find the top 30 words of each pre-processing ways and visualise in bar plot and word clouds, among these top words, I will see if the top words are providing insight. If there are any meaningless words, I will add them into the stop words list. These new stop words list will be use in the second and third way of pre-processing.



# Modelling

Topic modelling using LDA (Latent Dirichlet Allocation)

Preparing Data Transformation for Corpus and Dictionary

Comparing the coherence score of each pre-processing way for 3-10 number of topics

Tuning hyperparameter : alpha and eta(beta) for a higher coherence score



# Conclusion and Recommendation 

LDA helped to categorize 4 main topics, they are inferred to be :

Topic 0 : account issue - email follow up

Topic 1 : delivery - with Prime account

Topic 2 : membership and complaint

Topic 3 : refund and product return

### Recommendation :
To restructure the customer support team into sub team based on these 3 topics.
For example, we can have a sub team dealing with account issue. The second team will be responsible for Prime account. The third team will be dealing with compliant. The forth team is in charge for refund and product return. 
And the peak season is in Oct, Nov and Dec, be aware of the allocation of staffs and the SLA.



# Limitation and Improvement

1. The impact of the non english tweets such as Spanish and German tweets shown on Topic 1. The words are more likely in German, Spanish or French. I made a wrong judgement of keep them in the first place.
2. Examining tweets is challenging as it only has a short length of converstaion. And because of the business nature of Amazone is e-commerce. It seems that most of the requests are related to order delivery.
3. The coherence score are low. The highest are 0.44 after tunning. Also the hyperparameters setting is not able to provide the best outcome of LDA. In this part, it is definitely that I could have done better.



## Future work

For future work, I would like to do the following : 
1. Emoji analysis 
2. Sentiment analysis - to understand the painpoint and to enhance 
3. Multiclass Classification - to predict of the request topics so to have a forcast of workforce allocation,to work more intelligently and to prioritize the requests 







