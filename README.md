# GC 1min Entry Areas Trading Strategy

A TradingView Pine Script strategy for identifying potential long entries on Gold Futures (GC)

## Overview

Pine Script was developed with the free version of Claude in about a month during Dec 2025/Jan 2026 based on observations I've made over the past year or so. Objective: identify price ranges that represent potential unfilled orders and "tag along" when price retraces to that price range. Default price target is 2.5RR. 

As of Jan 2025, I'm beginning to evaluate the output of the automated testing script (strategy_script.pine) using Python. Rough analysis so far, but the hours of 7-9am ET yield the most winning trades using about 6 weeks of backtesting data. 

## Repository Contents

```
├── indicator_script.pine          # TradingView indicator for visualization
├── strategy_script.pine           # TradingView strategy for backtesting
├── strategy_output.xlsx           # Trade results exported from TradingView
├── gc entries.ipynb               # Python notebook for performance analysis
└── README.md                      # This file
```

## Strategy Logic

### Entry Area Formation

1. **Fractal Detection**: Identifies fractals (5-candle patterns)
   - High fractals mark potential resistance
   - Low fractals mark potential support

2. **FVG Trigger**: When a Fair Value Gap (FVG) occurs:
   - Finds the closest high and low fractals
   - Creates an entry area between these fractals

3. **Validation Criteria**:
   - Price must close above the high fractal
   - FVG must occur within X candles of the fractal (default: 10)
   - Entry area must be within size limit (default: 50 ticks)
   - Minimum FVG size (default: 5 ticks)

### Trade Execution

- **Entry**: Limit order at the top of the entry area
- **Stop Loss**: 1 tick below the low fractal
- **Take Profit**: 2.5x the risk distance above entry
- **Invalidation**: Entry area removed if price wicks 1 tick below the bottom

### Key Features

- Tracks multiple entry areas simultaneously
- Handles overlapping entry areas (optional removal of higher overlaps)
- Visual entry area boxes with dashed borders when touched
- Timestamps for entry areas older than 1 day

## Files Description

### `indicator_script.pine`

The indicator version for chart visualization:
- Displays entry areas as blue boxes
- Shows fractal markers (▼ for highs, ▲ for lows)
- Entry areas turn dashed when price enters them
- Includes commented-out alert functionality
- Optional overlap removal feature

**Parameters**:
- Max Candles from Fractal to FVG: 10
- Minimum FVG Size (ticks): 5
- Max Entry Area Size (ticks): 50
- Show Fractal Markers: true
- Remove Overlapping Entry Areas: false

### `strategy_script.pine`

The strategy version for backtesting:
- All indicator features plus trade execution
- Records entries at the top of entry areas
- Exits at precise TP/SL levels using limit/stop orders
- Tracks performance metrics

**Additional Parameters**:
- Risk/Reward Ratio: 2.5

### `testing 1 Dec - 9 Jan.xlsx`

Excel file containing trade results exported from TradingView's Strategy Tester:
- Trade list with entry/exit prices and times
- Win/loss statistics
- Profit factor and other performance metrics
- Maximum drawdown information

### `gc entries.ipynb`

Python Jupyter notebook for analyzing strategy performance:
- Loads trade data from Excel
- Basic descriptive stats (Distribution of Winning and Losing trades by entry hour)

## Installation & Usage

### TradingView Setup

1. Open TradingView and navigate to Gold Futures (GC) 1-minute chart
2. Open Pine Editor
3. For visualization:
   - Copy contents of `indicator_script.pine`
   - Click "Add to Chart"
4. For backtesting:
   - Copy contents of `strategy_script.pine`
   - Click "Add to Chart"
   - Open Strategy Tester tab to view results

### Exporting Trade Data

1. Run the strategy script on your desired timeframe
2. Open Strategy Tester panel
3. Click "List of Trades"
4. Export to Excel/CSV

### Python Analysis

1. Install required packages:
```bash
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

2. Launch Jupyter notebook:
```bash
jupyter notebook analysis_notebook.ipynb
```

3. Update the file path to your `strategy_output.xlsx`
4. Run all cells to generate analysis

## Strategy Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| Max Candles from Fractal to FVG | 10 | Maximum distance between fractal and FVG |
| Minimum FVG Size | 5 ticks | Smallest gap considered a valid FVG |
| Max Entry Area Size | 50 ticks | Largest allowed entry area |
| Risk/Reward Ratio | 2.5 | Target profit as multiple of risk |
| Remove Overlaps | false | Keep only the lowest overlapping entry area |

## Performance Considerations

### Known Limitations

- Strategy can only hold one position at a time
- Entry areas created during active trades may be missed if price moves away before the trade closes
- Uses limit orders at top of entry area (may miss fills in fast markets)
- Backtest results may differ from live performance due to slippage and execution delays


## Disclaimer

This strategy is for educational and research purposes only. 


---

*Last updated: 11 January 2026*
