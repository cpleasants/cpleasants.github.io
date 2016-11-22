---
layout: post
title: "A Tale of Two Models"
date: 2016-11-22
---
To aid in my job hunt, I recently worked on a project where I scraped data from the [indeed.com](https://www.indeed.com) website and created a statistical model to predict whether a job would be on the higher-end or lower-end of the salary spectrum. I looked at things like a company's star rating (which surprisingly has a negative correlation with salary), the city it's in, whether or not it's in the city (as opposed to suburbs), and some text features of the job title and summary. While working on this project, I decided to take two distinct approaches to create different models:
- The first was a more conservative approach where I only kept variables in my model that appeared statistically significant and variables that made logical sense to be included. In this approach, I focused on variables in my model being interpretable and understandable.
- The second was a more "black box" approach where I included as many variables as I possibly could, whether or not it made perfect logical sense to keep the variable in and whether or not each feature appeared statistically significant. Instead, I focused purely on the predictive power of my model.


The first approach is the approach I'm most used to given my background in program evaluation and the social sciences; whereas the second approach is perhaps more appropriate for the task at hand since my goal is only prediction and not explanation.

### Mystery Variable X
While I now consider myself a Data Scientist, my background is in [program evaluation](https://www.socialsolutions.com/blog/what-is-program-evaluation/), which is rooted in the social sciences. Evaluation and social science focus a lot on:
- Describing a program or phenomenon
- Determining if a program is working
- Explaining why a program is/isn't working or why the phenomenon exists
- Improving a program or taking advantage of a phenomenon

These rely on understanding and explaining things that you see, as well as ensuring that what you see is not just a fluke. Thus, things like theoretical grounding, accurate and interpretable measurements, and statistical significance are incredibly important in the social sciences. Creating a model with "Mystery Variable X" in it wouldn't make much sense because you can't describe it, you can't understand it, and you can't do anything to change it so you can improve your outcome. It also wouldn't make sense to include anything in your model that isn't statistically significant because you can't be confident that your interpretation of your model would be accurate (e.g. I wouldn't be able to confidently say that a word is predictive of high salary if the likelihood of seeing a pattern like the one I'm seeing due to random chance is not low).

On the other hand, "Mystery Variable X" is not always a problem in Data Science and Machine Learning, because these fields are often focused on *predicting* instead of *explaining*. If "Mystery Variable X" is a good predictor of our outcome variable, and it's something we have for all our data, then there's no reason not to use it in a model! There are times where we don't care about explaining, describing, understanding, or improving - we just want to predict. In addition, "statistical significance" is not the bar that we care about when predicting - the bar is "predictive power" and "generalizability". Usually, statistically significant variables have more predictive power, but we are simply shifting our focus when thinking about predicting instead of explaining.

### Model Differences
In exploring these job salary data, I took two relatively extreme approaches: an extremely conservative one and a very liberal one. In the conservative approach, I took the following approach:
- I looked at location variables and found that only certain cities appeared to have statistically significant coefficients, so I created a simpler variable with just "expensive" and "inexpensive" cities. 
- I tried other variables one-by-one in my model to see if they made a difference and were statistically significant; if they were not, I left them out of my model.
- I ended with 8 predictor variables
  - having a low star rating (over 5x the odds compared to a high star rating)
  - having no star rating (over 5x the odds compared to a high star rating)
  - being in an expensive city like New York, San Francisco, Boston, or DC (over 3.5x the odds compared to the other cities)
  - being inside the city instead of in surrounding areas like the suburbs (over 2x the odds)
  - having words in the title that suggest high-level jobs, like "senior", "manager", "director", "chief", etc. (over 3.5x the odds)
  - having the word "Data Science" or "Data Scientist" in the title (over 5x the odds compared to titles without these words)
  - having the word "engineer" in the title (over 2.5x the odds compared to titles without the word)
  - haing "machine learning" in the title (over 16x the odds compared to titles without the word).

### Striking a Balance
As I continue my journey into the world of Machine Learning, I hope to find more approaches to 
