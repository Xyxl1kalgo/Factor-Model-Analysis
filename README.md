# Hello everyone, I am a beginner quantitative researcher and I am engaged in the planned study and application of my knowledge in higher mathematics and in the market analysis that I have already done

# Financial Asset Analysis: CAPM vs. Fama-French 3-Factor Model

This project explores the daily excess returns of six prominent technology stocks – Apple (AAPL), Amazon (AMZN), Google (GOOG), Microsoft (MSFT), NVIDIA (NVDA), and Tesla (TSLA) – using two fundamental asset pricing models: the Capital Asset Pricing Model (CAPM) and the Fama-French 3-Factor Model. Our goal is to understand the drivers of these stocks' returns and assess which model provides a more comprehensive explanation of their historical performance.

## Theoretical Framework

Capital Asset Pricing Model (CAPM)

The Capital Asset Pricing Model (CAPM) is a widely used financial model that describes the relationship between systematic risk and expected return for assets, particularly stocks. It posits that the expected return on a security is equal to the risk-free rate plus a risk premium that is proportional to the amount of systematic risk undertaken.

The CAPM model is:

$$E(R_i) - R_f = \alpha_i + \beta_i (E(R_m) - R_f) + \epsilon_i$$

Where:

* $E(R_i)$ - is the expected return of the investment.

* $R_f$ - is the risk-free rate.

* $E(R_m)$ - is the expected return of the market portfolio.

* $\beta_i$ (Beta) - is the sensitivity of the asset's excess return to the market's excess return.

* $\alpha_i$ (Alpha) - represents the asset's excess return over what the CAPM predicts, often interpreted as a measure of a manager's skill or a security's mispricing.

* $\epsilon_i$ - is the residual (unexplained) return.

Fama-French 3-Factor Model

The Fama-French 3-Factor Model expands on the CAPM by adding two additional factors to better explain asset returns: the size risk and value risk. This model suggests that, in addition to market risk, the size of a company and its book-to-market ratio (value) can also explain differences in stock returns.

The Fama-French 3-Factor Model formula is:

$$E(R_i) - R_f = \alpha_i + \beta_{Mkt-RF} (E(R_m) - R_f) + \beta_{SMB} SMB + \beta_{HML} HML + \epsilon_i$$
Where:
* $E(R_i) - R_f$ is the excess return of the asset.

* $E(R_m)−R_f (Mkt-RF)$ is the excess return of the market, representing market risk.

* $SMB$ (Small Minus Big) is the size factor, representing the historical excess returns of small-cap stocks over large-cap stocks. A positive $\beta_{SMB}$ indicates a tendency to perform better with smaller companies.

* $HML$ (High Minus Low) is the value factor, representing the historical excess returns of high book-to-market (value) stocks over low book-to-market (growth) stocks. A positive 
$\beta_{HML}$ indicates a tendency to perform better with value companies.

* $\beta_{Mkt−RF}, \beta_{SMB}, and  \beta_{HML}$ are the sensitivities of the asset's excess return to each respective factor.

* $\alpha_i$ (Alpha) is the asset's excess return unexplained by these three factors.

## Methodology

### Data Sources

* **Stock Prices**: Daily historical stock prices for AAPL, AMZN, GOOG, MSFT, NVDA, and TSLA were obtained from ```yfinance```.

* **Fama-French Factors**: Daily Fama-French 3-factor data (Mkt-RF, SMB, HML, and RF) was sourced from Kenneth French's data library.

### Data Processing

* **Daily Returns**: Daily returns for each stock were calculated from adjusted closing prices.

* **Risk-Free Rate**: The daily risk-free rate (RF) was directly taken from the Fama-French dataset.

* **Excess Returns**: Excess returns for each stock and the market were calculated by subtracting the daily risk-free rate from their respective total returns.

* **Data Synchronization**: All time series were carefully synchronized to ensure that regressions were performed on common dates, handling any missing values (NaN).

### Regression Analysis

* **Ordinary Least Squares (OLS)** regression models were built using ```statsmodels.api``` in Python for each stock.

* **CAPM**: Each stock's excess return was regressed against the market excess return.

* **Fama-French 3-Factor Model**: Each stock's excess return was regressed against the market excess return (Mkt-RF), the size factor (SMB), and the value factor (HML).

## Results and Analysis

### Model Comparison: Explanatory Power (R-squared)

A crucial metric for comparing the models is the **R-squared (R²)**, which indicates the proportion of variance in the dependent variable (stock's excess return) that can be predicted from the independent variables (factors).

| Ticker 	| R-squared 	| R-squared (CAPM) 	|
|--------	|-----------	|------------------	|
| AAPL   	| 0.6037    	| 0.5597           	|
| AMZN   	| 0.516     	| 0.3953           	|
| GOOG   	| 0.5634    	| 0.5178           	|
| MSFT   	| 0.7139    	| 0.6394           	|
| NVDA   	| 0.5049    	| 0.4142           	|
| TSLA   	| 0.2871    	| 0.2226           	|


### Observation:
As observed in the table above, the Fama-French 3-Factor Model consistently demonstrates a significantly higher R-squared compared to the CAPM for all analyzed stocks. This indicates that incorporating the size (SMB) and value (HML) factors substantially improves the model's ability to explain the variability in these stocks' returns. For instance, for MSFT, the R-squared improved from 0.6394 to 0.7139, showcasing a much more comprehensive explanation of its return dynamics. This finding validates the inclusion of additional systematic risk factors beyond just market exposure.

### Fama-French 3-Factor Model: Detailed Analysis

Let's delve deeper into the specific factor sensitivities (beta coefficients) and Alpha (alpha) for each stock under the Fama-French model.

| Ticker 	| R-squared 	| Alpha (const) 	| Alpha p-value 	| Mkt-RF Beta 	| Mkt-RF p-value 	| SMB Beta 	| SMB p-value 	| HML Beta 	| HML p-value 	|
|--------	|-----------	|---------------	|---------------	|-------------	|----------------	|----------	|-------------	|----------	|-------------	|
| AAPL   	| 0.6037    	| 0.0003        	| 0.1787        	| 1.1734      	| 0.0            	| -0.2974  	| 0.0         	| -0.3997  	| 0.0         	|
| AMZN   	| 0.516     	| 0.0004        	| 0.1357        	| 1.1274      	| 0.0            	| -0.2019  	| 0.0         	| -0.7406  	| 0.0         	|
| GOOG   	| 0.5634    	| 0.0002        	| 0.4179        	| 1.1264      	| 0.0            	| -0.2585  	| 0.0         	| -0.4051  	| 0.0         	|
| MSFT   	| 0.7139    	| 0.0003        	| 0.1228        	| 1.2052      	| 0.0            	| -0.437   	| 0.0         	| -0.463   	| 0.0         	|
| NVDA   	| 0.5049    	| 0.0013        	| 0.0018        	| 1.6787      	| 0.0            	| 0.0149   	| 0.8227      	| -0.9364  	| 0.0         	|
| TSLA   	| 0.2871    	| 0.0006        	| 0.3324        	| 1.4364      	| 0.0            	| 0.5726   	| 0.0         	| -0.7276  	| 0.0         	|

### Key Observations per Stock:

* **Apple (AAPL), Amazon (AMZN), Google (GOOG), Microsoft (MSFT)**:

* * **Market Beta (Mkt-RF)**: All show betas significantly greater than 1 (e.g., AAPL: 1.1734, MSFT: 1.2052), indicating they are generally more volatile than the overall market. This is typical for large-cap tech companies with high growth potential and sensitivity to economic cycles.

* * **Size Factor (SMB)**: Their negative and highly significant SMB betas (e.g., MSFT: -0.4370) confirm they behave as "big companies." Their returns tend to move inversely with the performance of small-cap stocks, meaning they perform well when large companies outperform small ones.

* * **Value Factor (HML)**: All exhibit negative and highly significant HML betas (e.g., AMZN: -0.7406, NVDA: -0.9364). This firmly categorizes them as "growth stocks." Their returns are positively correlated with the performance of other growth stocks, reflecting their focus on future earnings rather than current book value.

* * **Alpha (const)**: For AAPL, AMZN, GOOG, and MSFT, the alpha coefficients are small and statistically insignificant (p-values > 0.05). This suggests that after accounting for market risk, size, and value factors, these stocks do not consistently generate abnormal returns. Their performance is largely explained by their exposure to these systematic factors.

* **NVIDIA (NVDA):**

* * **Market Beta (Mkt-RF):** At 1.6787, NVDA shows the highest market beta among the group, indicating its extreme sensitivity to market movements, characteristic of a high-growth, high-volatility semiconductor company.

* * **Size Factor (SMB)**: The SMB beta is 0.0149 with a p-value of 0.8227, making it statistically insignificant. This implies that NVIDIA's returns are not significantly influenced by the size premium factor within this model.

* * **Value Factor (HML):** With an HML beta of -0.9364, NVDA exhibits the strongest "growth" characteristic, indicating its returns are highly aligned with the performance of other growth-oriented companies.

* * **Alpha (const):** Interestingly, NVDA shows a positive and statistically significant alpha of 0.0013 (p-value 0.0018). This potentially indicates that NVIDIA generated abnormal returns beyond what is explained by its exposure to the market, size, and value factors during the analyzed period. This could be due to unique competitive advantages or market inefficiencies.

*  **Tesla (TSLA):**

* * **R-squared:** TSLA has the lowest R-squared (0.2871), suggesting that the 3-factor model explains a significantly smaller portion of its return variability compared to the other stocks. This implies that other, possibly idiosyncratic, factors or uncaptured systematic risks play a larger role in TSLA's performance.

* * **Market Beta (Mkt-RF):** With a beta of 1.4364, TSLA is highly volatile relative to the market, consistent with its disruptive and often speculative nature.

* * **Size Factor (SMB):** Uniquely, TSLA exhibits a positive and highly significant SMB beta of 0.5726. This is counter-intuitive for a large-cap company and suggests that, despite its considerable market capitalization, TSLA's returns are sensitive to factors usually associated with small-cap, high-growth, or potentially more speculative companies. This could reflect its rapid growth trajectory and high investor expectations.

* * **Value Factor (HML):** TSLA's HML beta is -0.7276, confirming it is a strong "growth stock," similar to its tech peers.

* * **Alpha (const):** The alpha for TSLA is insignificant (p-value 0.3324), meaning the returns are explained by the existing factors, despite the model's lower overall explanatory power.

## Conclusion
This analysis confirms that the Fama-French 3-Factor Model offers a superior framework for understanding the risk and return dynamics of large technology stocks compared to the simpler CAPM. The inclusion of size (SMB) and value (HML) factors significantly enhances the explanatory power of the model across the board.

Our findings highlight that most of these tech giants generally behave as **highly volatile, large-cap growth stocks**. However, distinct nuances emerge, such as NVIDIA's potential for **statistically significant alpha** and Tesla's intriguing **positive sensitivity to the small-cap factor (SMB)**, which deviates from typical large-company behavior.

**Practical Implications:**

Understanding these factor exposures is invaluable for investors. It enables more informed decision-making by:

* **Decomposing returns**: Identifying whether returns are driven by broad market movements, company size, value characteristics, or truly idiosyncratic factors (alpha).

* **Portfolio construction**: Designing more diversified portfolios that strategically manage exposure to these systematic risk factors.

* **Performance attribution**: Evaluating the true skill of fund managers by isolating pure alpha from factor-driven returns.

This project underscores the importance of multi-factor models in capturing the complexities of asset returns in modern financial markets.


# Thank you very much for reaching the end and I hope you read everything)

# If you disagree with something or want to discuss this topic, then my links are in my profile