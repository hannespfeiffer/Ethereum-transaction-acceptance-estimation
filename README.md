# Ethereum transaction acceptance estimation

An attempt to use probabilistic programming (Pyro) to infer how much one needs to pay for gas, to get one's transaction of at least $2000 of a stable  (USDT, USDC, DAI) accepted in the next block with 50% certainty. **Note:** code was written pre-EIP1559

Disclaimer: This repo should not be seen as rigorous, production ready code; moreso a simple study of probabilistic programming. The code was mostly adapted from one of the Pyro examples (link in notebook).

**Ethereum transactions and the Mempool**


![blocks](https://user-images.githubusercontent.com/20343898/112629852-1748f400-8e35-11eb-8c5f-c6fa32a5e0d0.png)


Given transaction event observations of 4 blocks (transactions entering the Mempool and transactions getting confirmed/stuck), we try to infer, how high the gas price would need to be, in order for a transaction to be accepted with 50% probability. The probability of getting accepted is modeled via a sigmoid function (logistic regression). This probability is used to sample from a Bernoulli distribution. As starting points for the priors, several parameter settings were explored, mainly using the (proprietarily computed by API provider) confidence levels of the same API, which start at 70% and go up to 99%. 

**Results for block 12108388:**

![image](https://user-images.githubusercontent.com/20343898/112632044-e9b17a00-8e37-11eb-9d9b-c9c58123fd96.png)


 
Both graphs show the prior and posterior(s). The first graph shows the prior gas price distribution, at which's mean (the API provider guessed) ~70% of transactions should be accepted and our posterior gas price distribution, at which's mean (we inferred) 50% should be accepted. The second graph visualizes how the posterior evolves through seeing more data. Blue is less data and green is more data.
