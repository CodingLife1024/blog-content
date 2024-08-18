# Black-Scholes Model: Introduction
## 20/08/2024 

The Black-Scholes model is a mathematical framework and algorithm for pricing European-style options, which are financial derivatives that give the holder the right, but not the obligation, to buy or sell an underlying asset at a specified price on a specified date.

### Introduction

Here are some basic definitions of some of the terms used in this model - 

__Strike Price (K)__: The strike price, also known as the exercise price, is the price at which the option holder can buy or sell the underlying asset. In the context of a call option, the strike price is the price at which the holder can purchase the asset. For a put option, it is the price at which the holder can sell the asset.

__Underlying Asset Price/Stock Price (S)__: The current price of the asset on which the option is written. This is the price that will be compared to the strike price to determine the payoff of the option at expiration.

__Volatility ($\sigma$)__: Volatility refers to the degree of variation in the price of the underlying asset over time. In the Black-Scholes model, volatility is a key input and is usually expressed as the standard deviation of the asset's returns. It reflects the market's expectation of the asset's future price fluctuations.

Mathematical Expression:

$
\sigma = \sqrt{\frac{1}{T} \sum_{t=1}^{T} (r_t - \bar{r})^2}
$

__Time to Maturity (in years) (T)__: This represents the remaining time until the option's expiration date.

__Risk-Free Interest Rate (r)__: The risk-free interest rate is the theoretical rate of return on an investment with zero risk of financial loss. It is often represented by the yield on government bonds. In the Black-Scholes model, the risk-free rate is used to discount the expected payoff of the option to present value.

__Option Price (C or P)__: The option price refers to the premium or cost of the option. The Black-Scholes model provides a formula to calculate the theoretical price of both call options (denoted as C) and put options (denoted as P).

Mathematical Expressions: 

Call Option Price (C):

$
C = S_0 \cdot N(d_1) - K \cdot e^{-rT} \cdot N(d_2)
$

Put Option Price (P):

$
P = K \cdot e^{-rT} \cdot N(-d_2) - S_0 \cdot N(-d_1)
$

Definitions of d1 and d2:

$
d_1 = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)T}{\sigma\sqrt{T}}
$

$
d_2 = d_1 - \sigma\sqrt{T}
$

where, 

$
N(d) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{d} e^{-\frac{x^2}{2}} \, dx
$

N(d) is the cumulative distribution function of the standard normal distribution.

__The Greeks__: The "Greeks" are various risk measures that describe how the option price is sensitive to various factors like the underlying asset's price, volatility, and time. Some common Greeks include:

1. __Delta ($\Delta$)__: Measures the sensitivity of the option price to changes in the underlying asset's price.

2. __Gamma ($\Gamma$)__: Measures the sensitivity of Delta to changes in the underlying asset's price.

3. __Theta ($\Theta$)__: Measures the sensitivity of the option price to the passage of time (time decay).

4. __Vega ($\nu$)__: Measures the sensitivity of the option price to changes in volatility.

5. __Rho ($\rho$)__: Measures the sensitivity of the option price to changes in the risk-free interest rate.

### Derivation of the Black-Scholes Equation

The Black-Scholes equation is a partial differential equation that describes the price of the option as a function of the underlying asset price and time. The derivation of this equation is based on constructing a risk-free portfolio and applying Ito's Lemma, which is a key result from stochastic calculus.

#### Step 1: Model Assumptions

1. The underlying asset price \( $S_t$ \) follows a geometric Brownian motion:

   $
   dS_t = \mu S_t dt + \sigma S_t dW_t
   $

   where:

   - \( $\mu$ \) is the drift rate (expected return) of the asset.

   - \( $\sigma$ \) is the volatility of the asset.

   - \( $W_t$ \) is a Wiener process (standard Brownian motion).

2. The risk-free rate \( r \) is constant over time.

3. No arbitrage opportunities exist.

#### Step 2: Portfolio Construction

Consider a portfolio \( $\Pi$ \) consisting of a long position in one option and a short position in \( $\Delta$ \) units of the underlying asset. The value of the portfolio at time \( t \) is:

$\Pi$ = V($S_t$, t) - $\Delta$ $S_t$

where \( V($S_t$, t) \) is the value of the option at time \( t \).

#### Step 3: Applying Ito's Lemma

Using [Ito's Lemma](https://en.wikipedia.org/wiki/It%C3%B4%27s_lemma), we can express the differential of the option price \( V \) as:

$
dV = \frac{\partial V}{\partial t} dt + \frac{\partial V}{\partial S} dS_t + \frac{1}{2} \frac{\partial^2 V}{\partial S^2} (dS_t)^2
$

Substituting the expression for \( $dS_t$ \) from the geometric Brownian motion model, we get:

$
dV = \frac{\partial V}{\partial t} dt + \frac{\partial V}{\partial S} (\mu S_t dt + \sigma S_t dW_t) + \frac{1}{2} \frac{\partial^2 V}{\partial S^2} \sigma^2 S_t^2 dt
$

Simplifying, we obtain:

$
dV = \left(\frac{\partial V}{\partial t} + \mu S_t \frac{\partial V}{\partial S} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial S^2}\right) dt + \sigma S_t \frac{\partial V}{\partial S} dW_t
$

#### Step 4: Eliminating Risk

For the portfolio \( $\Pi$ \) to be risk-free, the term involving \( $dW_t$ \) must be zero. Therefore, we set:

$
\Delta = \frac{\partial V}{\partial S}
$

Thus, the portfolio value becomes:

$
\Pi = V(S_t, t) - \frac{\partial V}{\partial S} S_t
$

The change in the portfolio value over a small time interval \( dt \) is:

$
d\Pi = dV - \Delta dS_t
$

Substituting the expressions for \( dV \) and \( $dS_t$ \), we get:

$
d\Pi = \left(\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial S^2}\right) dt
$

#### Step 5: No-Arbitrage Condition

Since the portfolio is risk-free, it must earn the risk-free rate \( r \). Therefore:

$
d\Pi = r\Pi dt
$

Substituting 

$
\Pi = V - S_t \frac{\partial V}{\partial S}
$

into the equation above:

$
\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial S^2} + r S_t \frac{\partial V}{\partial S} - r V = 0
$

#### Step 6: The Black-Scholes Equation
Rearranging the terms, we obtain the Black-Scholes partial differential equation:

$
\frac{\partial V}{\partial t} + \frac{1}{2} \sigma^2 S_t^2 \frac{\partial^2 V}{\partial S^2} + r S_t \frac{\partial V}{\partial S} - r V = 0
$

This equation is the foundation for pricing European options.

#### Boundary Conditions

For a European call option with strike price \( K \) and expiration time \( T \), the boundary condition is given by:

$
V(S_T, T) = \max(S_T - K, 0)
$

For a European put option, the boundary condition is:

$
V(S_T, T) = \max(K - S_T, 0)
$

The Black-Scholes equation, along with the boundary conditions, can be solved to find the price of European options.

### Solution of the Black-Scholes Equation with Boundary Conditions

To derive the explicit formulas for the European call and put options, we start by solving the Black-Scholes partial differential equation under the given boundary conditions.

The general solution to the Black-Scholes equation for a European call option is of the form:

$
C(S_t, t) = S_t N(d_1) - K e^{-r(T-t)} N(d_2)
$

For a European put option, the solution is:

$
P(S_t, t) = K e^{-r(T-t)} N(-d_2) - S_t N(-d_1)
$

where:

$
d_1 = \frac{\ln\left(\frac{S_t}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)(T-t)}{\sigma\sqrt{T-t}}
$

$
d_2 = d_1 - \sigma\sqrt{T-t}
$

Here, \( N(d) \) is the cumulative distribution function of the standard normal distribution.

### Applying the Boundary Conditions

1. **Call Option**: At maturity \( t = T \), the value of a call option is:

   $
   C(S_T, T) = \max(S_T - K, 0)
   $

   This condition reflects that the call option will be worth the difference between the stock price and the strike price if it is positive, and zero otherwise.

2. **Put Option**: At maturity \( t = T \), the value of a put option is:

   $
   P(S_T, T) = \max(K - S_T, 0)
   $

   This condition reflects that the put option will be worth the difference between the strike price and the stock price if it is positive, and zero otherwise.

To solve the Black-Scholes equation with these boundary conditions, we use the method of transforming variables and applying the Feynman-Kac theorem. This method leads to the closed-form solutions above for both call and put options.

### Final Black-Scholes Formulas

After applying the boundary conditions and solving the partial differential equation, we obtain the famous Black-Scholes formulas:

- **Call Option**:

  $
  C(S_0, t) = S_0 N(d_1) - K e^{-r(T-t)} N(d_2)
  $
  
- **Put Option**:

  $
  P(S_0, t) = K e^{-r(T-t)} N(-d_2) - S_0 N(-d_1)
  $

where:

$
d_1 = \frac{\ln\left(\frac{S_0}{K}\right) + \left(r + \frac{\sigma^2}{2}\right)T}{\sigma\sqrt{T}}
$

$
d_2 = d_1 - \sigma\sqrt{T}
$

These are the final pricing formulas for European call and put options derived from the Black-Scholes equation with the appropriate boundary conditions applied.
