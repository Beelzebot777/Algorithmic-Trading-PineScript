# **Piercing Line & Dark Cloud Cover Detector Documentation**

## **Overview**
The **Piercing Line & Dark Cloud Cover Detector** is a **Pine Script™ v6** indicator designed to identify and visualize the **Piercing Line** and **Dark Cloud Cover** candlestick patterns. These patterns are essential reversal signals in technical analysis, providing traders with key insights into potential market shifts.

This indicator highlights these patterns visually on the chart and is ideal for traders looking to identify potential bullish and bearish reversals in price action.

---

## **How It Works**

### **1. Pattern Logic**
The script identifies two key reversal patterns: **Piercing Line** (bullish reversal) and **Dark Cloud Cover** (bearish reversal).

#### **Piercing Line**
A **Piercing Line** is a bullish reversal pattern that occurs after a downtrend. It consists of **2 candles**:

1. **First Candle**: A large bearish candle.
2. **Second Candle**: A bullish candle that opens below the previous candle's low and closes beyond the midpoint of the first candle's body.

**Logic**:
- The first candle must be bearish (`open[2] > close[2]`).
- The second candle must be bullish (`open[1] < close[1]` and `open < close`).
- The closing price of the second candle must be greater than the midpoint of the body of the previous candle.

#### **Dark Cloud Cover**
A **Dark Cloud Cover** is a bearish reversal pattern that occurs after an uptrend. It consists of **2 candles**:

1. **First Candle**: A large bullish candle.
2. **Second Candle**: A bearish candle that opens above the previous candle's high and closes below the midpoint of the first candle's body.

**Logic**:
- The first candle must be bullish (`open[2] < close[2]`).
- The second candle must be bearish (`open[1] > close[1]` and `open > close`).
- The closing price of the second candle must be below the midpoint of the body of the previous candle.

---

### **2. Inputs & Customization**
This script does not currently provide user inputs, but it can be extended to allow users to customize **icon color**, **size**, and **offset** of the markers.

| **Feature**          | **Default** | **Description**                                           |
|----------------------|-------------|----------------------------------------------------------|
| Piercing Line Icon    | Green       | Indicates the Piercing Line pattern below the bar.        |
| Dark Cloud Cover Icon| Red         | Indicates the Dark Cloud Cover pattern above the bar.     |
| Text Labels          | C, D, N, P  | Letters indicating candle position in the pattern.        |
| Offset               | -1, -2      | Offsets to mark prior candles in the pattern.             |

---

### **3. Visual Indicators**
To provide clear feedback, the script uses **icons and labels** to highlight the patterns on the chart.

#### **Icons & Labels**
- **Dark Cloud Cover**: 
  - Three labels "C", "C", and "D" mark the candles forming the pattern. 
  - Plotted **above** the candles in **red**.

- **Piercing Line**: 
  - Three labels "N", "C", and "P" mark the candles forming the pattern. 
  - Plotted **below** the candles in **green**.

---

## **Script Logic**
The logic of the script is divided into two parts: 

### **1. Pattern Detection**
#### **Dark Cloud Cover**
- **Candlestick Direction**:
  - The second-to-last candle is bullish (`open[2] < close[2]`).
  - The previous candle is bearish (`open[1] > close[1]`).
  - The current candle is bearish (`open > close`).
- **Candlestick Sizes**:
  - The current candle's close must be below the low of the second-to-last candle.
  - The open of the second-to-last candle must be lower than the close of the previous candle.

#### **Piercing Line**
- **Candlestick Direction**:
  - The second-to-last candle is bearish (`open[2] > close[2]`).
  - The previous candle is bullish (`open[1] < close[1]`).
  - The current candle is bullish (`open < close`).
- **Candlestick Sizes**:
  - The current candle's close must be above the low of the second-to-last candle.
  - The open of the second-to-last candle must be higher than the close of the previous candle.

---

## **Functions Used**
| **Function**          | **Purpose**                                           |
|----------------------|------------------------------------------------------|
| `plotshape()`         | Plots icons and labels on the chart.                   |
| `offset`              | Sets the position of the shape relative to the candle.|

---

## **Visualization**
| **Visualization**          | **Color**          | **Placement**                                |
|---------------------------|-------------------|---------------------------------------------|
| **Dark Cloud Cover Label** | Red               | Above the bar.                              |
| **Piercing Line Label**     | Green             | Below the bar.                              |

---

## **Usage Tips**
- **Trend Reversals**: Use this indicator to identify key reversal points where the market may switch from bullish to bearish (Dark Cloud Cover) or from bearish to bullish (Piercing Line).
- **Combine with Indicators**: Combine it with other indicators like **Moving Averages (MA)**, **Relative Strength Index (RSI)**, or **Support/Resistance** for improved confirmation.
- **Backtesting**: Use this indicator in historical analysis to see how accurately it predicts reversals.

---

## **Summary**
The **Piercing Line & Dark Cloud Cover Detector** is a powerful Pine Script™ v6 indicator for identifying two crucial candlestick reversal patterns. By providing clear visual indicators for the **Piercing Line** and **Dark Cloud Cover**, this script allows traders to quickly recognize potential shifts in market momentum. The simple, clear design ensures usability for traders of all levels, and it can be customized to display additional indicators as needed.
