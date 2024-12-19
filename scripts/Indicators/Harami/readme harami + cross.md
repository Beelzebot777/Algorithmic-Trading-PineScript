# **Crypto Harami Pattern Detector Documentation**

## **Overview**
The **Harami Pattern Detector** is a **Pine Script™ v6** indicator designed to identify and visualize the **Bullish Harami**, **Bearish Harami**, **Bullish Harami Cross**, and **Bearish Harami Cross** candlestick patterns, which are key reversal signals in trading. This script highlights these patterns visually on the chart and features a **counting table** in the bottom-right corner that tracks the total number of detected patterns.

This indicator is ideal for traders aiming to identify potential trend reversal points in both **bullish** and **bearish** market conditions.

---

## **How It Works**

### **1. Inputs**
This script does not require any input customization since it works with a fixed logic to detect **Bullish Harami**, **Bearish Harami**, **Bullish Harami Cross**, and **Bearish Harami Cross** patterns. However, users can visually customize the color scheme directly within the script if needed.

| **Parameter**             | **Default** | **Description**                                               |
|--------------------------|-------------|-------------------------------------------------------------|
| Bullish Harami Icon Color | Green       | Color of the icon displayed for the Bullish Harami pattern.   |
| Bullish Harami Cross Icon Color | Blue  | Color of the icon displayed for the Bullish Harami Cross pattern.|
| Bearish Harami Icon Color | Red         | Color of the icon displayed for the Bearish Harami pattern.   |
| Bearish Harami Cross Icon Color | Blue | Color of the icon displayed for the Bearish Harami Cross pattern.|
| Counting Table Background | Gray        | Background color of the counting table in the bottom-right.  |
| Table Frame Color         | Gray        | Frame color for the counting table.                         |

---

### **2. Pattern Logic**
The script identifies four specific candlestick reversal patterns: **Bullish Harami**, **Bearish Harami**, **Bullish Harami Cross**, and **Bearish Harami Cross**.

#### **Bullish Harami**
A **Bullish Harami** is a bullish reversal pattern that occurs after a downtrend. It consists of **3 candles**:

1. **First Candle**: A large bearish candle.  
2. **Second Candle**: A small bullish candle that is fully contained within the body of the first candle.  
3. **Third Candle**: A bullish confirmation candle that closes higher than its open.  

**Logic**:
- The first candle must be bearish: `open[2] > close[2]`
- The second candle must be bullish: `close[1] > open[1]`
- The second candle’s body must be fully contained within the body of the first candle: `open[2] > close[1]` and `high[1] < open[2]`
- The third candle must be bullish: `close > open`

#### **Bullish Harami Cross**
A **Bullish Harami Cross** is similar to a **Bullish Harami**, but the second candle is a **Doji** (open and close are almost equal). 

**Logic**:
- The same conditions as the **Bullish Harami**. 
- Additionally, the second candle must be a Doji: `math.abs(open[1] - close[1]) < (high[1] - low[1]) * 0.1`

#### **Bearish Harami**
A **Bearish Harami** is a bearish reversal pattern that occurs after an uptrend. It also consists of **3 candles**:

1. **First Candle**: A large bullish candle.  
2. **Second Candle**: A small bearish candle that is fully contained within the body of the first candle.  
3. **Third Candle**: A bearish confirmation candle that closes lower than its open.  

**Logic**:
- The first candle must be bullish: `open[2] < close[2]`
- The second candle must be bearish: `open[1] > close[1]`
- The second candle’s body must be fully contained within the body of the first candle: `open[2] < close[1]` and `high[1] > open[2]`
- The third candle must be bearish: `open > close`

#### **Bearish Harami Cross**
A **Bearish Harami Cross** is similar to a **Bearish Harami**, but the second candle is a **Doji** (open and close are almost equal). 

**Logic**:
- The same conditions as the **Bearish Harami**. 
- Additionally, the second candle must be a Doji: `math.abs(open[1] - close[1]) < (high[1] - low[1]) * 0.1`

---

### **3. Counting Table**
The script features a **dynamic table** displayed in the **bottom-right corner** of the chart. This table tracks and displays the **total number of Bullish Harami, Bearish Harami, Bullish Harami Cross, and Bearish Harami Cross** patterns detected in real time.

**Table Layout**:
| **Pattern**               | **Count**  |
|---------------------------|------------|
| Bullish Harami             | Total Bullish Harami patterns detected. |
| Bullish Harami Cross       | Total Bullish Harami Cross patterns detected. |
| Bearish Harami             | Total Bearish Harami patterns detected. |
| Bearish Harami Cross       | Total Bearish Harami Cross patterns detected. |

The table updates dynamically as new patterns are identified in the chart.

---

## **Functions Used**
| **Function**       | **Purpose**                                                 |
|--------------------|-----------------------------------------------------------|
| `plotshape()`      | Displays the up/down triangles for the pattern candles.    |
| `table.new()`      | Creates a table for counting detected patterns.           |
| `table.cell()`     | Updates table cells with the pattern name and count.      |

---

## **Summary**
The **Crypto Harami Pattern Detector** is a powerful **Pine Script™ v6** indicator for identifying four of the most important candlestick reversal patterns. By providing clear visuals and a **dynamic counting table**, this indicator is an essential tool for traders seeking to detect and act on market reversal points. It enhances technical analysis, allowing for better decision-making in both bullish and bearish market conditions.

