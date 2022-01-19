What is a Funnel?
In the world of marketing analysis, “funnel” is a word you will hear time and time again.

A funnel is a marketing model which illustrates the theoretical customer journey towards the purchase of a product or service. Oftentimes, we want to track how many users complete a series of steps and know which steps have the most number of users giving up.

Some examples include:

Answering each part of a 5 question survey on customer satisfaction
Clicking “Continue” on each step of a set of 5 onboarding modals
Browsing a selection of products → Viewing a shopping cart → Making a purchase
Generally, we want to know the total number of users in each step of the funnel, as well as the percent of users who complete each step.

Throughout this lesson, we will be working with data from a fictional company called Mattresses and More. Using SQL, you can dive into complex funnels and event flow analysis to gain insights into their users’ behavior.
[![N|Solid](https://content.codecademy.com/courses/sql-intensive/funnels.svg)](https://nodesource.com/products/nsolid)

### Build a Funnel From a Single Table
Mattresses and More users were asked to answer a five-question survey:

“How likely are you to recommend Mattresses and More to a friend?”
“Which Mattresses and More location do you shop at?”
“How old are you?”
“What is your gender?”
“What is your annual household income?”
However, not every user finished the survey!

We want to build a funnel to analyze if certain questions prompted users to stop working on the survey.

We will be using a table called survey_responses with the following columns:

question_text - the survey question
user_id - the user identifier
response - the user answer

```sql 
select question_text, count(distinct user_id) from survey_responses
where response is not null
group by 1
```
### Survey Result
We could use SQL to calculate the percent change between each question, but it’s just as easy to analyze these manually with a calculator or in a spreadsheet program like Microsoft Excel or Google Sheets.

If we divide the number of people completing each step by the number of people completing the previous step:

| Question | Percent Completed this Question |
| -------- | ------------------------------- |
| 1        | 100%                            |
| 2        | 95%                             |
| 3        | 82%                             |
| 4        | 95%                             |
| 5        | 74%                             |

We see that Questions 2 and 4 have high completion rates, but Questions 3 and 5 have lower rates.

This suggests that age and household income are more sensitive questions that people might be reluctant to answer!
[![N|Solid](https://content.codecademy.com/courses/sql-intensive/survey.svg)](https://nodesource.com/products/nsolid)

### Compare Funnels For A/B Tests
Mattresses and More has an onboarding workflow for new users of their website. It uses modal pop-ups to welcome users and show them important features of the site like:

Welcome to Mattresses and More!
Browse our bedding selection
Select items to add to your cart
View your cart by clicking on the icon
Press ‘Buy Now!’ when you’re ready to checkout
The Product team at Mattresses and More has created a new design for the pop-ups that they believe will lead more users to complete the workflow.

They’ve set up an A/B test where:

50% of users view the original control version of the pop-ups
50% of users view the new variant version of the pop-ups
Eventually, we’ll want to answer the question:

How is the funnel different between the two groups?

We will be using a table called onboarding_modals with the following columns:

user_id - the user identifier
modal_text - the modal step
user_action - the user response (Close Modal or Continue)
ab_group - the version (control or variant)

