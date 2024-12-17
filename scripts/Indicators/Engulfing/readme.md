# **Bullish & Bearish Engulfing Detector Documentation**

## **Overview**
The **Bullish & Bearish Engulfing Detector** is a Pine Script indicator designed to identify and visualize **Bullish Engulfing** and **Bearish Engulfing** patterns on a TradingView chart. It applies criteria for **body size**, **volume**, and **trend analysis** to ensure the accurate detection of these powerful candlestick patterns.

This indicator also includes a **floating table** on the chart that tracks the total number of Bullish and Bearish Engulfing patterns detected during the current chart session. Users can customize the **lookback period** for trend validation, offering a more flexible approach to pattern detection.

---

## **Features**
- 📈 **Engulfing Pattern Detection**: Identifies and labels Bullish & Bearish Engulfing patterns on the chart.
- 📋 **Real-time Counting Table**: Displays the total number of Bullish and Bearish Engulfing patterns in a floating table.
- 🎨 **Customizable Lookback**: Allows users to customize the number of previous candles to check for a bullish or bearish trend.
- 🔥 **Volume Filter**: Ensures that only Engulfing patterns with increased volume are detected.
- 🛠️ **User Inputs**: Users can customize the lookback for trend detection and control the filtering logic.

---

## **How It Works**
### 🔥 **1. Pattern Detection**
The indicator identifies two specific types of patterns:

#### **Bullish Engulfing**
- The current candle is **bullish** (close > open).
- The previous candle is **bearish** (close < open).
- The current candle fully engulfs the body of the previous candle.
- **Volume** on the current candle is higher than the previous candle.
- A **downtrend** must be present before the Bullish Engulfing pattern (lookback period is customizable).

#### **Bearish Engulfing**
- The current candle is **bearish** (close < open).
- The previous candle is **bullish** (close > open).
- The current candle fully engulfs the body of the previous candle.
- **Volume** on the current candle is higher than the previous candle.
- An **uptrend** must be present before the Bearish Engulfing pattern (lookback period is customizable).

---

### 📋 **2. Customizable Inputs**
Users can customize the indicator to adapt it to different market conditions. Key inputs include:

- **Trend Lookback**: Users specify how many candles to check for a prior uptrend or downtrend before identifying an Engulfing pattern.  
  **Default**: 3 candles (can be set from 1 to 10).  

---

### 📈 **3. Volume Filter**
- The current candle must have higher volume than the previous candle to confirm a valid pattern.
- This ensures that the pattern is backed by sufficient market participation.

---

### 📋 **4. Trend Verification**
- **Bullish Engulfing** requires a **downtrend** prior to the pattern.
- **Bearish Engulfing** requires an **uptrend** prior to the pattern.
- The number of candles to check for the trend is customizable.
- **Downtrend**: Consecutive closes are lower than the previous close.
- **Uptrend**: Consecutive closes are higher than the previous close.

---

## **Logic and Conditions**
### 🕹️ **1. Bullish Engulfing Detection**
| **Condition**     | **Description** |
|-------------------|-----------------|
| `close > open`    | Current candle is bullish (green) |
| `close[1] < open[1]` | Previous candle is bearish (red) |
| `open <= close[1]`| Current candle opens below or at the prior close |
| `close >= open[1]`| Current candle closes above or at the prior open |
| **Volume filter**  | Volume of current candle > previous volume |
| **Trend requirement** | Downtrend before the pattern (number of candles configurable) |

---

### 🕹️ **2. Bearish Engulfing Detection**
| **Condition**     | **Description** |
|-------------------|-----------------|
| `close < open`    | Current candle is bearish (red) |
| `close[1] > open[1]` | Previous candle is bullish (green) |
| `open >= close[1]`| Current candle opens above or at the prior close |
| `close <= open[1]`| Current candle closes below or at the prior open |
| **Volume filter**  | Volume of current candle > previous volume |
| **Trend requirement** | Uptrend before the pattern (number of candles configurable) |

---

## **Customizable Inputs**
| **Input**         | **Type**        | **Description**                              | **Default** |
|-------------------|-----------------|---------------------------------------------|-------------|
| **Trend Lookback** | Integer         | Number of prior candles to check for trend | 3           |
| **Volume Filter**  | Boolean         | Only detect Engulfing patterns with higher volume than the previous candle | Yes          |

---

## **Visualization**
### 📈 **Bullish Engulfing**
- **Green arrow** below the candle.  
- **Text label "BE"** under the pattern.  

### 📈 **Bearish Engulfing**
- **Red arrow** above the candle.  
- **Text label "SE"** above the pattern.  

---

## **Counting Table**
A **real-time counting table** is displayed on the chart. This table tracks the total number of Bullish and Bearish Engulfing patterns detected during the current chart session.

### 📋 **Table Layout**
| **Engulfing Type**     | **Count** |
|------------------------|----------|
| **Bullish Engulfing**   | 5        |
| **Bearish Engulfing**   | 3        |

**How it works:**
- Each time a Bullish or Bearish Engulfing pattern is detected, the respective counter in the table is incremented.
- The table is displayed in the **bottom-right** corner of the TradingView chart.

---

## **Key Features**
| **Feature**            | **Description** |
|------------------------|-----------------|
| **Real-time Detection** | Marks Bullish & Bearish Engulfing patterns on the chart |
| **Counting Table**      | Tracks the total number of detected patterns |
| **Customizable Lookback**| Customizable trend lookback for better pattern validation |
| **Volume Filter**        | Ensures only Engulfing patterns with higher volume are detected |
| **Visual Alerts**       | Adds visual labels and arrows to highlight detected patterns |

---

## **Customization**
### 🛠️ **1. Input Customization**
- **Trend Lookback**: Customizable lookback period to identify uptrends and downtrends before an Engulfing pattern.
- **Volume Filter**: Enable or disable the volume filter to identify only high-volume patterns.

---

### 🎨 **2. Visual Customization**
- **Colors**: Customize the colors of Bullish and Bearish Engulfing patterns.
- **Shapes**: Use alternative symbols (circles, triangles, etc.) for pattern markers.
- **Labels**: Customize the text labels **"BE"** (Bullish) and **"SE"** (Bearish) displayed on the chart.

---

## **Usage Tips**
- **Increase Lookback for Stronger Patterns**:  
  Set **Trend Lookback** to 5-10 candles to detect only the strongest trends before Engulfing patterns.

- **Confirm with Volume**:  
  Enable the **Volume Filter** to confirm patterns backed by market participation.

- **Use on Higher Timeframes**:  
  Bullish & Bearish Engulfing patterns are more reliable on higher timeframes (e.g., 1-hour, 4-hour, daily).

- **Backtest for Optimal Settings**:  
  Test different combinations of **Trend Lookback** and **Volume Filter** to optimize the indicator for different assets.

---

## **Improvements**
Here are potential future improvements to this indicator:
- **Alerts**: Add alerts for Bullish & Bearish Engulfing patterns.
- **Dynamic Lookback**: Adapt the trend lookback based on market volatility.
- **Multi-Timeframe Support**: Allow detection of patterns from higher timeframes on lower timeframe charts.

---

## **Conclusion**
The **Bullish & Bearish Engulfing Detector** is a powerful indicator that identifies key reversal patterns in the market. By filtering weak patterns using volume and prior trends, it ensures that only the most **reliable patterns** are displayed.

With its **customizable inputs** and **real-time counting table**, this tool provides traders with essential information on market sentiment. It's ideal for traders looking for reliable reversal patterns on any asset class.
