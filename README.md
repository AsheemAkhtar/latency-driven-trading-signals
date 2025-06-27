# latency-driven-trading-signals
# Quant Cross-Market Signals 📉📈

This repository contains a high-frequency trading (HFT)-inspired analysis of the TRB/USDT pair on Binance. The goal is to uncover predictive relationships between the **spot** and **perpetual futures** markets using sudden price movements within short timeframes (3–5 milliseconds). This is a latency-sensitive, event-driven project designed for quantitative trading signal research.

---

## 🧠 Objectives

### 🎯 Primary Goals
- Predict price changes in the **spot** market based on **futures** market movements (and vice versa).
- Generate actionable **signals** for trading both markets with a 5ms prediction horizon.

### 🧩 Secondary Goals
- Determine which market (Spot or Perpetual) **leads price discovery**.
- **Detect noise** — sudden price changes that do not propagate.
- **Estimate momentum quality** — how long and how far a price move persists.
- Integrate **trade-level data** to study volume and market-maker behavior during events.

---

## 📦 Dataset

This project uses real-time, timestamped Binance export data:

| File Name                        | Description                         |
|----------------------------------|-------------------------------------|
| `trb_usdt_spot_export.csv`       | Spot order book (best bid/ask)      |
| `trb_usdt_futures_export.csv`    | Perpetual futures order book        |
| `trb_usdt_trades_export.csv`     | Executed trades (price, quantity)   |

Timestamps are in millisecond precision, but are **irregular** — multiple entries may exist per millisecond, or gaps of 100+ ms may appear.

---

## 📈 Methodology

### ✅ Event Detection
- Defined a **sudden move** as a ≥ ±7 basis points change within **3ms**.
- Used mid-price = (bid + ask) / 2 for accuracy.

### 🔁 Cross-Market Prediction
- After detecting an event in Spot, searched for a price response in Futures within **5ms**, and vice versa.

### 🚫 Noise Characterization
- Events with < 1 bps impact on the opposite market were labeled as **noise**.

### 🧮 Momentum Estimation
- Checked how long a price continues in the direction of the move.
- Added **trade metrics**: number of trades, market-maker ratio, and total quantity.

---

## 📂 Repository Structure

