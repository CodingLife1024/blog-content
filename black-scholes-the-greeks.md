# Black-Scholes Model: The Greeks
## 27/08/2024

### Introduction

The Black-Scholes model is a mathematical model for pricing options. It provides a theoretical estimate of the price of European-style options. The model calculates the price by solving a partial differential equation and incorporates variables such as the current price of the underlying asset, the option's strike price, time to expiration, risk-free interest rate, and volatility of the asset.

The Greeks are a set of metrics that describe how the price of an option changes as the parameters of the Black-Scholes model change. Each Greek represents a different sensitivity and is crucial for risk management and trading strategies.

### The Greeks

#### 1. Delta ($\Delta$)

**Formula:**

$$
\Delta = \frac{\partial C}{\partial S} = N(d_1)
$$

**Derivation:**

Delta measures the rate of change of the option price with respect to changes in the underlying asset's price.

- **Black-Scholes Formula for Call Option:**
  $$
  C = S N(d_1) - K e^{-rT} N(d_2)
  $$
  where:
  - $N()$ is the cumulative distribution function of the standard normal distribution.
  - $d_1 = \frac{\ln(S/K) + (r + \frac{\sigma^2}{2})T}{\sigma \sqrt{T}}$
  - $d_2 = d_1 - \sigma \sqrt{T}$

- **Delta Calculation:**
  $$
  \Delta = \frac{\partial C}{\partial S} = N(d_1)
  $$

##### Additional Information:

- **Range**: For a call option, Delta ranges from 0 to 1, meaning as the underlying asset's price increases, the option's price also increases. For a put option, Delta ranges from -1 to 0, indicating that as the underlying asset's price increases, the option's price decreases.

- **Delta Neutral**: Traders often use Delta-neutral strategies to hedge their portfolios. This involves adjusting the portfolio to have a net Delta of 0, thereby reducing the risk of price movements in the underlying asset.

#### 2. Gamma ($\Gamma$)

**Formula:**

$$
\Gamma = \frac{\partial \Delta}{\partial S} = \frac{N'(d_1)}{S \sigma \sqrt{T}}
$$

**Derivation:**

Gamma measures the rate of change of Delta with respect to changes in the underlying asset's price.

- **Derivative of Delta:**
  $$
  \Delta = N(d_1)
  $$
  where $N'(d_1)$ is the probability density function of the standard normal distribution.

- **Gamma Calculation:**
  $$
  \Gamma = \frac{\partial \Delta}{\partial S} = \frac{N'(d_1)}{S \sigma \sqrt{T}}
  $$

##### Additional Information:

- **Range**: Gamma is positive for both call and put options. It is highest when the option is at-the-money (the strike price is close to the underlying asset price) and decreases as the option moves in-the-money or out-of-the-money.

- **Gamma Scalping**: Traders use Gamma scalping to profit from the fluctuations in the underlying asset's price. This involves continually adjusting the Delta hedge as the underlying asset's price changes.

#### 3. Theta ($\Theta$)

**Formula:**

$$
\Theta = -\frac{\partial C}{\partial T} = -\frac{S N'(d_1) \sigma}{2 \sqrt{T}} - r K e^{-r T} N(d_2)
$$

**Derivation:**

Theta measures the sensitivity of the option price to the passage of time.

- **Black-Scholes Formula for Call Option (Recall):**
  $$
  C = S N(d_1) - K e^{-rT} N(d_2)
  $$

- **Derivative with respect to Time:**
  $$
  \Theta = -\frac{\partial C}{\partial T}
  $$
  - Derive $d_1$ and $d_2$ as previously mentioned.

##### Additional Information:

- **Time Decay**: Theta is often referred to as the "time decay" of an option. It quantifies the rate at which the option's value decreases as time passes, holding all other factors constant. As expiration approaches, Theta increases in magnitude, meaning the option loses value more rapidly.

- **Effect on Option Pricing**: Short-dated options have higher Theta compared to long-dated options, as the time decay accelerates as the expiration date nears.

#### 4. Vega ($\nu$)

**Formula:**

$$
\nu = \frac{\partial C}{\partial \sigma} = S N'(d_1) \sqrt{T}
$$

**Derivation:**

Vega measures the sensitivity of the option price to changes in the volatility of the underlying asset.

- **Derivative with respect to Volatility:**
  $$
  \nu = \frac{\partial C}{\partial \sigma} = S N'(d_1) \sqrt{T}
  $$

  - Derive $d_1$ as previously mentioned.

##### Additional Information:

- **Volatility Sensitivity**: Vega measures the sensitivity of an option's price to changes in the volatility of the underlying asset. It is highest for at-the-money options and decreases as the option moves in- or out-of-the-money.

- **Impact of Volatility**: High Vega indicates that the option's price is highly sensitive to changes in volatility. In markets with high volatility, options with high Vega can experience significant price changes even if the underlying asset's price remains stable.

#### 5. Rho ($\rho$)

**Formula:**

$$
\rho = \frac{\partial C}{\partial r} = K T e^{-r T} N(d_2)
$$

**Derivation:**

Rho measures the sensitivity of the option price to changes in the risk-free interest rate.

- **Derivative with respect to Interest Rate:**
  $$
  \rho = \frac{\partial C}{\partial r} = K T e^{-r T} N(d_2)
  $$
  - Derive $d_2$ as previously mentioned.

##### Additional Information:

- **Interest Rate Sensitivity**: Rho measures the sensitivity of an option's price to changes in the risk-free interest rate. It is generally more significant for long-term options, where the impact of interest rate changes on the present value of the strike price is more pronounced.

- **Call vs. Put Rho**: For call options, Rho is positive, indicating that an increase in interest rates will increase the option's price. For put options, Rho is negative, meaning an increase in interest rates will decrease the option's price.
