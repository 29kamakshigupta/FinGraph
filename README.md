# FinGraph

FinGraph is a finance analysis workspace with **two complementary systems**:

1. **Trading Agent** — a terminal-based investment assistant built with **LangGraph**, market/news retrieval, and a final risk-based recommendation flow.
2. **Stock Network Analyzer** — a web-based analytics tool for exploring relationships between stock prices with **Streamlit**, **NetworkX**, and **Plotly**.

It is designed so you can use either system independently or combine both for broader market insight.

---

## Features

### Trading Agent
- Fetches live market data with `yfinance`
- Pulls recent news using `Tavily` or a mock fallback
- Uses a multi-step agent pipeline for:
  - market analysis
  - news sentiment analysis
  - risk-based final decisioning
- Returns a clear recommendation such as **BUY**, **HOLD**, or **SELL**
- Includes long-term memory persistence with SQLite

### Stock Network Analyzer
- Interactive Streamlit dashboard
- Correlation network visualization
- Lagged correlation analysis
- Time-series comparison charts
- Summary statistics for selected tickers
- Standalone terminal script for quick analysis

### Project Utilities
- Validation / testing scripts mentioned in the repo docs
- Docker support
- Modular code structure for easier extension

---

## Tech Stack

- **Python**
- **TypeScript**
- **LangGraph**
- **LangChain Core**
- **yfinance**
- **Tavily / web search**
- **Streamlit**
- **Plotly**
- **NetworkX**
- **Pandas**
- **Docker**

---

## Repository Structure

```bash
FinGraph/
├── main.py
├── requirements.txt
├── .env.example
├── src/
│   └── trading_agent/
│       ├── agents.py
│       ├── graph.py
│       ├── state.py
│       ├── config.py
│       ├── tools/
│       │   ├── market_data.py
│       │   └── web_search.py
│       └── memory/
│           └── long_term.py
├── stock_network/
│   ├── app.py
│   ├── demo.py
│   ├── data_fetch.py
│   ├── processing.py
│   ├── analysis.py
│   ├── graph_builder.py
│   └── visualization.py
├── validate_system.py
├── validate_pipeline.py
├── test_pipeline.py
└── docs/
```

> Note: the repo docs also mention files such as `QUICKSTART.md`, `INDEX.md`, `CHANGES_SUMMARY.md`, and `HF_SPACE_USAGE.md` for setup, architecture, and deployment guidance.

---

## Getting Started

### 1) Install dependencies

```bash
pip install -r requirements.txt
```

If you are running the stock network app separately, install its extra dependencies as described in that module’s docs.

### 2) Set environment variables

For the trading agent:

```bash
export NVIDIA_API_KEY="your_key_here"
export TAVILY_API_KEY="your_key_here"
```

You can also create a `.env` file if you prefer.

### 3) Run the trading agent

```bash
python main.py
```

### 4) Run the stock network analyzer

From the stock network directory:

```bash
python demo.py AAPL,MSFT,GOOGL,NVDA
```

Or launch the web UI:

```bash
streamlit run app.py
```

---

## How It Works

### Trading Agent Flow
1. User enters a question such as: “Should I buy AAPL?”
2. The system fetches market data and recent news.
3. A market agent analyzes price action and volatility.
4. A news agent analyzes sentiment and event impact.
5. A risk agent combines the signals into a final recommendation.

### Stock Network Flow
1. The user provides a list of stock tickers.
2. The app fetches and aligns price data.
3. It computes returns, correlations, and lagged relationships.
4. A graph is built to visualize stock clusters and dependencies.
5. Results are shown in charts, matrices, and summary tables.

---

## Example Usage

### Trading Agent
```text
You: Should I buy Apple stock right now?

Agent: Based on the current market conditions...
Risk Level: Medium
Recommendation: HOLD
Confidence: 65%
```

### Stock Network Analyzer
```text
python demo.py AAPL,MSFT,GOOGL,NVDA
```

This can output:
- return statistics
- correlation matrix
- lagged correlation results
- network metrics
- detected clusters

---

## Validation

The repo docs mention validation scripts for checking setup and pipeline behavior. A typical flow is:

```bash
python validate_system.py
python validate_pipeline.py
python test_pipeline.py
```

---

## Configuration

Common environment variables used by the project:

- `NVIDIA_API_KEY` — for the model-backed trading agent
- `TAVILY_API_KEY` — for news / search integration

The system is designed with fallbacks so it can still run in a limited mode when some external services are unavailable.

---

## Troubleshooting

### Missing module errors
Reinstall dependencies:

```bash
pip install -r requirements.txt
```

### API key issues
Check that your environment variables are set correctly.

### No market data returned
- Verify the ticker symbol
- Check internet access
- Try a shorter analysis period

### Streamlit port already in use
```bash
streamlit run app.py --server.port=8502
```

---

## Roadmap Ideas

- Add portfolio-level analysis
- Improve sector-level sentiment aggregation
- Add alerting / watchlist features
- Extend visual analytics with more indicators
- Combine the chatbot and network analyzer into one unified dashboard

---

## License

Add a license file if you want to make usage terms explicit.

---

## Acknowledgements

Built with open-source tools and finance data libraries including LangGraph, yfinance, Streamlit, Plotly, and NetworkX.
