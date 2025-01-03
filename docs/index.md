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
*<small>**Left panel:** Scatter plot for 3 years of LEGO sets comparing retail price (\$AUD) and number of pieces in the set. The dashed black line is the measured mean PPP for the entire sample. **Right panel:** Scatter plot for 3 years of LEGO sets comparing retail price ($AUD) and the weight of the set in grams. The dashed black line is the measured mean PPW. </small>*

The reason for both the PPP and PPW being used as a common metric for describing the pricing of LEGO sets can readily be shown by the extremely high correlation coefficients ($\rho$). The correlation coefficient describes how strongly two variables (e.g. retail price and number of pieces) are correlated, with $\rho = 1$ corresponding to perfect correlation and $\rho = 0$ means no correlation. For our two cases, we have $\rho = 0.96$ for PPP and $\rho = 0.98$ for PPW. Both demonstrating almost perfect correlations, with PPW being slightly higher.

To visualise the mean PPP and PPW, I have added the black dashed line. This is simply the measured PPP or PPW multiplied by the number of pieces or weight of the set to estimate an expected retail price.

Despite both the PPP and PPW having extremely high correlation coefficients, we can immediately see larger scatter when considering the number of pieces (larger spread of blue points) compared to the weight of the set. To better quantify the level of scatter (or accuracy) of our mean PPP and PPW we can calculate the R$^{2}$ coefficient. This determines how good a fit the black dashed line is to our data. An R$^{2}$ of 1 means a perfect fit.

For our two cases, we find R$^{2}=0.75$ for PPP and R$^{2}=0.90$ for PPW. This immediately demonstrates that using the price per weight (PPW) is the superior metric when analysing LEGO pricing as it is much more accurate at characterising the data.

Importantly, despite the clear superiority of the PPW over the PPP, throughout the remainder of this analysis I will always provide both for completeness.

### A deeper look at metrics involving pieces and weight

Although we have established that the price per piece is the superior metric, we have done this based only on a single value (the R$^{2}$ coefficient). Therefore, it is worth looking deeper into how well do these metrics actually perform, and where the differences between the two metrics occur. 

To investigate the data deeper, I will calculate the mean price of LEGO sets within fixed regions (bins) of either 1000 pieces or 1000 grams. Doing so highlights whether there is any variation (evolution) in the data for increasing the number of pieces/weight in a LEGO set. This will also highlight how good or poor a fixed PPP or PPW is. Below, I show this for the number of pieces (left) and set weight (right).

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_pieces_corr.png?raw=true" alt="Pieces vs Retail Price Corrected" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_weight_corr.png?raw=true" alt="Weight vs Retail Price Corrected" width="465"/> 
*<small> The same as above, except with the red datapoints highlighting the mean retail price being calculated in regions (bins) seperated by 1000 pieces (left panel) or 1000 grams (right panel). The error bars highlight the scatter within each bin. The red dashed line provides an alternative method to fit the data, using a linear function rather than a single value (e.g. PPP or PPW).</small>*

Here, the red datapoints highlight how the mean retail price varies as the size/weight of the LEGO set increases. On each datapoint I also show the error bar, which highlights the amount of scatter within each bin.

Beginning with the number of pieces in a set (left panel), we can clearly see that using a single metric (PPP) to represent the data is quite poor. As we consider sets with larger pieces, the red datapoints deviate further from the mean PPP. This explains why the R$^{2}$ coefficient was not particularly high (e.g. 0.75). Therefore, a simple PPP is not a very good measure.

On the right hand side, I consider the same for the weight of a LEGO set. Here, the binned data much more closely follows the mean PPW (black dashed curve). This demonstrates why the PPW was a considerably better metric. However, like for the PPP, the binned data clearly deviates by an increasing amount from the mean PPW for increasing set weights. Showing that simple metrics such as PPP or PPW are not universally capable of describing all the data.

### The problem with a single number for a metric

The benefit of a single number metric such as a PPP or PPW is the ease with which it can be interpreted. A single price per piece or gram of LEGO can be easily understood. However, as I have showed, they are not the most accurate when fitting the full range of data. This is because they fundamentally assume that the trends in the data are universal.

For our data, this is problematic owing to the distribution of LEGO sets. As can be seen from the figures above, the vast majority of sets contain less than 1500 pieces or are less than 2 kg. Therefore, when computing the PPP or PPW, we are effectively calculating a mean PPP for sets less than 1500 pieces and assuming it extends for any number of pieces (equally for the weight). 

To better handle this, we can instead fit the data with a slightly expanded linear function. Theoretically, we could also go to even more complex functions, however, that does not seem necessary given the data. Earlier, when calculating the PPP or PPW we are assuming the following functional form;
$$
y = m \times x,
$$
where $y$ is the retail price, $m$ is our PPP or PPW and $x$ is the number of pieces or the weight of the set in grams. This function is quite rigid, in only providing one free parameter to determine ($m$). 

We can simply improve on this by adding an additional variable,
$$
y = m \times x + c,
$$
where $c$ is a vertical offset. 

This functional form is shown as the red dashed lines in the figure above. We can clearly see that this functional form is a much better fit to our data, by following the red data points much more closely (the red line is not fit to the red data points).

By adopting this functional form, the R$^{2}$ for the number of pieces in a set increases from 0.75 to 0.84, demonstrating the considerable improvement achievable. For the weight of the set, R$^{2}$ improves from 0.91 to 0.93. The larger improvement for the number of pieces relative to the weight is simply due to the PPP being considerably worse than the PPW. That is, PPW was already pretty good, so we do not improve as much compared to PPP.

### The downside of increased complexity

Although increasing the complexity of the model improves the fit to the data, which is always preferable, for our study into the evolution of LEGO pricing over the years it will make things a little more difficult to interpret. Rather than following how a single value (PPP or PPW) changes as a function of time (year) we will have to track two properties (the gradient, $m$ and the offset, $c$). Secondly, the offset does not have any real meaning. Additionally, while the gradient will still be a measure of price per piece or price per weight (gram), its value will correlate with the offset, $c$, therefore it will not be as clear to interpret.

As a result, despite improving the fit to the data, for the remainder of this specific analysis I will only consider the simpler PPP or PPW. Maybe in future, I will consider revisiting this will more complexity. Although, I do not think it is really necessary.

### Why is LEGO set weight better than the number of pieces for estimating retail price?

Quite simply this is because assuming a fixed price per piece is not a fair representation of the production costs of LEGO. For example, a single 1x1 stud cannot be thought of as costing the same as a 2x4 block or 1x12 Technic beam. In fact, in recent years LEGO has introduced themes (e.g. LEGO Art or Dots), which predominately use only coloured 1x1 studs. Further, Technic sets require a large number of small pins and rods for improving structural integrity. In both cases, this can quickly inflate the piece counts of sets. If a fixed price per piece was used, these sets would be very expensive. 

However, if we use the set weight instead, this normalises for piece size. A set with a large number of small pieces will weigh a lot less than a set with larger pieces. This is why the set weight is a much better metric for estimating LEGO pricing. Heavy sets are more expensive than ligher sets. While sets with large numbers of pieces are not necessarily more expensive.

## Has LEGO gotten more expensive over time?

Time series

## Is their a noticeable premium paid on licensed sets?

Noticeable bias

## How does the cost of LEGO in Australia compare to other countries?

Location specific

## Contact Information

For any questions please contact [Brad Greig](mailto:brad.s.greig@gmail.com).