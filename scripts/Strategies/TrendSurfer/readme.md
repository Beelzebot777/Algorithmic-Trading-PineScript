# **Trend Surfer Strategy Documentation**

## **Overview**
The **Trend Surfer Strategy** is a fully configurable Pine Script strategy designed to automate trading decisions based on EMA, RSI, and Stochastic indicators. This script features customizable Stop Loss and Take Profit levels, enabling dynamic risk management while incorporating time-based filters for precise entry and exit points.

---

## **Script Code**

```pinescript
//@version=6
// [Include the complete script code here for reference]
```

---

## **How It Works**

### **1. Input Parameters**
#### **General Settings**:
| Parameter            | Default Value | Description                                           |
|----------------------|---------------|-------------------------------------------------------|
| `selectedTimeframe`  | `60`          | Timeframe for EMA trend calculation (e.g., 60 min).  |

#### **EMA Settings**:
| Parameter            | Default Value | Description                                           |
|----------------------|---------------|-------------------------------------------------------|
| `emaShortPeriod`     | `10`          | Short EMA period for trend detection.                |
| `emaLongPeriod`      | `55`          | Long EMA period for trend detection.                 |

#### **RSI Settings**:
| Parameter            | Default Value | Description                                           |
|----------------------|---------------|-------------------------------------------------------|
| `rsiPeriod`          | `14`          | RSI period for oversold/overbought detection.        |
| `oversoldLevel`      | `33`          | RSI level below which the market is oversold.        |
| `overboughtLevel`    | `67`          | RSI level above which the market is overbought.      |

#### **Stochastic Settings**:
| Parameter            | Default Value | Description                                           |
|----------------------|---------------|-------------------------------------------------------|
| `stochKPeriod`       | `14`          | %K period for stochastic oscillator.                 |
| `stochDPeriod`       | `3`           | %D smoothing period for stochastic oscillator.       |
| `stochSmooth`        | `3`           | Smoothing factor for stochastic oscillator.          |
| `stochOversold`      | `20`          | Stochastic level indicating oversold conditions.     |
| `stochOverbought`    | `80`          | Stochastic level indicating overbought conditions.   |

#### **Risk Management Settings**:
| Parameter            | Default Value | Description                                           |
|----------------------|---------------|-------------------------------------------------------|
| `stopLossPerc`       | `1.0`         | Stop Loss as a percentage of entry price.            |
| `takeProfitPerc`     | `2.0`         | Take Profit as a percentage of entry price.          |

---

### **2. Trading Conditions**
The script uses a combination of EMA, RSI, and Stochastic indicators to generate buy and sell signals:

- **Buy Conditions**:
  - RSI is oversold.
  - Stochastic bullish crossover occurs.
  - Current price is above the long EMA.
  - Time is within the specified range.

- **Sell Conditions**:
  - RSI is overbought.
  - Stochastic bearish crossover occurs.
  - Current price is below the long EMA.
  - Time is within the specified range.

---

### **3. Risk Management**
- **Stop Loss**: Automatically triggers an exit when the price moves against the position by a percentage (`stopLossPerc`).
- **Take Profit**: Automatically locks in profits when the price moves favorably by a percentage (`takeProfitPerc`).

---

### **4. Visualization**
The strategy plots key information directly on the chart:

- **EMA Lines**:
  - Short EMA: Blue line.
  - Long EMA: Orange line.

- **Pivot Table**:
  Displays trend state and key indicator levels (e.g., RSI and Stochastic).

- **Background Highlights**:
  - Green: Bullish condition.
  - Red: Bearish condition.

- **Entry/Exit Labels**:
  Buy and sell signals are displayed with labels and arrows.

---

## **Features**

### **Dynamic Indicator Integration**
- Combines EMA, RSI, and Stochastic indicators for robust signal generation.

### **Configurable Parameters**
- Fully customizable settings for fine-tuning the strategy.

### **Risk Management**
- Built-in Stop Loss and Take Profit mechanisms.

### **Time-Based Filters**
- Ensures trades occur only within a specified time range.

---

## **Functions Used**
| **Function**         | **Purpose**                                         |
|----------------------|---------------------------------------------------|
| `ta.rsi`             | Calculates the RSI value.                         |
| `ta.pivothigh`       | Detects pivot highs.                              |
| `ta.pivotlow`        | Detects pivot lows.                               |
| `request.security`   | Fetches data from a different timeframe.          |
| `strategy.entry`     | Places a new trade order.                         |
| `strategy.exit`      | Sets Stop Loss and Take Profit conditions.        |
| `plot`               | Draws EMA lines on the chart.                     |
| `bgcolor`            | Highlights background colors based on conditions. |
| `table.new`          | Creates a table for displaying trend information. |

---

## **Customization**

### **Indicator Settings**
- Adjust EMA, RSI, and Stochastic parameters to match your trading style.

### **Risk Management**
- Modify Stop Loss (`stopLossPerc`) and Take Profit (`takeProfitPerc`) percentages.

### **Visualization**
- Customize line colors, label styles, and table formats.

---

## **Summary**
The **Trend Surfer Strategy** provides a comprehensive solution for automated trading by leveraging advanced technical indicators and robust risk management. Its dynamic and customizable features make it a powerful tool for traders seeking efficient and informed decision-making.

