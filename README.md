# REX

So, you want to play the stock market? Come on, it's 21st century... Time to teach the machine to play for you.

REX is an OpenAI Gym environment that simulates a cryptocurrency exchange in multi-agent setting. It comes with preprogrammed bots that imitate the behavior of other market participants. Compared to a traditional backtesting environment, REX is better in the following ways:

1. REX simulates slippage & spread by maintaining a full orderbook.
1. REX simulates API delays by sending data to agents & executing their orders in batch.
1. REX simulates change of market conditions by training multiple agents simultaneously. 

As a reinforcement learning environment, REX uses the following definitions:

1. **State** is a tuple of current position size + sequence of raw trades (not candles). You can, of course, roll trades into candles, but this way you'll lose valuable information (e.g. there was a huge volume spike - was that a "buy" or a "sell"? Who's got the FOMO: buyers or sellers?). Raw trades, by definition, are lossless - they provide complete information about the market.
1. **Action** is a single order (two floats for "price offset" and "amount"). "Price offset" represents "percentage offset from midpoint between bid & ask". For example, if bid = 8000.0, ask = 8010.0, an action of 0.01 would result in a placement of a sell order at 8005.8005 (`(8010.0 + 8000.0) / 2 + 0.01% = 8005.8005`). And yes, your agent should always produce an action to keep an order in the market - even if it's a stink bid to catch fat-finger dumps.

For simplicity, we recommend setting "amount" to constant and focusing on "price offset". If you decide to operate in the market using a different amount, you'd better retrain the agent, since the order size influences the behavior of market participants (large bids move the price up without being filled).

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
