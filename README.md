# REX

So, you want to play the stock market? Come on, it's 21st century... Time to teach the machine to play for you.

REX is an OpenAI Gym environment that simulates a cryptocurrency exchange in multi-agent setting. It comes with preprogrammed bots that imitate the behavior of other market participants. Compared to a traditional backtesting environment, REX is better in the following ways:

1. REX simulates slippage & spread by maintaining a full orderbook.
1. REX simulates API delays by sending data to agents & executing their orders in batch.
1. REX simulates change of market conditions by training multiple agents simultaneously. 

As a reinforcement learning environment, REX uses the following definitions:

1. **State** is a tuple of `(current position size, bid, ask, trade history)`. You can, of course, convert trades into candles, but this way you'll lose valuable information (e.g. there was a huge volume spike - was that a "buy" or a "sell"? Who's got the FOMO: buyers or sellers?). Raw trades, by definition, are lossless - they provide complete information about the market.
1. **Action** is a single order - a tuple of `(price, amount)`. The agent should always produce an action to keep an order in the market - even if it's a stink bid to catch fat-finger dumps. Positive amount means placing a buy order, negative amount means placing a sell order.
1. **Reward** is profit or loss - `(price of exit order - price of entry order) * amount`. An agent only receives reward when his current position size reaches zero (or changes sign, which may happen if the agent decides to completely reverse his position with a single order).

The agent can also "short" (borrow an asset and sell it in anticipation of a price decline). In this case, the agent should specify amount as negative number (to place a sell order). Note that some exchanges don't support shorting.

## Recommendations

* Try to set "amount" to constant and focus on "price". If you decide to operate in the market using a different amount, you'd better retrain the agent, since the order size influences the behavior of market participants (large bids move the price up without being filled).
* Try to produce "price offset" instead of "price". "Price offset" represents "percentage offset from midpoint between bid & ask". For example, if bid = 8000.0, ask = 8010.0, an action of 0.01 would result in a placement of a sell order at 8005.8005 (`(8010.0 + 8000.0) / 2 + 0.01% = 8005.8005`).
* Try to train a single agent for a single market: the winning strategies for distinct markets may be vastly different (for example, some altcoins can't be shorted, so the agent can sell only after buying)

## Philosophy

We believe that:

1. Machine learning is the most promising field of computer science.
1. Reinforcement learning is the most promising field of machine learning.
1. Solving the hardest problems is the fastest way to advance any field of science.
1. Winning in a multi-agent continuously-evolving environment is the hardest problem of reinforcement learning.
1. Market is the purest form of multi-agent continuously-evolving environment.

Therefore, developing profitable trading algorithms is the best way to advance computer science.

## Contributing

1. Clone this repository.
1. [Install Conda](https://conda.io/docs/user-guide/install/index.html).
1. `conda env create -f environment.yml`
1. `source activate gym-rex`
1. `pip install -r requirements.txt`
1. `python examples/macd.py # make sure it works`
