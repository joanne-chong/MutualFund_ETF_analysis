# Mutual Fund & ETFs Analysis
---

## Executive Summary
In 2022, mutual funds in the US suffered a loss of USD 879 billion from investors pulling out in the first 11 months of the year. During the same time frame, passive funds recorded USD 51.6 billion net inflows (positive difference between cash inflow and outflow). In fact, active mutual funds reported consecutive monthly net outflows since October 2021 while passive mutual funds have collected net inflows. These are the result of a volatile market and ongoing economic uncertainties - which saw investors becoming conservative and turning to alternative investment strategies. ETF.com reported that firms are focusing on building out their exchange-traded fund (ETFs) and more than 400 of them were launched in 2022. ([Financial Times](https://www.ft.com/content/e52a9fa6-bc94-4284-81e9-4bb01da2eb9d), Jan 2023)

Both mutual funds and ETFs are two different type of pooled investment funds that sell shares to investors. These type of funds are a great way to diversify investments from international stocks, government bonds, industry-focused stocks to specialized growth or value investing. These are usually a great choice for long-term investors. However, both types of funds do vary - mutual funds usually includes maintenance fees, sales loads and expenses as they are actively managed while ETFs have lower fees (though there is still commissions and transaction costs). 

Over the years, ETFs have been gaining traction across experienced investors and those new to investments - leading to ongoing discussion on the performance and benefits to the investors. Meanwhile fund managers are shifting gears to expand their offerings and cater to the increasingly savvy investors. 

Using historical data, we've used machine learning models to identify whether mutual fund or ETFs would make a better investment option. These are based on the accuracy of performance prediction and the top features that influence each of the investment funds.

These models are aimed at helping fund managers and potential investors evaluate their portfolio and maximize their investment efforts.

## Content
- [Part 1: Data Cleaning](Part_1_Cleaning.ipynb)
- [Part 2: Exploratory Data Analysis](Part_2_EDA.ipynb)
- [Part 3: Modeling: Mutual Fund v1](Part_3_Modeling_MF_v1.ipynb) - Mutual Fund Prediction of fund returns
- [Part 4: Modeling: Mutual Fund v2](Part_4_Modeling_MF_v2.ipynb) - Mutual Fund Prediction of alpha
- [Part 5: Modeling: ETFs v1](Part_5_Modeling_ETF_v1.ipynb) - ETF Prediction of fund returns
- [Part 6: Modeling: ETFs v2](Part_6_Modeling_ETF_v2.ipynb) - ETF Prediction of fund alpha
- [Part 7: Evaluation & Conclusion](Part_7_Conclusion.ipynb)

## About the datasets
The datasets were taken from [Kaggle](https://www.kaggle.com/datasets/stefanoleone992/mutual-funds-and-etfs), covering US-based mutual fund and ETF information scraped from Yahoo Finance. The dataset was last updated in November 2021. The files we'll be using for this project:
- `MutualFunds.csv`: This dataset contains 23,782 mutual funds, including yearly and quarterly fund returns from 2000 to the first three quarters of 2021. The dataset and the processed datasets can be found [here](https://drive.google.com/drive/folders/16XIzuLcKMnxGcqjRc5XfT_gDTKouQch2?usp=share_link)
- `ETFs.csv`: This dataset contains 2,309 ETFs, including yearly fund returns from 2000 to 2020

NOTE: Full data dictionary can be found [here](Part_1_Cleaning.ipynb)

## Methodology 
We've conducted a thorough analysis and modeling through thse steps:
1. **Data Cleaning**: We assessed both the mutual fund and ETF datasets for missing values where we've filled them or removed them if irrelevant.
2. **Exploratory Data Analysis**: We visualized the dataset through a series of graphs and plots to better understand the relationships between variables as well as its individual impact on the mutual fund performance.
3. **Feature Engineering & Data Preprocessing**: After evaluating specific variables, we removed variables that didn't have much impact and combined variables that were relevant to each other.
4. **Data Modeling & Prediction**: Based on the selected features, we used several regressor models in these approaches:
    - Approach 1: Mutual fund prediction of the year-to-date return 
    - Approach 2: Mutual fund prediction of alpha value
    - Approach 3: ETF prediction of year-to-date return 
    - Approach 4: ETF prediction of alpha value
5. **Evaluation & Conclusion**: Following the results, we were able to identify the models that generated the best prediction accuracy and identify the features that influenced a fund's performance.

## Initial Findings
1. Blend portfolio is the most popular investment strategy - Mutual fund Blend (46%), ETF Blend (43%)
2. Large portfolio makes up the most mutual funds with an average of USD6.2mil total net assets, where the portfolio is spread is 56% Blend, 22% Growth and 22% Value
3. Large portfolio makes up the most ETFs with an average of USD3.5mil total net assets, where the portfolio is spread is 55% Blend, 23% Growth and 22% Value
4. The top sector portfolio in mutual funds are: Technology, financials, healthcare
5. The top sector portfolio in ETF are: Technology, financials, consumer cyclical
6. Mutual fund has higher annual holdings turnover of 92.9%, compared to ETF's 83.1%
7. The average annual net expense ratio of mutual funds is 1.04% while for ETF is it close to half of the value - 0.54%
8. Overall, mutual funds reported higher fund returns compared to ETF. The average year-to-date return for mutual fund is 9.2% while ETF is 7.3%.
9. The average fund yield for mutual fund is 1.7% while ETF is 1.9%.
10. The average price-to-earnings (P/E) ratio for mutual fund is 24.7 while for ETF it is 23.5
11. When it comes to alpha scores, it's difficult to generate a positive alpha. Large funds were able to generate alphas closer to 0, indicating that they are tracking well against the benchmark. Growth portfolio usually has positive alpha as they are focused on companies with high growth rates.
12. Overall, while mutual funds have better performance, the data shows ETF isn't far behind and is able to keep up with the market performance.

## Modeling Results
We generateD predictions using:
- **Supervised learning**: Linear regression, Lasso regression, Ridge regression
- **Clustering**: KNeighbors regressor
- **Ensemble learning**: Decision tree, Bagged tree, Random Forest, Adaptive Boosting, Support Vector, Gradient Boosting

Overall, Random Forest showed the best initial performance so GridSearch was used to tune the parameters. Summary of the tuned results:
|                                           	| **Best score** 	| **R2  Train** 	| **R2 Test** 	| **RMSE Train** 	| **RMSE Test** 	|
|-------------------------------------------	|:--------------:	|:-------------:	|:-----------:	|:--------------:	|:-------------:	|
| **Mutual fund prediction of YTD returns** 	|     0.9246     	|     0.9919    	|    0.9410   	|     0.0072     	|     0.0193    	|
| **Mutual fund prediction of alpha**       	|     0.9290     	|     0.9921    	|    0.9294   	|     0.4438     	|     1.3637    	|
| **ETF prediction of YTD returns**         	|     0.2315     	|     0.5287    	|    0.1998   	|     0.0814     	|     0.1341    	|
| **ETF prediction of alpha**               	|     0.2685     	|     0.5661    	|    0.1871   	|     3.6966     	|     6.029     	|

Overall, alpha predictions achieved the best scores and improved results. We would recommend using it as a target variable to predict. 

However, we do note that the ETF predictions fall significantly short compared to mutual funds due to the lack of quality dataset.

The best parameters for:
- Mutual fund prediction of alpha:-
    - `n_estimators`: 200
    - `max_depth`: None
- ETF prediction of alpha:-
    - `n_estimators`: 150
    - `max_depth`: 4   
    
`n_estimators` represent the number of trees in the Random Forest model. As we can see that the mutual fund prediction has a higher value because of the volume of data.

`max_depth` represents the depth of each tree in the forest, to capture information about the data. The mutual fund prediction didn't require any parameters for this as the volume of data was sufficient to learn from, meanwhile the ETF prediction needed more depth to be able to learn from the dataset.

## Conclusion
Overall, we were able to create a model to generate near-accurate prediction for mutual funds - making it the better investment option solely based on prediction accuracy. 

The 10 most important features that would impact the accuracy of the model: 
1. Investment type (Growth)
2. Morningstar overall rating
3. Stocks asset breakdown
4. ESG score
5. Fund sector (Energy)
6. Fund sector (Industrials)
7. Size fund (Large)
8. Size fund (Small)
9. Morningstar risk rating
10. Fund sector (Technology)

However, this does not mean that ETF is not a worthy investment alternative. As we saw from the EDA section that ETFs have been able to keep up with market and cost investors a lot less, enabling them to earn more for less. Furthermore, ETFs have been gaining traction over the years and will continue to stay. 

## Limitations
1. The lack of quality ETF dataset has certainly impacted our EDA and modeling section. Fortunately, as ETF gains more traction, there will be more effort to keep record of the data and eventually create a better prediction model. 
2. Prediction model in practice - unfortunately the market changes too fast for prediction models to be put to work effectively. Many studies and fund managers have attempted to predict performance, but the actual market performance often vary greatly and this remains an ongoing quest.
3. Since the key to the success of mutual funds and ETFs is based on how the portfolio changes, we should ideally look at the performance before and after that change within the same fund. This way we'll be able to tell which of the changes had a bigger impact on performance. 

## Recommendations
Through our findings and model, fund managers and investors will be able to look for ways to maximize their returns.
- For fund managers:
    - Re-look at both current active and passive funds and ensure that the shortlisted features are optimized
    - For active mutual funds that have been doing well consistently with minimal effort, consider converting them to index funds
    - Create new active mutual funds using this model and also focus on bringing the added-value to investors, for example, share information on coveted stocks that are not widely available to the public
    - Collect more data on mutual funds and ETF to improve prediction accuracy
    - Put on different hats from a market expert to financial advisor, while keeping the investor's priority in mind, by adapting the counsel to client on the best investment option for their needs
- For investors:
    - Using the shortlisted features, re-look at current portfolio to ensure that these features are optimized to meet investment objectives
    - Prioritize investment goals and diversify accordingly, e.g. engage a fund manager if the goal is to outperform market and willingly take risks
    - Keep up with new products and regulatory changes in this space as well, to make informed decisions about investment
    
