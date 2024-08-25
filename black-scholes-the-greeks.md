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
