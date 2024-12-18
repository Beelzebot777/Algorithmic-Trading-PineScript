# **Shooting Star Detector Documentation**

## **Overview**
The **Shooting Star Detector** is a Pine Script™ v6 indicator designed to identify and highlight the **Shooting Star candlestick pattern**. This pattern is a **bearish reversal signal** that occurs after an uptrend, signaling potential weakness and reversal in the market.

The script highlights valid Shooting Stars visually on the chart and includes a **dynamic counting table** in the bottom-right corner to track the number of patterns detected.

---

## **How It Works**

### **1. Inputs**
The indicator allows users to adjust the sensitivity of the trend detection.

| **Parameter**                     | **Default** | **Description**                                         |
|-----------------------------------|------------|-------------------------------------------------------|
| Number of candles for previous trend | 1          | Number of bullish candles to confirm the previous uptrend.|

---

### **2. Shooting Star Logic**

#### **Candle Characteristics**
1. **Small Body**:
   - The candle body must be less than **40% of the total range** (high to low).
   - **Formula**:  
     ```pinescript
     is_small_body = candle_body < (high - low) * 0.4
     ```

2. **Large Upper Shadow**:
   - The upper shadow must be **greater than or equal to the size of the candle body**.
   - **Formula**:  
     ```pinescript
     is_large_upper_shadow = upper_shadow > (candle_body * 1)
     ```

3. **Small Lower Shadow**:
   - The lower shadow must be **less than 20% of the candle body**.
   - **Formula**:  
     ```pinescript
     is_small_lower_shadow = lower_shadow < (candle_body * 0.2)
     ```

---

#### **Previous Uptrend**
To confirm the Shooting Star as a bearish reversal pattern:
- The script checks for a **previous uptrend** defined by the user-selected number of candles.
- Each of these candles must be **bullish** (close > open).
- The highs in the previous trend must also show **higher highs**.

**Logic**:
```pinescript
is_uptrend = true
for i = 1 to trendLength
    if close[i] <= open[i]
        is_uptrend := false
```

### **Confirmation of Reversal**
- The script confirms the reversal by checking the next candle.
- The next candle must close below the low of the Shooting Star.
**Formula:**
```pinescript
is_confirmation = close[1] < low
```

### **Valid Shooting Star**
To identify a valid Shooting Star, all the following conditions must be true:

- **Small body**
- **Large upper shadow**
- **Small lower shadow**
- **Previous uptrend detected**
- **Confirmation candle closes below the Shooting Star's low**
**Final Logic:**

```pinescript
is_valid_shooting_star = is_shooting_star and is_uptrend and is_confirmation
```

## **3. Visual Indicators**
The indicator highlights valid **Shooting Stars** on the chart using visual signals.

| **Feature**           | **Appearance**                          |
|----------------------|------------------------------------------|
| Shooting Star Signal  | A red label ("SS") above the bar         |

---

## **4. Counting Table**
The script dynamically tracks the total number of **Shooting Stars detected** and displays the count in a table located in the **bottom-right corner**.

### **Table Layout**
| **Pattern**            | **Count**                                      |
|-----------------------|------------------------------------------------|
| Shooting Star          | Total number of Shooting Stars detected.       |

---

## **Key Features**
- **Accurate Shooting Star Detection**  
  Combines small body, large upper shadow, and confirmation candle logic for precise identification.

- **Dynamic Trend Validation**  
  Allows users to customize the number of candles considered in the previous uptrend.

- **Real-Time Counting Table**  
  Tracks the number of Shooting Stars detected and displays the count for easy monitoring.

- **Visual Signals**  
  Highlights valid Shooting Stars directly on the chart for clear visibility.

---

## **Customization**
The following input is available for user adjustment:

| **Parameter**                     | **Description**                                         |
|-----------------------------------|-------------------------------------------------------|
| Number of candles for previous trend | Adjust the number of candles to validate the uptrend before the Shooting Star. |

---

## **Visualization**
| **Element**             | **Color**           | **Placement**                      |
|-----------------------|---------------------|-------------------------------------|
| Shooting Star Signal    | Red Label "SS"      | Above the valid Shooting Star       |
| Counting Table          | Gray Background     | Bottom-right corner of the chart    |

---

## **Usage Tips**
- **Confirm Reversals**: Use the **Shooting Star Detector** to identify potential bearish reversals after uptrends.
- **Combine with Other Indicators**: Improve accuracy by combining this indicator with tools like **Relative Strength Index (RSI)**, **Moving Averages (MA)**, or **Support/Resistance** levels.
- **Adjust Trend Sensitivity**: Use the **Number of candles for previous trend** input to fine-tune the uptrend detection for different timeframes or markets.
- **Monitor Count**: Use the **counting table** to track the frequency of Shooting Stars and identify patterns in market behavior.

---

## **Functions Used**
| **Function**         | **Purpose**                                           |
|---------------------|------------------------------------------------------|
| `math.abs()`         | Calculates the absolute value (used to determine the candle body size). |
| `plotshape()`        | Plots the "SS" label above valid Shooting Star bars.   |
| `table.new()`        | Creates a table to display the count of Shooting Stars.|
| `table.cell()`       | Updates table cells with the pattern name and the total count. |

---

## **Summary**
The **Shooting Star Detector** is a powerful Pine Script™ v6 indicator for identifying **Shooting Star candlestick patterns**, a key bearish reversal signal. With its combination of **precise pattern logic**, **uptrend validation**, and a **dynamic counting table**, this tool is essential for traders looking to detect and act on potential market reversals.

By providing clear **visual signals** and tracking the frequency of detected patterns, this indicator enhances technical analysis and supports better trading decisions.

---

## **Example Use Case**
1. **Apply the indicator** to charts with uptrends to identify potential reversal points.  
2. **Monitor the "SS" labels** to spot Shooting Stars.  
3. **Use the counting table** to track the number of valid signals.  


