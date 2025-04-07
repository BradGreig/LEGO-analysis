I am a huge LEGO fan. Being such a fan, a common thing that I hear is that people find purchasing LEGO to be expensive. Following on, people also believe that LEGO has gotten more expensive in recent times.

For quite some time I have been meaning to delve into available data on the cost of LEGO sets to explore whether it is in fact getting more expensive. Finally I have gotten around to it.

On this page, I will explore this question and a few others regarding the cost of LEGO. Namely;

- **Has LEGO gotten more expensive over time?**
- **Is their a premium paid on licensed sets (e.g. Star Wars) over unlicensed sets (e.g. Ninjago)?**
- **Is it cheap or expensive to purchase LEGO in Australia compared to elsewhere?**

For those not overly interested in the deep-dive, the **TL;DR** of these questions are;

- **Yes and No**. It depends on how you define it. Individual metrics commonly used such as cost per piece or cost per gram are fairly stable over time (decreasing when adjusted for median weekly salaries). However, the median size of sets has been steadily increasing (both in terms of weight and number of pieces) leading to, on average, higher retail prices for sets.
- **Yes!**
- Relatively speaking **yes**, although it is cheaper in US states with low sales tax.

For those interested in the details, this analysis is broken into the following:

- [Available data](#available-data)
- [Metrics for analysing the cost of LEGO sets](#metrics-for-analysing-the-cost-of-lego-sets)
- [Has LEGO gotten more expensive over time?](#has-lego-gotten-more-expensive-over-time)
- [Is their a noticeable premium paid on licensed sets?](#is-their-a-noticeable-premium-paid-on-licensed-sets)
- [How does the cost of LEGO in Australia compare to other countries?](#how-does-the-cost-of-lego-in-australia-compare-to-other-countries)

Jupyter Notebooks are provided for re-creating the plots shown within this analysis. For these, please go [here](https://github.com/BradGreig/LEGO-analysis/blob/main/data/Scripts/). 

## Available data

There are multiple excellent websites hosting databases of historical information about released LEGO sets. For this exploration I have used three main sources; [Brickset](https://brickset.com/), [BrickLink](https://www.bricklink.com/v2/main.page) and [BrickEconomy](https://www.brickeconomy.com/). I have been most familiar with Brickset, which dictated that choice. I found BrickLink had a more comprehensive database when it came to information about a LEGO sets weight. Finally, BrickEconomy had easily obtainable Australian pricing information.

As this exploration is focused on pricing information, I restricted my dataset to only include sets sold at retail. That is, excluding special sets (gifts with purchase) or BrickLink sets. Further, I also restrict the dataset to sets with a minimum of 100 pieces. Finally, I consider sets from 1990 until 2024. In total, this leads to a dataset of roughly 5500 unique sets.

To explore how the pricing of sets changes over time I decided to compare against the median salary in Australia (and a few other countries). One could adjust the historical pricing data for inflation using something like the consumer price index, however, I decided instead to use actual salary information. The reason for this choice is that wage growth does not necessarily follow inflation (e.g. inflation is currently outpacing wage growth in Australia). Therefore, by using actual salary information I can effectively compare the cost of LEGO as a fraction of take home salary. Importantly, although I have not checked, I am fairly confident that using inflation instead of salary information would produce fairly similar results.

Across the various LEGO data sources above I had access to Australian, US, UK and German pricing. I grabbed the median salary information for each of these countries from their respective national statistics sources; the Australian Bureau of Statistics ([ABS](https://www.abs.gov.au/)), the US Bureau of Labor Statistics ([BLS](https://www.bls.gov/)), the Office of National Statistics for the UK ([ONS](https://www.ons.gov.uk/])) and the Federal Statistics office for Germany ([Destatis](https://www.destatis.de/EN/Home/_node.html)).


## Metrics for analysing the cost of LEGO sets

When it comes to a metric to accurately quantify the perceived value of a LEGO set, the two common ones that come to mind are: (i) the price per piece (PPP) and (ii) the price per weight (PPW) in grams. These two are simply the retail price of the set divided by either the number of pieces in the set or the total weight of the set in grams.

To investigate these metrics further I compared them for the most recent 3 years of data (2022 - 2024). By selecting 3 years of data, I can increase the sample size of the sample subset to roughly 1000 sets while limiting the chance of any variation in prices over different years (e.g. due to inflation). For these I consider all themes of LEGO products, not specifically selecting certain themes (I will look into that later). Below, I show scatter plots for the PPP (left) and PPW (right)

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_pieces.png?raw=true" alt="Pieces vs Retail Price" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_weight.png?raw=true" alt="Weight vs Retail Price" width="465"/> 
*<small>**Left panel:** Scatter plot for 3 years of LEGO sets comparing retail price (\$AUD) and number of pieces in the set. The dashed black line is the measured mean PPP for the entire sample. **Right panel:** Scatter plot for 3 years of LEGO sets comparing retail price ($AUD) and the weight of the set in grams. The dashed black line is the measured mean PPW. </small>*

The reason for both the PPP and PPW being used as a common metric for describing the pricing of LEGO sets can readily be shown by the extremely high correlation coefficients ($\rho$). The correlation coefficient describes how strongly two variables (e.g. retail price and number of pieces) are correlated, with $\rho = 1$ corresponding to perfect correlation and $\rho = 0$ means no correlation. For our two cases, we have $\rho = 0.96$ for PPP and $\rho = 0.98$ for PPW. Both demonstrating almost perfect correlations, with PPW being slightly higher.

To visualise the mean PPP and PPW, I have added the black dashed line. This is simply the measured PPP or PPW multiplied by the number of pieces or weight of the set to estimate an expected retail price.

Despite both the PPP and PPW having extremely high correlation coefficients, we can immediately see larger scatter when considering the number of pieces (larger spread of blue points) compared to the weight of the set. To better quantify the level of scatter (or accuracy) of our mean PPP and PPW we can calculate the R$^{2}$ coefficient. This determines how good a fit the black dashed line is to our data. An R$^{2}$ of 1 means a perfect fit.

For our two cases, we find R$^{2}=0.75$ for PPP and R$^{2}=0.90$ for PPW. This immediately demonstrates that using the price per weight (PPW) is the superior metric when analysing LEGO pricing as it is much more accurate at characterising the data.

Importantly, despite the clear superiority of the PPW over the PPP, throughout the remainder of this analysis I will always provide both for completeness.

### A deeper look at metrics involving pieces and weight

Although we have established that the price per piece is the superior metric, we have done this based only on a single value (the R$^{2}$ coefficient). Therefore, it is worth looking deeper into how well these metrics actually perform, and where the differences between the two metrics occur. 

To investigate the data deeper, I will calculate the mean price of LEGO sets within fixed regions (bins) of either 1000 pieces or 1000 grams. Doing so highlights whether there is any variation (evolution) in the data for increasing the number of pieces/weight in a LEGO set. This will also highlight how good or poor a fixed PPP or PPW is. Below, I show this for the number of pieces (left) and set weight (right).

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_pieces_corr.png?raw=true" alt="Pieces vs Retail Price Corrected" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/scatter_weight_corr.png?raw=true" alt="Weight vs Retail Price Corrected" width="465"/> 
*<small> The same as above, except with the red datapoints highlighting the mean retail price being calculated in regions (bins) seperated by 1000 pieces (left panel) or 1000 grams (right panel). The error bars highlight the scatter within each bin. The red dashed line provides an alternative method to fit the data, using a linear function rather than a single value (e.g. PPP or PPW).</small>*

Here, the red datapoints highlight how the mean retail price varies as the size/weight of the LEGO set increases. On each datapoint I also show the error bar, which highlights the amount of scatter within each bin.

Beginning with the number of pieces in a set (left panel), we can clearly see that using a single metric (PPP) to represent the data is quite poor. As we consider sets with larger pieces, the red datapoints deviate further from the mean PPP. This explains why the R$^{2}$ coefficient was not particularly high (e.g. 0.75). Therefore, a simple PPP is not a very good measure.

On the right hand side, I consider the same for the weight of a LEGO set. Here, the binned data much more closely follows the mean PPW (black dashed curve). This demonstrates why the PPW was a considerably better metric. Further highlighting why the PPW is better, is the considerably smaller error bars (reduced scatter relative to PPP). However, like for the PPP, the binned data clearly deviates by an increasing amount from the mean PPW for increasing set weights. Showing that simple metrics such as PPP or PPW are not universally capable of describing all the data.

### The problem with a single number for a metric

The benefit of a single number metric such as a PPP or PPW is the ease with which it can be interpreted. A single price per piece or gram of LEGO can be easily understood. However, as I have showed, they are not the most accurate when fitting the full range of data. This is because they fundamentally assume that the trends in the data are universal.

For our data, this is problematic owing to the distribution of LEGO sets. As can be seen from the figures above, the vast majority of sets contain less than 1500 pieces or are less than 2 kg. Therefore, when computing the PPP or PPW, we are effectively calculating a mean PPP for sets less than 1500 pieces and assuming it extends for any number of pieces (equally for the weight). 

To better handle this, we can instead fit the data with a slightly expanded linear function. Theoretically, we could also go to even more complex functions, however, that does not seem necessary given the data. Earlier, when calculating the PPP or PPW we are assuming the following functional form;
$$
y = m \times x,
$$
where $y$ is the retail price, $m$ is our PPP or PPW and $x$ is the number of pieces or the weight of the set in grams. This function is quite rigid, in only providing one free parameter to determine (e.g. $m$). 

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

To investigate whether LEGO has gotten more expensive over time, we need to calculate our chosen metrics as a function of LEGO set release year. As outlined earlier, I chose the price per piece (PPP) and price per weight in grams (PPW) as the two metrics for completeness. Although, remember that the PPW is the better metric. 

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/PPP_per_year.png?raw=true" alt="PPP over time" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/PPW_per_year.png?raw=true" alt="PPW over time" width="465"/> 
*<small>Evolution in the price per piece (PPP) or the price per weight in grams (PPW) determined over 35 years of LEGO pricing information. The solid black curve is the determined PPP or PPW whereas the dashed black curve is corrected for historical inflation.</small>*

Above, the two solid black curves are the median PPP and PPW as a function of year for the 35 years of LEGO pricing information that I selected. Using the raw data, the price per piece (left panel) is fairly stable over time. For the price per weight (right panel) there is a very slight increase over 35 years, but nothing overly substantial. For example, between 2010 and 2024 the PPW has increased 10%. For a 1kg set, that would correspond to an increase of only $10 from $100 to $110. Insignificant compared to inflation which we will see next.

However, using the raw pricing data over 35 years is not a true representation of the story. We need to take into account inflation, adjusting the price of LEGO over the years to account for the increase of goods and services over time. To estimate the impact of inflation I have chosen to use historical median weekly salary data. The reason for using this is that the cost of LEGO relative to salary data to me is a better representation of how expensive something is. That is, a $100 set in 1990 is a bigger hit to the hip pocket than a $100 set in 2024 owing to the increase in weekly salaries over 35 years (which are supposed to grow in proportion to inflation).

The inflation corrected PPP and PPW are provided by the black dashed curve in the figure above. **These both conclusively show that over time both the PPP and PPW are decreasing with time. Therefore, according to PPP and PPW metrics, LEGO is cheaper than it has ever been!**

### But is that the end of the story?

Rather than looking at specific cost metrics, we can also look directly at the median cost of a LEGO set as seen below. The solid black curve is the raw data, whereas the dashed curve is the inflation adjusted median price. In terms of median set cost, we can clearly see an increase over time. In the past 5 years, the median price has gone up from $60 to $80. This corresponds to an increase by 33%.

![Median set price per year](https://github.com/BradGreig/LEGO-analysis/blob/main/data/Median_price_peryr.png?raw=true")
*<small>The median set price as a function of time.</small>*

With respect to the inflation adjusted median price (dashed curve), it has consistently been decreasing until it becomes fairly stable after 2015 albeit with some sizeable fluctuations year on year. Importantly, there does still appear to be an upswing since 2020. Implying that the increase in set prices since 2020 observed in the unadjusted data is occurring at a rate faster than inflation. **Implying the median LEGO set price is increasing**.

However, can we establish why it is increasing? We have already looked at the PPW and observed that it gradually increases in time. Now, lets look now at the median set weight as a function of time. This is shown in the left panel below. This oscillates over time, going through peaks and troughs, with two strong peaks in 1996 and 2006 (I have not investigated the sources of these, but they are likely due to smaller numbers of sets released in those years relative to later years). However, it has also steadily increased since 2015. Conveniently, the strong peak in 2006 corresponds in the dip in PPW (see the earlier figure). However, the increase since 2015 in the median set weight overlaps with the increasing PPW.

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/Median_weight_peryr.png?raw=true" alt="Median set weight over time" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/Estimated_cost_peryr.png?raw=true" alt="Estimated cost over time" width="465"/> 
*<small>Evolution in the median set weight as a function of time (left panel) and the estimated median set cost obtained by multiplying the PPW by the median set weight.</small>*

To more clearly understand what is going on, we can estimate a median cost by multiplying this median set weight (left panel above) by our PPW that we calculated earlier. This is shown in the right panel above. This overlaps strongly with our earlier estimated median set price (solid black curve).

Earlier, we estimated an increase of 33% in the median set price since 2020. Over this period the PPW only increases by just under 10%, however, the median set weight has increased by almost 20%. **Therefore the dominant contributor to the increasing median LEGO set cost is an increasing median set weight over the past 5 or so years.**

Another way to look at this is to investigate the number of sets released year on year above a certain weight. In the left panel below I have created a histogram of all sets above 3kg released since 1990. As can be seen, the number of large sets have considerably increased over the years. Last year alone, there were 23 sets above 3kg.

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/Histogram_price_peryr.png?raw=true" alt="Number of sets above 3kg" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/Percentage_peryr.png?raw=true" alt="Percentage of sets above 3kg" width="465"/> 
*<small>The number of sets released each year above 3kg (left panel) and the percentage of all LEGO sets released each year above 3kg (right panel). </small>*

Rather than the total number of large sets, we can also look at the percentage of large sets (above 3kg) released in a year relative to all sets released in that year. This is shown in the right panel above. Since 2010, the percentage of large sets have steadily increased. Earlier than 2010 the trend is less reliable owing to the considerably fewer sets released in a single year.

### Summary of findings

Inflation adjusted price metrics are decreasing with time implying the price paid per piece or weight in grams of LEGO are currently the cheapest they have ever been. However, the median size of sets is currently increasing at a faster rate than these stable or decreasing cost metrics (adjusted for inflation). This has led to an increase in the median cost of LEGO sets. In short, this leads to higher retail price of sets. Giving the appearance that LEGO has become more expensive.

However, this is purely driven by LEGO releasing more large sets (by weight and by pieces) year on year. So while the retail prices are higher, these LEGO sets also contain more pieces and/or weigh more.

## Is their a noticeable premium paid on licensed sets?

Another thing I have been curious about is whether there is a discernible price difference between licensed LEGO sets (e.g. Star Wars) and LEGO's own themes (e.g. LEGO City). That is, is there a price premium (bias) passed onto the customer to cover the additional costs of LEGO purchasing the licensing. It is well known that LEGO was in dire financial trouble in the late 1990's, rescued in no small part by purchasing and releasing licensed sets such as Star Wars and Harry Potter. 

To investigate this, I return to the same 3yr (2002 - 2024) LEGO set data that I used earlier for investigating the different LEGO price metrics (price per piece and price per weight in grams). I then split this dataset into two smaller datasets, separating licensed themes from unlicensed themes.

For the purposes of this investigation, I have considered the following two groups of licensed/unlicensed sets;

- **Licensed:** Star Wars, Disney, Marvel and DC, Harry Potter, Minecraft, Super Mario, Jurassic World, Sonic and Avatar
- **Unlicensed:** City, Creator, Friends, Classic, Dreamzzz, Ninjago, Seasonal, Monkie Kid and Dots

Importantly, I have excluded the Technic, Ideas, Icons, BrickHeadz and LEGO art themes as these ranges can contain a mix of licensed/unlicensed products. While these could be separated, it could more easily be prone to errors.

In order to establish whether there is a discernible difference between licensed and unlicensed themes I computed histograms of the PPP and PPW for all sets from the themes listed above. Below, in the left panel I have the two histograms from the unlicensed (blue) and licensed (red) sets for the PPP and in the right panel the histograms for PPW.

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/piece_licensed.png?raw=true" alt="Licensed sets by PPP" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/weight_licensed.png?raw=true" alt="Licensed sets by PPW" width="465"/> 
*<small>Distribution of Licensed and Unlicensed sets according to PPP (left) and PPW (right).</small>*

Quite clearly, for both cost metrics there is a discernible difference, with licensed sets clearly having higher PPP or PPW metrics (the distributions offset further to the right). The vertical coloured dashed lines denote the median of the two histograms to more easily visualise the difference between licensed and unlicensed sets. According to this, licensed sets have a 23% higher price per piece (3.4 cents) or 21% higher price per weight in grams (2.2 cents).

**Therefore, licensed sets are definitely more expensive**, by about 20%. However, this is not too surprising. I was just curious if it was immediately obvious from the data.

### A more detailed look

Above, we considered just a binary licensed/unlicensed classification for the LEGO sets. However, we can also go deeper and look specifically at individual themes. To do this, I have produced box and whisker plots below for each individual LEGO theme for the PPP (left panel) and the PPW (right panel). Further, I have coloured the themes that were used in the above analysis of licensed (red) and unlicensed (blue). All other themes are represented in black. I have also included the median PPP or PPW of the entire sample, denoted by the grey dashed line.

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/theme_pieces.png?raw=true" alt="Individual themes by PPP" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/theme_weight.png?raw=true" alt="Individual themes by PPW" width="465"/> 
*<small>Box and whisker plots showing the distribution of PPP (left panel) and PPW (right panel) for individual LEGO themes over a 3yr period (2022-2024). Blue corresponds to unlicensed sets, red to licensed sets and black to sets not assigned a classification.</small>*

A box and whisker plot is an easy to understand visual representation of a histogram (or probability distribution). The two whiskers (at the two extremes) correspond to the 10 and 90 percentiles of the histogram (that is, these bounds include 80% of all sets). The box highlights the central 25th and 75th percentiles (including the central 50% of all sets). The vertical line in the centre of the box is the median. Wide boxes imply broad histograms (large spread) while narrow boxes imply narrow histograms (small spread).

Representing all themes individually in this way, it is clear which sets have higher/lower cost metrics relative to the median of the entire data set. Unsurprisingly, the licensed sets are predominately above the median of the data set (owing to the premium paid that we identified above). The most expensive themes being Star Wars, Marvel and Jurassic World.

## How does the cost of LEGO in Australia compare to other countries?

Finally, I thought it would be interesting to see if I could determine whether LEGO is cheaper or more expensive here in Australia. For the data that I extracted from the data sources above, I have seemingly reliable information for the US, UK and Germany back to 2010. I have reliable data way back to 1990 for Australia which was used earlier. 

The way I decided to investigate this was to compare the cost of LEGO sets relative to the median weekly salary. A LEGO set is considered cheap if this ratio is small, as it represents a small fraction of a persons median salary. Conversely, a set is considered expensive if it is a large fraction of a take home salary.

There are two primary advantages for considering the data in this way; (i) this normalises the data across the various currencies as the cost is simply a fraction of a salary, so no longer dependent on foreign exchange rates between different countries and (ii) it essentially adjusts for inflation (taking into account that salaries were smaller in the past).

Importantly, for the figures shown below, the actual numbers on the vertical (y) axis are irrelevant as they are very small quantities (price per piece/gram divided my median salary is a small number). What is relevant, is the trend and amplitude of the line. The lower the line, the cheaper LEGO is in that country.

<img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/Country_cost_PPP.png?raw=true" alt="PPP by country" width="465"/> <img src="https://github.com/BradGreig/LEGO-analysis/blob/main/data/Country_cost_PPW.png?raw=true" alt="PPW by country" width="465"/> 
*<small>A metric to quantify how expensive LEGO is between different countries. Measured as the median PPP (left panel) or PPW (right panel) relative to the median weekly salary within each country.</small>*

Note, LEGO in Australia (10% GST), the UK (20% VAT) and Germany (19% VAT) have tax included in the retail price of LEGO sets, whereas the US does not (as the sales tax differs on a state by state basis). To account for this, for the US I provide a grey shaded box with the lower bound corresponding to a 0% sales tax and the upper bound being a 10% sales tax.

Immediately, LEGO appears to be more expensive in the UK (red line) than in all other countries I have considered. Primarily this is due to the lower salaries earnt in the UK relative to other countries. LEGO in Germany (blue) and Australia (green and gold, of course!) are fairly comparable, with Germany being very marginally lower (cheaper).

LEGO in Germany and Australia appears to be roughly comparable to US states with 5-6% sales tax. Therefore, any US state with lower sales tax will be the cheapest location to purchase LEGO. However, only 10 US states have sales taxes below 5-6%. Therefore, on average purchasing LEGO in the US is more expensive than in Australia or Germany. These conclusions appear to be broadly consistent with an analysis I just [found](https://bricknerd.com/home/which-country-has-the-cheapest-lego-9-28-23), although using a completely different methodology.

In summary, the cost of LEGO in Australia and Germany is fairly comparable, which is cheaper on average than the US and much cheaper than the UK.

## Contact Information

For any questions please contact [Brad Greig](mailto:brad.s.greig@gmail.com).