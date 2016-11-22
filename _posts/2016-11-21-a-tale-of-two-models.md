---
layout: post
title: "A Tale of Two Models"
date: 2016-11-22
---
To aid in my job hunt, I recently worked on a project where I scraped data from the [indeed.com](https://www.indeed.com) website and created a statistical model to predict whether a job would be on the higher-end or lower-end of the salary spectrum. I looked at things like a company's star rating (which surprisingly has a negative correlation with salary), the city it's in, whether or not it's in the city (as opposed to suburbs), and some text features of the job title and summary. While working on this project, I decided to take two distinct approaches to create different models:
- One is an approach I am more familiar with, which is using finding the most interpretable 

### Mystery Variable X
While I now consider myself a Data Scientist, my background is in [program evaluation](https://www.socialsolutions.com/blog/what-is-program-evaluation/), which is rooted in the social sciences. Evaluation and social science focus a lot on:
- Describing a program or phenomenon
- Determining if a program is working
- Explaining why a program is/isn't working or why the phenomenon exists
- Improving a program or taking advantage of a phenomenon

These rely on understanding and explaining things that you see, as well as ensuring that what you see is not just a fluke. Thus, things like theoretical grounding, accurate and interpretable measurements, and statistical significance are incredibly important in the social sciences. Creating a model with "Mystery Variable X" in it wouldn't make much sense because you can't describe it, you can't understand it, and you can't do anything to change it so you can improve your outcome. It also wouldn't make sense to include anything in your model that isn't statistically significant because you can't be confident

On the other hand, "Mystery Variable X" is not always a problem in Data Science and Machine Learning, because these fields are often focused on *predicting* instead of *explaining*. If "Mystery Variable X" is a good predictor of our outcome variable, and it's something we have for all our data, then there's no reason not to use it in a model! There are times where we don't care about explaining, describing, understanding, or improving - we just want to predict.

### Finding a Balance
