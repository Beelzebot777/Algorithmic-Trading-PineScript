# **Crypto Harami Pattern Detector Documentation**

## **Overview**
The **Harami Pattern Detector** is a **Pine Script™ v6** indicator designed to identify and visualize the **Bullish Harami** and **Bearish Harami** candlestick patterns, which are key reversal signals in trading. This script highlights these patterns visually on the chart and features a **counting table** in the bottom-right corner that tracks the total number of detected patterns.

This indicator is ideal for traders aiming to identify potential trend reversal points in both **bullish** and **bearish** market conditions.

---

## **How It Works**

### **1. Inputs**
This script does not require any input customization since it works with a fixed logic to detect **Bullish Harami** and **Bearish Harami** patterns. However, users can visually customize the color scheme directly within the script if needed.

| **Parameter**             | **Default** | **Description**                                               |
|--------------------------|-------------|-------------------------------------------------------------|
| Bullish Harami Icon Color | Green       | Color of the icon displayed for the Bullish Harami pattern.   |
| Bearish Harami Icon Color | Red         | Color of the icon displayed for the Bearish Harami pattern.   |
| Counting Table Background | Gray        | Background color of the counting table in the bottom-right.  |
| Table Frame Color         | Gray        | Frame color for the counting table.                         |

---

### **2. Pattern Logic**
The script identifies two specific candlestick reversal patterns: **Bullish Harami** (bullish reversal) and **Bearish Harami** (bearish reversal).

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

---

### **3. Visual Indicators**
The script provides **visual icons** to identify each of the 3 candles that form the **Bullish Harami** and **Bearish Harami** patterns.

#### **Icons**
- **Bullish Harami**: 🟢 Triangle Up icons are displayed **below** the bar for all 3 candles in the pattern.  
- **Bearish Harami**: 🔴 Triangle Down icons are displayed **above** the bar for all 3 candles in the pattern.  

| **Visualization**          | **Color**    | **Placement**       |
|----------------------------|--------------|---------------------|
| **Bullish Harami Icons**    | Green        | Below the bar       |
| **Bearish Harami Icons**    | Red          | Above the bar       |

---

### **4. Counting Table**
The script features a **dynamic table** displayed in the **bottom-right corner** of the chart. This table tracks and displays the **total number of Bullish Harami and Bearish Harami patterns** detected in real time.

**Table Layout**:
| **Pattern**         | **Count**  |
|---------------------|------------|
| Bullish Harami      | Total Bullish Harami patterns detected. |
| Bearish Harami      | Total Bearish Harami patterns detected. |

The table updates dynamically as new patterns are identified in the chart.

---

## **Key Features**
1. **Clear Visual Identification**  
   The use of **icons** allows for quick identification of the Bullish Harami and Bearish Harami patterns directly on the chart.

2. **Dynamic Counting Table**  
   A **real-time counting table** is displayed in the bottom-right corner, tracking the frequency and distribution of the detected patterns.

3. **Accurate Pattern Logic**  
   The script employs **strict pattern logic** to accurately identify valid Bullish Harami and Bearish Harami patterns, ensuring precision in reversal detection.

---

## **Functions Used**
| **Function**       | **Purpose**                                                 |
|--------------------|-----------------------------------------------------------|
| `plotshape()`      | Displays the up/down triangles for the pattern candles.    |
| `table.new()`      | Creates a table for counting detected patterns.           |
| `table.cell()`     | Updates table cells with the pattern name and count.      |

---

## **Usage Tips**
- **Identify Reversals Early**: Use this indicator to detect potential trend reversals after strong bearish or bullish moves.  
- **Combine with Other Indicators**: Combine this script with indicators like **Moving Averages (MA)**, **Relative Strength Index (RSI)**, or **Support/Resistance** levels for enhanced accuracy.  
- **Track Counts**: Use the **counting table** to track how frequently the patterns are detected during your analysis session.  

---

## **Summary**
The **Crypto Harami Pattern Detector** is a powerful **Pine Script™ v6** indicator for identifying two of the most important candlestick reversal patterns. By providing clear visuals and a **dynamic counting table**, this indicator is an essential tool for traders seeking to detect and act on market reversal points. It enhances technical analysis, allowing for better decision-making in both bullish and bearish market conditions.
