# Black-Scholes Model: The Greeks
## 27/08/2024

### Introduction

The Black-Scholes model is a mathematical model for pricing options. It provides a theoretical estimate of the price of European-style options. The model calculates the price by solving a partial differential equation and incorporates variables such as the current price of the underlying asset, the option's strike price, time to expiration, risk-free interest rate, and volatility of the asset.

The Greeks are a set of metrics that describe how the price of an option changes as the parameters of the Black-Scholes model change. Each Greek represents a different sensitivity and is crucial for risk management and trading strategies.

### The Greeks

#### 1. Delta ($\Delta$)

**Formula:**

$
\Delta = \frac{\partial C}{\partial S} = N(d_1)
$

**Explanation:**

Delta measures the rate of change of the option price with respect to changes in the underlying asset's price. It is the first derivative of the option price with respect to the asset price. For a call option, Delta ranges from 0 to 1, and for a put option, it ranges from -1 to 0.

**Relevance:**

Delta is crucial for hedging as it indicates the number of shares needed to hedge the option position. A Delta of 0.5 means that the option price will move by 50% of the change in the underlying asset price.

#### 2. Gamma ($\Gamma$)

**Formula:**

$
\Gamma = \frac{\partial \Delta}{\partial S} = \frac{N'(d_1)}{S \sigma \sqrt{T}}
$

**Explanation:**

Gamma measures the rate of change of Delta with respect to changes in the underlying asset's price. It is the second derivative of the option price with respect to the asset price. Gamma is highest when the option is at-the-money and decreases as the option goes deeper in-the-money or out-of-the-money.

**Relevance:**

Gamma is important for understanding how Delta changes as the underlying asset price changes. High Gamma means that Delta is very sensitive to price changes, which can lead to larger swings in the option's value.

#### 3. Theta ($\Theta$)

**Formula:**

$
\Theta = -\frac{\partial C}{\partial T} = -\frac{S N'(d_1) \sigma}{2 \sqrt{T}} - r K e^{-r T} N(d_2)
$

**Explanation:**

Theta measures the sensitivity of the option price to the passage of time, also known as time decay. It is the first derivative of the option price with respect to time. As time passes, the option's time value decreases, leading to a decline in its price.

**Relevance:**

Theta is significant for option holders because it quantifies how much the option's value decreases as the expiration date approaches. A high Theta means the option is losing value rapidly as time passes.

#### 4. Vega ($\nu$)

**Formula:**

$
\nu = \frac{\partial C}{\partial \sigma} = S N'(d_1) \sqrt{T}
$

**Explanation:**

Vega measures the sensitivity of the option price to changes in the volatility of the underlying asset. It is the first derivative of the option price with respect to volatility. Vega is higher for options that are at-the-money and decreases as the option moves in-the-money or out-of-the-money.

**Relevance:**

Vega is important for understanding how the option price will change with shifts in volatility. Traders often monitor Vega to gauge the potential impact of volatility changes on their positions.

#### 5. Rho ($\rho$)

**Formula:**

$
\rho = \frac{\partial C}{\partial r} = K T e^{-r T} N(d_2)
$

**Explanation:**

Rho measures the sensitivity of the option price to changes in the risk-free interest rate. It is the first derivative of the option price with respect to the interest rate. For call options, Rho is positive, while for put options, it is negative.

**Relevance:**

Rho is less commonly used compared to other Greeks but can be significant in environments where interest rates are volatile or for long-term options where the impact of interest rates is more pronounced.
