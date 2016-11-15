---
layout: post
title: "The Art of Keeping it Simple"
date: 2016-11-15
---

Sometimes making predictions is complicated - there can be endless numbers of factors that contribute to an outcome in sometimes counter-intuitive ways. You have to balance the need for a model complex enough to fit your data (reducing error due to "bias") and the need to ensure your model is simple enough to be generalizable to future scenarios (reducing "variance"). Other times...it's as simple as can be. 

### Iowa Liquor Sales
For a recent project, I was trying to predict 2016 total and county-by-county liquor sales for the state of Iowa based on Quarter 1 data. They have a [comprehensive dataset](https://data.iowa.gov/Economy/Iowa-Liquor-Sales/m3tr-qhgy) available on their website so I was able to use 2015 data to make a predictive model. The data are rich in detail - the state of Iowa provides:
 - A row of data for each item purchased in the state of Iowa
 - The store name, address, city, state, county, and zip code for each transaction
 - A description of each item
 - Vendor names and numbers
 - How much each bottle costs
 - The volume of each bottle
 - The number of bottles sold
 - The price the state pays and how much they sell it for
 - ...and MORE!

As any Data Nerd in their right mind would, I was thinking, "**Jackpot!**". My mind instantly starting thinking about how maybe I could use types of products a store sells, or maybe average bottle costs, to predict sales by telling me whether a store is high-end or not; or, maybe, certain stores sell primarily in large volume and that will have an impact on total sales. The possibilities were endless - this was going to be such an interesting model! I carefully cleaned the data (always an adventure), grouped by store, and started looking at which things I might add to my prediction.

Unfortunately, these things [weren't very predictive](https://public.tableau.com/views/IowaLiquorSalesPredictions/BadCorrelations?:embed=y&:display_count=yes) of total sales for the year...but I didn't want to discount them yet because there was *some* predictive value and maybe, in conjunction with total sales, these make a difference. (I don't know how to put a Tableau element into markdown, so this is it for now...)

You know what Q1 information extremely predictive of the year's sales? I'm sure you can guess it if you think about it for a second...SALES! Q1 Sales predict Yearly Sales *incredibly* well. How well? Look [here](https://public.tableau.com/views/IowaLiquorSalesPredictions/Sheet13?:embed=y&:display_count=yes)...yeah, **THAT** predictive...

### Modeling
Okay, so now that I know how well my predictive factors correlate with my outcome variable, it's time to come up with a linear model! I started by throwing in all the variables that had at least *some* correlation with my outcome, and I came up with a model score of 0.98 - that's *really* good. That means that my model accounts for 98% of the variance in the data - a perfect (and practically impossible) model would account for 100%, but this is about as close as you can get. I was good, right? With a model score that high I can just pack up and leave, right? **Wrong**. With any model you need to balance how well it fits your training data (where you can compare your predicted values to the *actual* values) to make sure it can generalize well to future data (where you don't know the *actual* values). What good is a model that fits your data perfectly if it doesn't predict anything? Typically, this means you need to make sure it's the **simplest** model that fits the data well.

A great way to see if your model generalizes well for outside data is to do what's called "cross validation", which is basically making a model on a subset of your data and seeing how well this model predicts the part of your data that is not in your subset, and then repeating this process a number of times (it's a little more complex than that, but that's the basics of it). I did a cross-validation on my model, and it performed okay: I got cross-validation scores ranging from about .8 to .99 (meaning between 80% and 99% of the variance in my test samples were accounted for by the model). In many scenarios, anything above .8 would be considered great, but the large range of scores told me that my model was probably too complex to be as generalizable as I'd like. So how can I make it simpler?

### Making it Simpler
In this project, making my model simpler was easy: I took out everything except for Q1 sales and my model score stayed about the same, but the cross-validated scores were much better and more consistent. However, if I wasn't sure what variables to kick out of my model, one way to do that would be to do a **Lasso Regularization**. Regularization basically "punishes" (adds negative points to) a model for complexity in a variety of ways (I won't bore you with the details) and picks a model that is best *after* this punishment. Lasso Regularization is good at essentially kicking out variables that punish the model without adding enough predictive power to the model to make up for the punishment. When I did this on my complex model, it kicked out everything but Q1 sales. That told me that I was probably right to make a mode on just Q1 sales. In fact, want to see how well my model was able to predict actual sales by county after adding up the stores in each county? [This well](https://public.tableau.com/views/IowaLiquorSalesPredictions/2015PredictedvsActualbyCounty?:embed=y&:display_count=yes).

So, I have a great model! I'm done, right? Not quite. It's important to take a broader look at your approach when you're done to see if you learned something along that way that can inform a better approach. In doing this, I realized that the only reason I looked at store-by-store data to predict county total sales was that I believed some store-level data would make my predictions better and I would lose this data if I looked at too high of a level. But, now that I knew all I needed is Quarter 1 sales, I realized that I could make this whole model even simpler by predicting directly on the county level instead of the store level. So, I did that. The model is slightly better - the model score went up a few points and my errors were significantly smaller. So this is the model I should use

## Conclusion? Find Ways to Keep it Simple
