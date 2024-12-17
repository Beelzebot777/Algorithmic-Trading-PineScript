# **Hammer & Inverted Hammer Detector (with ATR and Table) Documentation**

## **Overview**
The **Hammer & Inverted Hammer Detector** is a Pine Script indicator that identifies and visualizes **Hammer** and **Inverted Hammer** candlestick patterns. It also integrates the **ATR (Average True Range)** to determine the relevance of candles and displays a **counting table** at the bottom-right of the chart, which tracks the number of Hammers and Inverted Hammers detected.

This indicator is ideal for traders seeking to identify key reversal points in the market.

---

## **Script Code**
```pinescript
//@version=6
indicator("Hammer & Inverted Hammer Detector (with ATR and Table)", overlay=true)

// 🛠️ Customizable Parameters
body_ratio = input.float(defval=0.2, title="Body proportion (0.1 to 1)", minval=0.1, maxval=1)
lower_wick_ratio = input.float(defval=0.5, title="Lower wick proportion (0.1 to 1)", minval=0.1, maxval=1)
upper_wick_ratio = input.float(defval=0.5, title="Upper wick proportion (0.1 to 1)", minval=0.1, maxval=1)
small_wick_ratio = input.float(defval=0.2, title="Maximum opposite wick proportion (0.1 to 1)", minval=0.1, maxval=1)
atr_period = input.int(defval=14, title="ATR period", minval=1, maxval=100)
atr_multiplier = input.float(defval=1.5, title="ATR multiplier for relevance", minval=0.1, maxval=10)

// 📊 Price variables
openPrice = open
closePrice = close
highPrice = high
lowPrice = low

// 📐 Calculation of candle sizes
bodySize = math.abs(closePrice - openPrice)          // Size of the candle body
totalRange = highPrice - lowPrice                    // Total range of the candle
upperWick = highPrice - math.max(openPrice, closePrice) // Upper wick size
lowerWick = math.min(openPrice, closePrice) - lowPrice  // Lower wick size

// 🔥 Calculate ATR to determine the average volatility
atrValue = ta.atr(atr_period) // ATR calculated with the user-defined period
atrAverage = ta.sma(atrValue, atr_period) // Simple moving average of the ATR

// ⚡️ Normalize the ATR to the price scale
normalizedATR = atrValue + low 
normalizedATRAverage = atrAverage + low 

// ⚡️ Determine if the candle is relevant
isRelevant = totalRange > (atrValue * atr_multiplier)  // The candle must have a size larger than the ATR * multiplier

// 📘 Condition for Hammer
isHammer = (bodySize > (totalRange * body_ratio)) and           
           (lowerWick > (totalRange * lower_wick_ratio)) and    
           (upperWick < (totalRange * small_wick_ratio)) and    
           isRelevant 

// 📘 Condition for Inverted Hammer
isInvertedHammer = (bodySize > (totalRange * body_ratio)) and   
                   (upperWick > (totalRange * upper_wick_ratio)) and 
                   (lowerWick < (totalRange * small_wick_ratio)) and 
                   isRelevant 

// 🔍 Display icons on the chart
plotshape(isHammer, title="Hammer", location=location.belowbar, color=color.green, style=shape.labelup, text="🔨")
plotshape(isInvertedHammer, title="Inverted Hammer", location=location.abovebar, color=color.red, style=shape.labeldown, text="🔼")

// 📈 Plot ATR and ATR average on the main chart
plot(normalizedATR, title="ATR", color=color.blue, linewidth=2)
plot(normalizedATRAverage, title="ATR Average", color=color.orange, linewidth=2)
fill(plot(normalizedATR), plot(normalizedATRAverage), color=color.new(color.blue, 80)) 

// 📋 🧮 Count of Hammers and Inverted Hammers
var int hammerCount = 0 // Counter for Hammers
var int invertedHammerCount = 0 // Counter for Inverted Hammers

// Increment the counters if a Hammer or Inverted Hammer is detected
if isHammer
    hammerCount += 1
if isInvertedHammer
    invertedHammerCount += 1

// === 📋 Counting table in the bottom-right corner ===
var table hammerTable = table.new(position.bottom_right, 3, 2, bgcolor=color.new(color.gray, 90), frame_color=color.gray, frame_width=1)

// 📋 Table headers
table.cell(hammerTable, 0, 0, "🟢 Type", text_color=color.white, bgcolor=color.blue)
table.cell(hammerTable, 0, 1, "📈 Count", text_color=color.white, bgcolor=color.blue)

// 📋 Names of the patterns
table.cell(hammerTable, 1, 0, "Hammer", text_color=color.green)
table.cell(hammerTable, 2, 0, "Inverted Hammer", text_color=color.red)

// 📋 Count of each pattern
table.cell(hammerTable, 1, 1, str.tostring(hammerCount), text_color=color.white)
table.cell(hammerTable, 2, 1, str.tostring(invertedHammerCount), text_color=color.white)

```

---

## **How It Works**

### **1. Inputs**
The user can customize several key parameters to define the strictness of the detection logic. These inputs allow flexibility to fine-tune the detection of **Hammer** and **Inverted Hammer** candlestick patterns.

| **Parameter**         | **Default** | **Description**                                               |
|----------------------|-------------|---------------------------------------------------------------|
| **Body Proportion**    | 0.2         | The minimum proportion of the candle body relative to the total range. |
| **Lower Wick Proportion** | 0.5     | The minimum proportion of the lower wick relative to the total range. |
| **Upper Wick Proportion** | 0.5     | The minimum proportion of the upper wick relative to the total range. |
| **Maximum Opposite Wick** | 0.2    | Maximum allowable proportion of the opposite wick relative to the total range. |
| **ATR Period**         | 14          | Period for calculating the Average True Range (ATR).            |
| **ATR Multiplier**      | 1.5        | Multiplier to define how large the candle must be compared to the ATR. |

---

### **2. Candle Size Calculation**
To classify a candle as a **Hammer** or **Inverted Hammer**, the following candle components are calculated:
- **Body Size**: `abs(close - open)`  
- **Total Range**: `high - low`  
- **Upper Wick**: `high - max(open, close)`  
- **Lower Wick**: `min(open, close) - low`  

These components are crucial for identifying Hammer and Inverted Hammer patterns.

---

### **3. ATR Calculation**
The **ATR (Average True Range)** is used to filter candles based on their significance.  
- **ATR Value**: Calculated using `ta.atr(atr_period)`.  
- **ATR Average**: Calculated as the simple moving average of the ATR, `ta.sma(atrValue, atr_period)`.  
- The script ensures that the total range of a candle is at least `atrValue * atr_multiplier` for it to be considered a **relevant candle**.  

---

### **4. Pattern Detection**
The following logic is applied to identify the **Hammer** and **Inverted Hammer** patterns.

#### **Hammer Conditions**
A candle is considered a **Hammer** if it satisfies the following conditions:
1. The **body** is large relative to the total range (`bodySize > totalRange * body_ratio`).
2. The **lower wick** is large (`lowerWick > totalRange * lower_wick_ratio`).
3. The **upper wick** is small (`upperWick < totalRange * small_wick_ratio`).
4. The candle is **relevant** according to the ATR filter (`totalRange > atrValue * atr_multiplier`).

#### **Inverted Hammer Conditions**
A candle is considered an **Inverted Hammer** if it satisfies the following conditions:
1. The **body** is large relative to the total range (`bodySize > totalRange * body_ratio`).
2. The **upper wick** is large (`upperWick > totalRange * upper_wick_ratio`).
3. The **lower wick** is small (`lowerWick < totalRange * small_wick_ratio`).
4. The candle is **relevant** according to the ATR filter (`totalRange > atrValue * atr_multiplier`).

---

### **5. Counting and Table Display**
The script tracks the total number of **Hammers** and **Inverted Hammers** detected on the chart. This information is displayed in a **counting table** at the bottom-right of the screen.

**Table Layout**:
| **Pattern**           | **Count**        |
|----------------------|------------------|
| **Hammer**            | Total detected Hammers |
| **Inverted Hammer**   | Total detected Inverted Hammers |

The table has two rows, each displaying the name of the pattern and its corresponding count. The table updates dynamically as new patterns are detected.

---

### **6. Visualization**
**Icons** are plotted on the chart to visualize the detected Hammer and Inverted Hammer patterns.  
- **Hammers**: Displayed with a **🔨 icon below the bar**.  
- **Inverted Hammers**: Displayed with a **🔼 icon above the bar**.  

---

## **Key Features**

### **1. Customizable Pattern Detection**
The user can customize key parameters like the body size, wick sizes, and ATR relevance. This allows fine-tuning of pattern detection.

### **2. ATR Relevance Filter**
The script filters out small candles by ensuring that only candles larger than a multiple of the **ATR** are considered **relevant**.

### **3. Counting Table**
A dynamic table is displayed at the bottom-right of the chart to keep track of the number of **Hammers** and **Inverted Hammers** detected in the current session.

### **4. Intuitive Visuals**
- **🔨 Hammer**: Icon displayed **below the bar**.  
- **🔼 Inverted Hammer**: Icon displayed **above the bar**.  
- **Count Table**: Displays the number of Hammers and Inverted Hammers detected.  

---

## **Functions Used**

| **Function**       | **Purpose**                                                     |
|--------------------|-----------------------------------------------------------------|
| `ta.atr()`         | Calculates the Average True Range (ATR) for the given period.    |
| `ta.sma()`         | Calculates the simple moving average of the ATR.                 |
| `math.abs()`       | Calculates the absolute value (used for body size).              |
| `table.new()`      | Creates the table used to count and display detected patterns.  |
| `table.cell()`     | Updates table cells with the pattern name and count.            |
| `plotshape()`      | Plots the **🔨 Hammer** and **🔼 Inverted Hammer** icons.       |
| `plot()`           | Draws the ATR and ATR average on the main chart.                |
| `fill()`           | Highlights the area between ATR and its average.                |

---

## **Customization**

You can customize the script in the following ways:

### **1. Modify Pattern Detection**
- Adjust **Body Proportion**, **Wick Sizes**, and **Opposite Wick** to detect patterns with stricter or looser criteria.

### **2. Control Relevance Using ATR**
- Change the **ATR Period** and **ATR Multiplier** to modify how large a candle must be relative to ATR for it to be considered.

### **3. Customize the Counting Table**
- You can customize the table layout, position (`position.bottom_right`), and design (background color, frame color, and text color).

### **4. Icon Display**
- Icons for **Hammers** and **Inverted Hammers** can be changed or removed.  
- Change the **text and color** for the Hammer (`🔨`, color green) and Inverted Hammer (`🔼`, color red).

---

## **Visual Output**

| **Visualization**      | **Color**        | **Placement**         |
|-----------------------|-----------------|-----------------------|
| **Hammer Icon**        | **Green**        | **Below the bar**     |
| **Inverted Hammer Icon** | **Red**         | **Above the bar**     |
| **ATR Line**           | **Blue**         | **Overlay on chart**  |
| **ATR Average Line**   | **Orange**       | **Overlay on chart**  |
| **Table**              | **Gray Background** | **Bottom-right corner** |

---

## **Usage Tips**

1. **Use the ATR Filter**  
   The ATR filter is essential for avoiding detection of small candles. Adjust the **ATR Multiplier** if you notice false positives.

2. **Fine-Tune Body and Wick Ratios**  
   The default settings work well, but you can increase **Body Ratio** and **Wick Ratios** to make detection stricter.

3. **Focus on Relevant Patterns**  
   Use the **Count Table** to track the total number of Hammers and Inverted Hammers during your session.

4. **Customize the Look**  
   Change the table, icon styles, and plot colors to match your chart's color scheme.

---

## **Summary**
This **Hammer & Inverted Hammer Detector** identifies and tracks Hammers and Inverted Hammers. It integrates **ATR relevance** and provides users with a visual and statistical summary of the patterns detected on the chart.
