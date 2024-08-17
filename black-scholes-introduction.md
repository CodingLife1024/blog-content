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