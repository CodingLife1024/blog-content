# Black-Scholes Model: Introduction
## 20/08/2024 

The Black-Scholes model is a mathematical framework and algorithm for pricing European-style options, which are financial derivatives that give the holder the right, but not the obligation, to buy or sell an underlying asset at a specified price on a specified date.

### Introduction

Here are some basic definitions of some of the terms used in this model - 

__Strike Price (K)__: The strike price, also known as the exercise price, is the price at which the option holder can buy or sell the underlying asset. In the context of a call option, the strike price is the price at which the holder can purchase the asset. For a put option, it is the price at which the holder can sell the asset.

__Underlying Asset Price/Stock Price (S)__: The current price of the asset on which the option is written. This is the price that will be compared to the strike price to determine the payoff of the option at expiration.

__Volatility (\sigma)__: Volatility refers to the degree of variation in the price of the underlying asset over time. In the Black-Scholes model, volatility is a key input and is usually expressed as the standard deviation of the asset's returns. It reflects the market's expectation of the asset's future price fluctuations.