# Dividend Risk

Dividend risk arises from dividend uncertainty, mostly coming from company idiosyncrasy. Like other type of market risk, the dividend risk is primarily due to market perception rather than actual performance of the underlying company. 
Dividend risk arises from dividend uncertainty, mostly coming from company idiosyncrasy. Like other type of market risk, the dividend risk is primarily due to market perception rather than actual performance of the underlying company. The equity derivatives that take expected dividend amount or yield as a pricing input are exposed to dividend risk.
 
The proposal is to capture the dividend risk under normal market conditions. Stress test is considered a more appropriate approach to capture the risk of severe cutting or eliminating dividend of large blue chip stocks during financial crisis.
 
We model dividend risk by introducing a new risk factor – the innovation in dividend expectation. It is to describe the day-to-day relative changes to the expected dividend amount of the underlying stock, basket of stocks, or equity index. The new risk factor facilitates the calculation of the market expected dividend when pricing an equity derivative at future time. See https://finpricing.com/lib/EqBarrier.html

We model one-day innovation in dividend expectation of a stock as a mixed distribution with two components: jumps and no jump. Jumps refer to non-zero innovation, modeled using double exponential distribution to account for fat tails. No-jump corresponds to the scenario that the dividend projection stays unchanged, typical for large utilities. 

For equity index, due to diversification we assume that the innovation is always non-zero. Thus, the one-day innovation in dividend expectation of an equity index is modeled using double exponential distribution. Baskets of stocks are mapped to equity index. Correlation among dividend of equity indices, as well as correlation between dividend risk factors and other risk factors, is also captured. We assume no correlation among the dividend of single stocks.

To calibrate the dividend risk factor, implied dividend yield from equity index futures market is investigated. However, we observe that the implied dividend yield is contract specific and predominantly driven by index price, which is already a risk factor. The innovation in expected dividend cannot be accurately estimated from implied dividend yield due to the large noise from market technicalities. This is evidenced by the extraordinarily high volatility (over 40%) of the daily innovation in dividend expectation.
 
As an alternative, Bloomberg projected dividend amount is a forward-looking estimate based on multiple factors including market price of traded options. It is widely used by traders in pricing equity derivatives. We consider it appropriate to calibrate dividend risk model using Bloomberg projected dividend.
 
The emphasis is on model implementation. Specifically, the document covers dividend data collection, sensitivity calculation, risk factor mapping and simulation. This involves stakeholders across Market Risk, Technology, and Trading System. The breakdown of tasks is summarized as follows.

-          Market Risk: investigate data availability for risk factors calibration and sensitivity calculation, develop and automate calibration engine, provide functional specifications for implementing the model, design UAT plan and perform UAT, perform regular calibration update.
 
-          Technology: implement risk factor mapping and simulation, and sensitivity calculation based on functional specifications; perform UAT test; perform maintenance and implement enhancement as per Market Risk specifications.
 
-          Trading System: provide the risk system with end of the day annualized dividend yield (may be converted from amount) used in pricing; provide description and pricing model for new equity derivative products to be traded and booked in trading book.

We introduce a simple approach to account for dividend risk. The dividend risk arises from the uncertainty of the future dividend cash flow of a dividend-paying stock. Historically, dividends are an important part of the total return of an equity investment, contributing approximately one third of long term total return of S&P 500 index [1]. Equity derivatives and equity hybrid instruments have meaningful exposure to dividend risk.

Similar to bond investment, where the future cash flow has two components: periodical interest/coupon payment and principal repayment if held to maturity or the market price of the bond if sold before maturity, the cash flow from an equity investment also has two components: periodical dividend payment, if any, and the market value of equity at the time of liquidations. 

However, unlike bond where there is no separate coupon risk because coupon payment is legally promised in bond covenant and hence is incorporated into credit risk of the issuer, common share may have dividend risk since dividend is not legally guaranteed – cutting or eliminating dividend is completely at the corporate board’s discretion and as such, dividend risk is a separate risk from the equity price risk.
 
Note that holder of equity is exposed to the combined risk of equity price risk and dividend risk. In this case, there is no need to separate the two and model them separately. A rate of total return is a more practical and convenient way to model this combined risk. We all know that under the risk-neutral measure, the rate of total return of a stock is the risk-free interest rate for the holding period.
