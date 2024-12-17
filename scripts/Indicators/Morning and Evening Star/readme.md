# **Morning Star & Evening Star Detector Documentation**

## **Overview**
The **Morning Star & Evening Star Detector** is a **Pine Script™ v6** indicator designed to identify and visualize the **Morning Star** and **Evening Star** candlestick patterns, which are key reversal signals in trading. This script highlights these patterns visually on the chart and features a **counting table** in the bottom-right corner that tracks the total number of detected patterns.

This indicator is ideal for traders aiming to identify potential trend reversal points in both **bullish** and **bearish** market conditions.

---

## **How It Works**

### **1. Inputs**
The script allows users to customize the appearance of the indicator, including the colors of the icons and the background for the detected patterns.

| **Parameter**             | **Default** | **Description**                                               |
|--------------------------|-------------|-------------------------------------------------------------|
| Morning Star Icon Color   | Green       | Color of the icon displayed for the Morning Star pattern.     |
| Evening Star Icon Color   | Red         | Color of the icon displayed for the Evening Star pattern.     |
| Morning Star Background   | Green       | Background color for the 3 candles that form the Morning Star.|
| Evening Star Background   | Red         | Background color for the 3 candles that form the Evening Star.|
| Background Transparency   | 85          | Transparency level of the background fill (0 = opaque, 100 = fully transparent).|

---

### **2. Pattern Logic**
The script identifies two specific candlestick reversal patterns: **Morning Star** (bullish reversal) and **Evening Star** (bearish reversal).

#### **Morning Star**
A **Morning Star** is a bullish reversal pattern that occurs after a downtrend. It consists of **3 candles**:

1. **First Candle**: A large bearish candle.  
2. **Second Candle**: A small indecisive candle (can be a doji).  
3. **Third Candle**: A large bullish candle that closes above the midpoint of the first candle.  

**Logic**:
- The first candle must have a large bearish body.  
- The second candle must be small relative to the total range (indecision).  
- The third candle must have a large bullish body.  

#### **Evening Star**
An **Evening Star** is a bearish reversal pattern that occurs after an uptrend. It also consists of **3 candles**:

1. **First Candle**: A large bullish candle.  
2. **Second Candle**: A small indecisive candle (can be a doji).  
3. **Third Candle**: A large bearish candle that closes below the midpoint of the first candle.  

**Logic**:
- The first candle must have a large bullish body.  
- The second candle must be small relative to the total range (indecision).  
- The third candle must have a large bearish body.  

---

### **3. Visual Indicators**
To provide clear visual feedback, the script uses **icons** and **background colors** to highlight the patterns on the chart.

#### **Icons**
- **Morning Star**: ☀️ Icon displayed **below** the bar of the 3rd bullish candle.  
- **Evening Star**: 🌙 Icon displayed **above** the bar of the 3rd bearish candle.  

#### **Background Colors**
- **Morning Star**: The background of the 3 candles forming the pattern is filled with a **customizable green color**.  
- **Evening Star**: The background of the 3 candles forming the pattern is filled with a **customizable red color**.  

---

### **4. Counting Table**
The script features a **dynamic table** displayed in the **bottom-right corner** of the chart. This table tracks and displays the **total number of Morning Star and Evening Star patterns** detected in real time.

**Table Layout**:
| **Pattern**    | **Count** |
|----------------|-----------|
| Morning Star   | Total Morning Stars detected. |
| Evening Star   | Total Evening Stars detected. |

The table updates dynamically as new patterns are identified in the chart.

---

## **Key Features**
1. **Clear Visual Identification**  
   The use of **icons** and **background coloring** allows for quick identification of the Morning Star and Evening Star patterns directly on the chart.

2. **Dynamic Counting Table**  
   A **real-time counting table** is displayed in the bottom-right corner, tracking the frequency and distribution of the detected patterns.

3. **Customization**  
   Users can customize the **icon colors**, **background colors**, and **transparency** for better visibility and alignment with the chart’s style.

4. **Accurate Pattern Logic**  
   The script employs **strict pattern logic** to accurately identify valid Morning Star and Evening Star patterns, ensuring precision in reversal detection.

---

## **Visualization**
| **Visualization**          | **Color**          | **Placement**                                |
|---------------------------|-------------------|---------------------------------------------|
| **Morning Star Icon**      | Green             | Below the bar (☀️).                        |
| **Evening Star Icon**      | Red               | Above the bar (🌙).                        |
| **Morning Star Background**| Light Green       | 3 candles forming the Morning Star.         |
| **Evening Star Background**| Light Red         | 3 candles forming the Evening Star.         |
| **Counting Table**         | Gray Background   | Bottom-right corner.                        |

---

## **Usage Tips**
- **Identify Reversals Early**: Use this indicator to detect potential trend reversals after strong bearish or bullish moves.  
- **Combine with Other Indicators**: Combine this script with indicators like **Moving Averages (MA)**, **Relative Strength Index (RSI)**, or **Support/Resistance** levels for enhanced accuracy.  
- **Customize for Your Chart**: Customize **colors** and **transparency** to ensure clear visibility of the patterns.  
- **Monitor Counts**: Use the **counting table** to track how frequently the patterns are detected during your analysis session.  

---

## **Functions Used**
| **Function**    | **Purpose**                                         |
|-----------------|---------------------------------------------------|
| `bgcolor()`     | Fills the background of the detected candles with a specified color. |
| `plotshape()`   | Displays ☀️ and 🌙 icons on the chart.                 |
| `table.new()`   | Creates a table for counting detected patterns.     |
| `table.cell()`  | Updates table cells with the pattern name and count.|
| `math.abs()`    | Calculates the absolute value (used to determine body size).|

---

## **Summary**
The **Morning Star & Evening Star Detector** is a powerful Pine Script™ v6 indicator for identifying two of the most important candlestick reversal patterns. By providing clear visuals, a **dynamic counting table**, and **user-friendly customization**, this indicator is an essential tool for traders seeking to detect and act on market reversal points. It enhances technical analysis, allowing for better decision-making in both bullish and bearish market conditions.
