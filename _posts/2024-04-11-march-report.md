---
layout: post
title: "March 2024 Earnings"
categories: diary
tags: indie hacking
header-image: /images/mar-report.jpg
---

No freelancing in March. I paused all contracts and stopped looking for new clients. My goal is to build a business that can outgrow the potential income from freelancing contracts or long-term employment.

## New products

I have developed and launched one product, [X Topics][xtopics]. It's a scratch my own itch product, that I built to find the right topics to tweet about on X. It's a topic analytics tool. You upload your latest tweets, the tool extracts all tweet topics, and it ranks them according to the X score algorithm.
It took me less than 20 days to build, with the help of [SpeedPy template][speedpy]. It's pretty boilerplate, with a landing page, a login system, an upload form, and a dashboard to show the results. I had only to build a form to upload tweets and a job to analyze the tweets content. And of course, an HuggingFace endpoint to run the inference and extract the topics. I launched on PH at the end of the month, got something like 8 upvotes, and 10 or so users (mostly friends from X). No paid customer. I have given the Premium Tier to all the early subscribers. The engagement has been pretty low. Only half of the users have uploaded their tweets, there seems to be a big friction in downloading the tweets from X and uploading them on the app for analysis.

It's been less than 2 weeks since I launched. All in all, it's been a failure. Even a single paying customer would make me reconsider. There have been a few lessons learned, looking at the bright side

- Learned how to implement HuggingFace endpoints
- Created a few components for my next project
- I have a few emails I can write to for my next project
- I can keep the project running on autopilot, costs are very low

## The cashflow

Let's look at the in and out from March.

| Item              | Income/Expense |
| ----------------- | -------------- |
| Amazon book sales | + $133.23      |
| Amazon Ads        | - $8.45        |
| Appliku           | - $10.00       |
| Hetzner           | - $5.31        |
| Twitter blue      | - $10.68       |
| Domains           | - $27.30       |
| HuggingFace       | - $0.83        |
| Total             | + $70.66       |

With no project generating any revenue so far, I have only one source of income left, my books. I have invested some time in a [blog on soccer betting][soccrbets], with the main aim to attract customers. I have researched the questions with the highest traffic and I plan to publish 6 or 7 articles about various aspects of soccer betting. For now, I have published only one, but the goal is to write two articles per month. Still not sure how to get nice backlinks, but I have a few ideas.

I kept advertising on Amazon in March, but the results were underwhelming. I didn't get a single sale and my ACOS jumped to 40%. This lead me to pause the ads for now. So far, the book sales are not suffering. There is still a good amount of people that buy both of my books every month. But I would like to review a bit the ad keywords and resume the campaign as soon as I have some time.

Costs are low, with the biggest impact coming from the new domains. This will keep growing, I have already bought another one for a new project and I will have to renew the old ones for [Stoic Quotes][stoicquotes] and [Data Internships][datainternships]. I think I will let the Stoic Quotes one expire. It was a nice experiment, but I didn't find a way to make it generate any money. I want to give Data Internships another year instead. I actually enjoy going through the internship offers every week, I have built a nice mailing list of aspiring Data Scientists, which I can potentially collaborate with and who could be potential customers too. Recently I have started writing cold emails to companies that post the internship ads to ask them if they want to get a Premium spot on the website, but I have had no luck with any of those so far. I wrote to maybe 30 of them across the last 4 weeks and got only 1 negative reply. Probably need to get better at cold emails and intros. Something I am willing to do.
Another idea for monetization could be a short info product on how to get started as a Data Science freelancer, something I have experience and could help newcomers with.

[xtopics]: https://xtopics.co
[speedpy]: https://speedpy.com
[soccrbets]: https://soccrbets.com
[datainternships]: https://datainternships.co
[stoicquotes]: https://stoicquotes.co
