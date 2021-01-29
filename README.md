# Riding the Wave

### Project Proposition - Level 1

- I aim to use a classifier to predict whether an individual stock is in a ‘bubble’ state, i.e. significantly overpriced based on given information in a market. I will label previous bubbles using research that suggests a stock is a bubble if, given the CAPM/regression model stock_returns = alpha + beta * market_return, the resulting alpha is statistically significant. I do not have a backup idea, but I would choose something related.
  * Features for the classifier will include previous stock prices, moving averages, volumes, fundamental data including cash flow or net income, and possibly more.
  * Data sources: full datasets of stock prices and volumes are available on Kaggle, and I am still weighing multiple APIs that include greater detail.



### Project Proposition - Level 2

I aim to use a classifier to predict whether an individual stock is in a ‘bubble’ state, i.e. significantly overpriced based on given information in a market.

Step 1: Find target variable: 1,0 if the given stock is in a bubble.  

- Use the CAPM model, and determine if the alpha is statistically significant. 

- Model:  
  $$
  R_{it}-R_{ft} = a_i + \beta_{im}(R_{mt}-R_{ft}) + \epsilon_{it}
  $$
  where $i$ is the $i$th stock, $f$ is the risk free asset, $m$ is the relevant market, $t$ is the day.

  - An extension will be to use Fama-French model including a correlation of small cap returns minus big cap returns, and high book to market ratio minus low book to market ratio.  NOT in MVP plan.

- Method: 

  - Use stock prices month to month (or day to day, look at sources, day to day may actually be easier) to calculate $R_{it}$.  Online sources suggest a 5 year span to calculate $\beta$, but a simpler method may be useful here.
    - What time periods does the [quant paper](https://poseidon01.ssrn.com/delivery.php?ID=661105029067072102073086126120102075036068033079045035081067017018024121121124115118096007116103015125020080111083098125105109006001026038048122007124114126113120066047075020002097002118116073090116106089113124003024113102008107118124085111092017069&EXT=pdf&INDEX=TRUE) use? It may be best to replicate this. **Answer here.**
  - Take $R_{ft}$ from the treasury website for a monthly treasury bond.  The formula does generally assume a constant risk free rate across time.  This may also be simpler to look at these on a month to month basis.
  - $B_{im}$ can be calculated, and the $a_i$ will be given from this model.
    - Find the t-test using statsmodel t_test (link [here](https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.OLSResults.t_test.html))

- If $\alpha_i$ is statistically significant, add in a boolean true value for the overarching dataset of stock IDs.

- Causes for concern

  - Will this classifier only be worse than the data signifies because the method above only looks backwards.  It may actually be better to find a more accurate 'hindsight' bubble flag than this.  **Read through [this paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3460430) to determine the answer to this and look for better measures**. 

Step 2: Develop the classifier.

- Use this bubble flag to







Idea Notebook:

The goal of this project is to predict the bubble of a stock using a classification algorithm.  But why can't I just use the algorithm from the below paper?



**Riding an industry bubble**

- https://quantpedia.com/strategies/riding-industry-bubbles/
  - http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1071670
- Calculate the alpha resulting from CAPM (or FFM)
- Possible methods: determine past bubbles by stock by using the 'riding industry bubbles' method. Then use categorization to predict the same for out of sample stocks/date ranges
- But is there a better and more active way to determine a bubble than through
- The alpha method of determining a bubble might only make sense for an industry
- Maybe look at whether the stock has a significantly different price than the industry (but similar fundamentals).

**Main Sources**

- https://www.kaggle.com/borismarjanovic/price-volume-data-for-all-us-stocks-etfs/discussion/134703

- https://finnhub.io/docs/api/financials-reported
- https://www.quandl.com/databases/SF1/data

**Other possible sources**: 

- https://www.kaggle.com/boanxu/balance-sheet-cash-flow-analysis/comments
- https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2827051
- https://quantpedia.com/strategies/riding-industry-bubbles/
- https://www.federalreserve.gov/pubs/feds/2005/200504/200504pap.pdf

- http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html

- https://www.treasury.gov/resource-center/data-chart-center/interest-rates/pages/textview.aspx?data=yield

- 