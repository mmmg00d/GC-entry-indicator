# GC 1min Entry Areas Trading Strategy

A TradingView Pine Script strategy for identifying potential long entries on Gold Futures (GC)

## Overview

Pine Script was developed with the free version of Claude in about a month during Dec 2025/Jan 2026 based on observations I've made over the past year or so. Objective: identify price ranges that represent potential unfilled orders and "tag along" when price retraces to that price range. 

As of Jan 2026, I'm beginning to evaluate the output of the automated testing script (strategy_script.pine) using Python. Rough analysis so far, but the hours of 7-9am ET yield the most winning trades using about 21 weeks of backtesting data. 


#### Stable version:
Using all trades from 7-9am ET, the strategy is profitable, although a trailing drawdown limit of $6500 would have been exceeded (where $6500 is the max buffer and ratchets up only after a winning trade). Analysis uses default values of $500 and 2.5RR for position size and price target, respectively.


#### Experimental version (and possible next steps):
1) How does P/L change after removing overlapping entry areas? (see screenshot of parameter selected to remove overlapping entry areas)
2) Review raw data of winning trades from 7-9am ET...qualitatively, do these trades share any charateristics?
3) Test a hunch/observation: Sunday evening price action seems to often reveal large "pops" when profitable trades occur - is this true? What hours generally contain these "pops" and is that timeframe profitable?
4) If the P/L is insufficient and/or the trailing drawdown is hit, adjust the parameters and retest using the same 21-week period. Since my best trades occured after a large "pop," I could test entries occuring after larger "pops." Potential things to test: larger FVG size, ratio of FVG to entry area (larger?...need to collect a few examples)


#### Quips and brief reflections:
Testing and revising the experimental branch while reading "Fooled by Randomness" by Nassim Nicholas Taleb (mid-Jan 2026). Perhaps like previous strategies I've tested over the past couple years, the successful GC trades I've observed and executed may be governed by a discretionary component and/or influenced by luck; I currently don't know the significance of those factors, which may oscure a systematic approach.




#### Example
Screenshot taken on Sunday, Jan 11 2026 as GC made yet another new ATH

<img width="916" height="800" alt="image" src="https://github.com/user-attachments/assets/1c16cc79-a1e9-4eee-9427-ed67a982b09b" />

#### Distribution of winning and losing trades (stable version)
<img width="1113" height="549" alt="image" src="https://github.com/user-attachments/assets/061e71a7-9a59-4140-b249-873d08404421" />


#### P/L (stable version)

<img width="1095" height="545" alt="image" src="https://github.com/user-attachments/assets/423cad57-b8f2-491b-b016-a961240cc621" />

## Strategy Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| Max Candles from Fractal to FVG | 10 | Maximum distance between fractal and FVG |
| Minimum FVG Size | 5 ticks | Smallest gap considered a valid FVG |
| Max Entry Area Size | 50 ticks | Largest allowed entry area |
| Risk/Reward Ratio | 2.5 | Target profit as multiple of risk |
| Remove Overlaps | false | Keep only the lowest overlapping entry area |



### Experimental Version


#### Removing Overlapping Entry Areas

Parameter that removes overlapping entry areas

<img width="375" height="429" alt="image" src="https://github.com/user-attachments/assets/6e3fd423-ef5f-40ed-913d-83849cad9c99" />


Left: all entry areas. Right: entry areas after removing overlapping entry areas. (Monday, Jan 12 2026 approx 12:30am ET) 

<img width="1639" height="717" alt="image" src="https://github.com/user-attachments/assets/f9d51d30-ed34-43d1-916c-d7bb7638e482" />



#### Distribution of winning and losing trades (experimental version)

<img width="1111" height="542" alt="image" src="https://github.com/user-attachments/assets/9dafeaa5-625e-4f4c-8159-4ea468a2a87d" />

#### P/L (experimental version)

<img width="1113" height="542" alt="image" src="https://github.com/user-attachments/assets/2610d891-909e-40d0-9daa-968370053fdb" />


#### Results and Interpretations (experimental version)
Using the same 21-week period, I collected and analyzed testing results after selecting the parameter to remove overlapping entry areas. As expected, the total number of valid trades decreased. Removing overlapping entries reduced the win rate and profitability, and drawdown reached a lower minimum. So, simply using only "fresh" entry areas that are not overlapped does not lead to better P/L results. 




## Performance Considerations

### Known Limitations

- Strategy can only hold one position at a time
- Entry areas created during active trades may be missed if price moves away before the trade closes
- Uses limit orders at top of entry area (may miss fills in fast markets)
- Backtest results may differ from live performance due to slippage and execution delays


## Disclaimer

This strategy is for educational and research purposes only. 


---

*Last updated: Jan 19 2026*
