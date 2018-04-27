# REX

Ever wanted to play the stock market? Come on, it's 21st century. Time to teach the bot to play for you.

REX is an OpenAI Gym environment that simulates a cryptocurrency exchange in multi-agent setting. It comes with preprogrammed bots that trade according to simple strategies (MACD, RSI) - these can be used to simulate the behavior of other market participants (which your model should counter-trade). REX is different in the following ways:

1. **State** is a sequence of raw trades (not candles). You can, of course, roll trades into candles, but this way you'll lose valuable information (e.g. there was a huge volume spike - was that a "buy" or a "sell"? Who's got the FOMO: buyers or sellers?). Raw trades, by definition, are lossless - they provide complete information about the market.
1. **Action** is a float that represents "percentage offset from midpoint between bid & ask". For example, if bid = 8000.0, ask = 8010.0, an action of 0.01 would result in a placement of a sell order at 8005.8005 (`(8010.0 + 8000.0) / 2 + 0.01% = 8005.8005`). And yes, the action of 0.0 is heavily penalized. Your bot should always have an order in the market - even if it's some stink bid to catch fat-finger dumps.


## Philosophy

We believe that:

1. Machine learning is the most promising field of computer science.
1. Reinforcement learning is the most promising field of machine learning.
1. Solving the hardest problems is the fastest way to advance any field of science.
1. Winning in a multi-agent continuously-evolving environment is the hardest problem of reinforcement learning.
1. Market is the purest form of multi-agent continuously-evolving environment.

Therefore, developing profitable trading algorithms is the best way to advance computer science.

