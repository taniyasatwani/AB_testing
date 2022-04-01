# AB_testing

A/B testing (also known as split testing or bucket testing) is a method of comparing two versions of a webpage or app against each other to determine which one performs better.

# Motivation

A/B testing allows to make careful changes to their user experiences while collecting data on the results. This allows them to construct hypotheses and to learn why certain elements of their experiences impact user behavior. In another way, they can be proven wrong—their opinion about the best experience for a given goal can be proven wrong through an A/B test.

More than just answering a one-off question or settling a disagreement, A/B testing can be used to continually improve a given experience or improve a single goal like conversion rate over time.

# Dataset

The dataset is taken from the [Kaggle](https://www.kaggle.com/saraabdelaal/abtestdata). Each row is logged when user is exposed to a webpage. 

   • `User_id`: id of user exposed to webpage
   
   • `timestamp`: time the user is first exposed
   
   • `group`: bucket
   
   • `landing_page`: Which page are they seeing
   
   • `converted`: Initialized to 0. Changes to 1 if the user makes a purchase within 7 days of first exposure
   
# Overview

There are some repeated exposures for some users. Same users have been exposed to control and treatement. 

Get timestamp of first exposure. Remove users with multiple buckets.

1.32 % user_ids have been exposed to both versions. It should be okay to remove them.

Created a new column which contains the week number.


**Get Started**

1. `Frequentist Approach` - Used `Chi-Squared Test` .

`H0` = control and treatment are independent

`H1` = control and treatment are not independent

p_value > 0.05, we cannot reject null hypothesis. Hence, we cannot conclude if there exists a relationship between the control and treatment groups.

21.61% probability that a more extreme chi square than 1.53 would have occured by chance. But this is tough to interpret. We cannot say something about the actual maginitude of lift. Something like this: We are 21.61% confident that our lift = -0.148%

Thats why we use Bayesian Approach.

2.  `Bayesian Approach` - We want to input the prior distribution and have the experiment update the parameters to create posterier distributions. Since these prior & posterior distributions will be used to sample Conversion Rate, we model them after 'Beta distribtion'.

Created the `prior beta distribtion` from the first weeks of conversion data

Created `posterior beta distribtion` from second to fourth weeks of conversion data. Updated Prior parameters with experiment conversion rates.

Probability that treatment > control: 15.4%. lift = -0.0121. Probability that we are seeing a 1% lift: 3.5000000000000004%

**Advantages of Bayesian over Frequentist:**

 • Results are more interpretable than the ones we got from the frequentist approach

 • We can interpret results at any point during the experiment. Don't need to wait for an arbitrary "statsig"
