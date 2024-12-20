# **EMA & RSI Bullish & Bearish Detector Documentation**

## **Overview**
The **EMA & RSI Bullish & Bearish Detector** is a **Pine Script™ v6** indicator designed to identify bullish and bearish trends using a combination of **Exponential Moving Averages (EMAs)**, **Relative Strength Index (RSI)**, and **Stochastic Oscillator**. This script provides dynamic buy and sell signals, and allows users to configure RSI and Stochastic thresholds for overbought and oversold zones. Additionally, it features a **trend table** in the bottom-right corner of the chart to display the current trend for the selected timeframe.

This indicator is ideal for traders looking to combine multiple technical analysis tools to identify high-probability trading opportunities.

---

## **How It Works**

### **1. Inputs**
The script includes various input parameters grouped into sections for better organization. These inputs allow users to customize EMA periods, RSI thresholds, Stochastic settings, and the timeframe for the trend analysis.

| **Parameter**             | **Default** | **Description**                                               |
|--------------------------|-------------|-------------------------------------------------------------|
| Select Timeframe Trend   | 60          | Timeframe for trend calculation (options: 1H, 4H, D, W, M).  |
| Short EMA Period         | 10          | Period for the short EMA.                                    |
| Long EMA Period          | 55          | Period for the long EMA.                                     |
| RSI Period               | 14          | Period for the RSI calculation.                              |
| Overbought Level         | 67          | RSI value indicating an overbought condition.               |
| Oversold Level           | 33          | RSI value indicating an oversold condition.                 |
| Stochastic %K Period     | 14          | Period for the Stochastic %K calculation.                   |
| Stochastic %D Smoothing  | 3           | Smoothing factor for the %D line of the Stochastic.         |
| Stochastic Smoothing     | 3           | Smoothing factor for the %K line of the Stochastic.         |
| Stochastic Overbought Level | 80       | Stochastic value indicating an overbought condition.        |
| Stochastic Oversold Level | 20         | Stochastic value indicating an oversold condition.          |

---

### **2. Features**

#### **a) Exponential Moving Averages (EMAs)**
The script calculates two EMAs (short and long) for the selected timeframe. Crossovers between these EMAs are used to determine the **main trend**:
- **Bullish Trend**: Short EMA crosses above the Long EMA.
- **Bearish Trend**: Short EMA crosses below the Long EMA.

#### **b) Relative Strength Index (RSI)**
The RSI is calculated based on the current chart interval to identify overbought and oversold conditions:
- **Overbought**: RSI exceeds the overbought level.
- **Oversold**: RSI falls below the oversold level.

#### **c) Stochastic Oscillator**
The Stochastic Oscillator is used to refine buy and sell signals by identifying crossovers between the %K and %D lines in overbought and oversold zones:
- **Bullish Signal**: %K crosses above %D in the oversold zone.
- **Bearish Signal**: %K crosses below %D in the overbought zone.

#### **d) Dynamic Buy/Sell Signals**
Based on the **main trend**:
- In a **Bullish Trend**, signals include **"BUY"** and **"CLOSE SELL"**.
- In a **Bearish Trend**, signals include **"SELL"** and **"CLOSE BUY"**.

#### **e) Trend Table**
A **dynamic table** is displayed in the bottom-right corner of the chart to show the current trend for the selected timeframe.

| **Header**               | **Value**    |
|--------------------------|-------------|
| **🕒 Trend {Timeframe}**  | "BULLISH" or "BEARISH" based on the EMA crossovers. |

---

### **3. Signals**

#### **Buy Conditions**
A **BUY** signal is generated when:
1. The Stochastic Oscillator shows a **bullish crossover** (%K crosses above %D in the oversold zone).
2. The RSI is in the **oversold zone**.

#### **Sell Conditions**
A **SELL** signal is generated when:
1. The Stochastic Oscillator shows a **bearish crossover** (%K crosses below %D in the overbought zone).
2. The RSI is in the **overbought zone**.

#### **Close Conditions**
- **CLOSE BUY**: Generated in a bearish trend when a sell condition is met.
- **CLOSE SELL**: Generated in a bullish trend when a buy condition is met.

---

### **Visualization**

#### **1. EMA Plot**
- **Blue Line**: Short EMA.
- **Orange Line**: Long EMA.

#### **2. Background Colors**
- **Green**: Indicates a bullish condition based on EMA crossovers.
- **Red**: Indicates a bearish condition based on EMA crossovers.
- **Blue**: Indicates the RSI is oversold.
- **Orange**: Indicates the RSI is overbought.

#### **3. Buy/Sell Shapes**
- **Green Label (BUY)**: Indicates a buy signal.
- **Red Label (SELL)**: Indicates a sell signal.
- **Orange Label (CLOSE BUY)**: Indicates a close buy signal.
- **Blue Label (CLOSE SELL)**: Indicates a close sell signal.

#### **4. Trend Table**
The trend table dynamically displays the **main trend** ("BULLISH" or "BEARISH") based on EMA crossovers for the selected timeframe.

---

### **Logic Summary**

| **Logic Component**       | **Condition**                                                                          |
|---------------------------|---------------------------------------------------------------------------------------|
| Main Trend                | Determined by EMA crossovers (Bullish or Bearish).                                     |
| RSI Overbought            | RSI > Overbought Level.                                                               |
| RSI Oversold              | RSI < Oversold Level.                                                                 |
| Stochastic Bullish Cross  | %K crosses above %D in oversold zone.                                                 |
| Stochastic Bearish Cross  | %K crosses below %D in overbought zone.                                               |
| Buy Signal                | RSI is oversold **and** Stochastic Bullish Cross **and** Main Trend is Bullish.        |
| Sell Signal               | RSI is overbought **and** Stochastic Bearish Cross **and** Main Trend is Bearish.      |
| Close Buy Signal          | Opposite condition in a Bearish trend.                                                |
| Close Sell Signal         | Opposite condition in a Bullish trend.                                                |

---

## **Functions Used**

| **Function**       | **Purpose**                                                 |
|--------------------|-----------------------------------------------------------|
| `ta.ema()`         | Calculates the Exponential Moving Averages (EMAs).         |
| `ta.rsi()`         | Calculates the Relative Strength Index (RSI).              |
| `ta.stoch()`       | Calculates the Stochastic Oscillator (%K and %D).          |
| `plotshape()`      | Displays the buy/sell signals on the chart.                |
| `table.new()`      | Creates a table to display the main trend.                 |
| `table.cell()`     | Updates the trend table dynamically.                       |

---

### **Recommended Usage**
0. **Timeframe Selection**: Choose the timeframe for trend analysis based on your trading strategy. By default, the script uses a 1-hour trend timeframe, to use 5m to open trades more frequently.
1. Configure the indicator based on your trading strategy (adjust EMA, RSI, and Stochastic settings).
2. Use the trend table to identify the dominant trend.
3. Monitor the **buy/sell signals** for potential entry and exit points.

This indicator is a versatile tool that combines EMAs, RSI, and Stochastic Oscillator for a multi-dimensional analysis of market trends and reversal points.

