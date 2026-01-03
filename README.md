# Meta-Learning Based Stock Prediction & Portfolio Optimization

A production-grade machine learning system that combines LSTM-based stock price forecasting with Model-Agnostic Meta-Learning (MAML) to enable rapid adaptation across financial assets and drive intelligent portfolio allocation.

---

## Overview

This project implements a comprehensive financial forecasting and portfolio optimization pipeline that addresses a critical challenge in quantitative finance: **how to quickly adapt predictive models to new assets with limited historical data**.

The system consists of three core components:

1. **LSTM-based stock price forecasting** using raw OHLCV data and technical indicators
2. **Model-Agnostic Meta-Learning (MAML)** framework that enables rapid adaptation to unseen stocks with minimal training data
3. **Reliability-weighted portfolio optimization** that integrates prediction confidence into Markowitz mean-variance optimization

Unlike traditional approaches that require retraining from scratch for each new asset, this meta-learning framework learns a generalizable initialization that can adapt to new stocks in just a few gradient steps, making it practical for real-world deployment scenarios.

---

## Key Highlights

- **Smart LSTM Architecture**: Dual-path LSTM combining raw OHLCV data with feature-engineered technical indicators, with learned weighting based on performance
- **MAML Framework**: Fast adaptation to unseen stocks using only a small support set, reducing training time from hours to minutes
- **Reliability-Weighted Optimization**: Portfolio allocation constraints based on prediction confidence (MAPE), preventing over-allocation to unreliable predictions
- **Comprehensive Backtesting**: Performance comparison against equal-weighted and classical Markowitz portfolios across multiple market conditions
- **Modular Design**: Clean, reproducible notebook-based experimentation suitable for research and production deployment

---

## Notebooks Description

### `LSTM.ipynb`
Baseline and enhanced LSTM models for stock price prediction across multiple sectors (Technology, Financial, Healthcare, Energy). Includes:
- Basic LSTM implementation with OHLCV features
- Enhanced models with technical indicators (MA, RSI, MACD, Bollinger Bands)
- Smart feature selection strategy based on model performance
- Sector-wise performance analysis and visualization

### `META-LEARNING.ipynb` / `META-LEARNING-UPDATED 1.ipynb`
Complete MAML implementation with Smart LSTM architecture for meta-learning across stocks. Includes:
- **SmartLSTM Class**: Dual-path architecture with raw and feature-enhanced LSTMs
- **MAML Framework**: Inner-loop adaptation and outer-loop meta-update
- **DataProcessor**: Technical indicator engineering and sequence generation
- **PortfolioOptimizer**: Markowitz mean-variance optimization with reliability constraints
- **MAMLPortfolioManager**: End-to-end pipeline from prediction to portfolio construction
- **Backtesting System**: Performance evaluation against baseline strategies

---

## Methodology

### Data Preprocessing
- Historical stock data retrieval via yfinance
- Technical indicator calculation (moving averages, RSI, MACD, Bollinger Bands)
- Sequence generation for time-series modeling (60-day lookback windows)
- MinMax scaling for feature normalization

### LSTM & Smart LSTM Modeling
- Standard LSTM networks with dropout regularization
- Dual-path architecture: raw OHLCV data and feature-enhanced inputs
- Performance-based weighting between raw and feature paths
- Early stopping and validation-based model selection

### Meta-Learning with MAML
- **Meta-Training**: Learn a generalizable initialization across multiple stocks (tasks)
- **Inner Loop**: Fast adaptation to each stock using support set (5 gradient steps)
- **Outer Loop**: Meta-update based on query set performance across all tasks
- **Quick Adaptation**: New stocks can be integrated with minimal data (60% support, 40% query split)

### Portfolio Construction
- Expected returns derived from MAML predictions (forward-looking)
- Covariance matrix calculated from historical returns (risk estimation)
- Reliability-weighted constraints: MAPE-based allocation caps prevent over-exposure to unreliable predictions
- Sharpe ratio maximization subject to constraints

### Backtesting & Evaluation
- Three-strategy comparison:
  1. **MAML-Optimized**: Reliability-weighted portfolio using MAML predictions
  2. **Traditional Markowitz**: Historical data-driven optimization
  3. **Equal-Weighted**: Baseline benchmark
- Performance metrics: Cumulative returns, Sharpe ratio, maximum drawdown, annualized volatility

---

## Results Summary

- **Fast Adaptation**: MAML models adapt to new stocks in 5 gradient steps vs. full retraining
- **Improved Performance**: MAML-driven portfolios show superior risk-adjusted returns compared to equal-weighted and traditional Markowitz strategies in historical backtests
- **Robustness**: Consistent performance across multiple sectors and market conditions
- **Reliability Integration**: MAPE-based constraints successfully prevent over-allocation to high-error predictions (e.g., volatile stocks like TSLA)

---

## Tech Stack

- **Python 3.8+**
- **TensorFlow/Keras**: Deep learning framework
- **NumPy, Pandas**: Numerical computing and data manipulation
- **Scikit-learn**: Preprocessing and metrics
- **Matplotlib, Seaborn**: Visualization
- **yfinance**: Financial data retrieval
- **SciPy**: Portfolio optimization
- **Jupyter Notebook**: Interactive development and experimentation

---

## How to Run

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Installation

```bash
# Clone the repository
git clone <repo-url>
cd META-LEARNING

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook
```

### Execution
1. Open `LSTM.ipynb` for baseline LSTM experiments
2. Open `META-LEARNING-UPDATED 1.ipynb` for the complete MAML pipeline
3. Ensure data files (if any) are in the project directory
4. Run cells sequentially; notebooks are self-contained

**Note**: The notebooks download stock data automatically via yfinance. Ensure internet connectivity for data retrieval.

---

## Resume-Ready Summary

> Built a meta-learning–driven financial forecasting system using LSTM and MAML to enable rapid adaptation across stocks and drive portfolio optimization, outperforming classical allocation strategies in historical backtests. The system combines dual-path LSTM architectures with Model-Agnostic Meta-Learning to learn generalizable stock prediction models that adapt to new assets in minutes rather than hours. Integrated prediction confidence (MAPE) into Markowitz portfolio optimization to create reliability-weighted allocation constraints, resulting in improved risk-adjusted returns compared to equal-weighted and traditional optimization strategies.

---

## Project Structure

```
META-LEARNING/
├── LSTM.ipynb                          # Baseline LSTM experiments
├── META-LEARNING.ipynb                 # MAML implementation (original)
├── META-LEARNING-UPDATED 1.ipynb       # MAML implementation (updated)
├── DL_PAPER-R026,61,62 (1).pdf        # Research paper reference
├── requirements.txt                    # Python dependencies
├── .gitignore                          # Git ignore rules
└── README.md                           # This file
```

---

## Future Enhancements

- Real-time data pipeline integration
- Multi-asset class support (bonds, commodities, crypto)
- Reinforcement learning for dynamic portfolio rebalancing
- Alternative meta-learning algorithms (Reptile, FOMAML)
- Production API deployment

---

## Disclaimer

This project is for **educational and research purposes only**. The models, predictions, and portfolio strategies presented here are not financial advice. Past performance does not guarantee future results. Always consult with qualified financial professionals before making investment decisions.

---

## License

This project is provided as-is for educational purposes. Use at your own risk.

---

## Contact

For questions, suggestions, or collaboration opportunities, please open an issue or contact the repository maintainer.

