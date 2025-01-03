# Overview

I am a huge LEGO fan and have spent a non-trivial amount of money purchasing LEGO sets that I find interesting. Being such a fan, a common thing that I hear is that people find purchasing LEGO to be expensive. Following on, people also believe that LEGO has gotten more expensive in recent times.

For quite some time I have been meaning to delve into available data on the cost of LEGO sets to explore whether it is in fact getting more expensive. Finally I have gotten around to it.

On this page, I will explore this question and a few others regarding the cost of LEGO. Namely;

- **Has LEGO gotten more expensive over time?**
- **Is their a premium paid on licensed sets (e.g. Star Wars) over unlicensed sets (e.g. Ninjago)?**
- **Is it cheap or expensive to purchase LEGO in Australia compared to elsewhere?**

For those not overly interested in the deep-dive, the **TL;DR** of these questions are;

- **Yes and No**. It depends on how you define it. Individual metrics commonly used such as cost per piece or cost per gram are fairly stable over time (decreasing when adjusted for median weekly salaries over time). However, the median size of sets has been steadily increasing (larger and more detailed) leading to, on average, higher retail prices for sets.
- **Yes!**
- Relatively speaking **yes**, although it is cheaper in US states with low sales tax.

For those interested in the details, this analysis is broken into the following:

- [Available data](#available-data)
- [Metrics for analysing the cost of LEGO sets](#metrics-for-analysing-the-cost-of-lego-sets)
- [Has LEGO gotten more expensive over time?](#has-lego-gotten-more-expensive-over-time)
- [Is their a noticeable premium paid on licensed sets?](#is-their-a-noticeable-premium-paid-on-licensed-sets)
- [How does the cost of LEGO in Australia compare to other countries?](#how-does-the-cost-of-lego-in-australia-compare-to-other-countries)

## Available data

There are multiple excellent websites hosting databases of historial information about released LEGO sets. For this exploration I have used three main sources; [Brickset](https://brickset.com/), [BrickLink](https://www.bricklink.com/v2/main.page) and [BrickEconomy](https://www.brickeconomy.com/). I have been most familiar with Brickset, which dictated that choice. I found BrickLink had a more comprehensive database when it came to information about a LEGO sets weight. Finally, BrickEconomy had easily obtainable Australian pricing information.

As this exploration is focused on pricing information, I restricted my dataset to only include sets sold at retail. That is, excluding special sets (gifts with purchase) or BrickLink sets. Further, I also restict the dataset to sets with a minimum of 100 pieces. Finally, I consider sets from 1990 until 2024. In total, this leads to a dataset of roughly 5500 unique sets.

To explore how the pricing of sets changes over time I decided to compare against the median salary in Australia (and a few other countries). One could adjust the historical pricing data for inflation using something like the consumer price index, however, I decided instead to use actual salary information. The reason for this choice is that wage growth does not necessarily follow inflation (e.g. inflation is currently outpacing wage growth in Australia). Therefore, by using actual salary information I can effectively compare the cost of LEGO as a fraction of take home salary. Importantly, although I have not checked, I am fairly confident that using inflation instead of salary information would produce fairly similar results.

Across the various LEGO data sources above I had access to Australian, US, UK and German pricing. I grabbed the median salary information for each of these countries from their respective national statistics sources; the Australian Bureau of Statistics ([ABS](https://www.abs.gov.au/)), the US Bureau of Labor Statistics ([BLS](https://www.bls.gov/)), the Office of National Statistics for the UK ([ONS](https://www.ons.gov.uk/])) and the Federal Statistics office for Germany ([Destatis](https://www.destatis.de/EN/Home/_node.html)).


## Metrics for analysing the cost of LEGO sets

When it comes to a metric to accurately quantify the perceived value of a LEGO set, the two common ones that come to mind are: (i) the price per piece (PPP) and (ii) the price per weight (PPW). These two are simply the retail price of the set divided by either the number of pieces in the set or the total weight of the set.

To investigate these metrics further I compared them for the most recent 3 years of data (2022 - 2024). By selecting 3 years of data, I can increase the sample size of the sample subset to roughly 1000 sets while limiting the chance of any variation in prices over different years. For these I consider all themes of LEGO products, not specifically selecting certain themes (I will look into that later). Below, I show scatter plots for the PPP (left) and PPW (right)

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_pieces.png?raw=true" alt="Pieces vs Retail Price" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_weight.png?raw=true" alt="Weight vs Retail Price" width="465"/> 
*<small>**Left panel:** Scatter plot for 3 years of LEGO sets comparing retail price ($AUD) and number of pieces in the set. The dashed black line is the measured mean PPP for the entire sample. **Right panel:** Scatter plot for 3 years of LEGO sets comparing retail price ($AUD) and the weight of the set in grams. The dashed black line is the measured mean PPW. </small>*

The reason for both the PPP and PPW being used as a common metric for describing the pricing of LEGO sets can readily be shown by the extremely high correlation coefficients ($\rho$). The correlation coefficient describes how strongly two variables (e.g. retail price and number of pieces) are correlated, with $\rho = 1$ corresponding to perfect correlation and $\rho = 0$ means no correlation. For our two cases, we have $\rho = 0.96$ for PPP and $\rho = 0.98$ for PPW. Both demonstrating almost perfect correlations, with PPW being slightly higher.

To visualise the mean PPP and PPW, I have added the black dashed line. This is simply the measured PPP or PPW multiplied by the number of pieces or weight of the set to estimate an expected retail price.

Despite both the PPP and PPW having extremely high correlation coefficients, we can immediately see larger scatter when considering the number of pieces (larger spread of blue points) compared to the weight of the set. To better quantify the level of scatter (or accuracy) of our mean PPP and PPW we can calculate the R$^{2}$ coefficient. This determines how good a fit the black dashed line is to our data. An R$^{2}$ of 1 means a perfect fit.

For our two cases, we find R$^{2}=0.75$ for PPP and R$^{2}=0.90$ for PPW. This immediately demonstrates that using the price per weight (PPW) is the superior metric when analysing LEGO pricing as it is much more accurate at characterising the data.

Importantly, despite the clear superiority of the PPW over the PPP, throughout the remainder of this analysis I will always provide both for completeness.

### Why is the set weight better than the number of pieces for estimating the cost of LEGO?



<figure>
  <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_pieces_corr.png?raw=true" alt="Pieces vs Retail Price Corrected" width="300"/> <figcaption>This is my caption text.</figcaption> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_weight_corr.png?raw=true" alt="Weight vs Retail Price Corrected" width="300"/> <figcaption>This is my caption text.</figcaption>
</figure>  

## Has LEGO gotten more expensive over time?

Time series

## Is their a noticeable premium paid on licensed sets?

Noticeable bias

## How does the cost of LEGO in Australia compare to other countries?

Location specific

## Contact Information

For any questions please contact [Brad Greig](mailto:brad.s.greig@gmail.com).