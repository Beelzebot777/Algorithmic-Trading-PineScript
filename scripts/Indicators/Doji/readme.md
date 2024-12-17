# **Advanced Doji Detector Script Documentation**

## **Overview**
The **Advanced Doji Detector** is a Pine Script indicator designed to detect and visualize five different types of Doji candles on a TradingView chart. The five Doji types it identifies are:  
- **Standard Doji**  
- **Gravestone Doji**  
- **Dragonfly Doji**  
- **Long-Legged Doji**  
- **Four-Price Doji**  

The indicator also provides a floating table on the chart that keeps track of how many of each type of Doji has appeared during the current chart session. 

---

## **Script Code**

```pinescript
//@version=6
indicator("Advanced Doji Detector (All Types)", overlay=true)

// === 🛠️ Customizable Inputs ===
doji_threshold = input.float(defval=0.1, title="Doji Threshold", minval=0.001)
shadow_similarity_threshold = input.float(defval=0.8, title="Minimum proportion between shadows (0 to 1)", minval=0.1, maxval=1.0)
shadow_ratio = input.float(defval=0.3, title="Minimum proportion for long shadows (30% of the candle)", minval=0.1, maxval=1.0)

// === 📏 Calculation of candle parameters ===
body_size = math.abs(open - close)
upper_shadow = high - math.max(open, close)
lower_shadow = math.min(open, close) - low
total_range = high - low

// === 🕯️ Logic for the different types of Doji ===

// 0️⃣ Four-Price Doji
is_four_price_doji = (open == close) and (open == high) and (open == low)

// 1️⃣ Standard Doji
small_body = body_size < doji_threshold * total_range
proporcion_sombras = lower_shadow > 0 and upper_shadow > 0 ? math.min(upper_shadow, lower_shadow) / math.max(upper_shadow, lower_shadow) : 0
sombras_similares = proporcion_sombras > shadow_similarity_threshold
is_standard_doji = small_body and sombras_similares and not is_four_price_doji

// 2️⃣ Gravestone Doji
no_lower_shadow = lower_shadow < 0.05 * total_range
long_upper_shadow = upper_shadow > shadow_ratio * total_range
is_gravestone_doji = small_body and no_lower_shadow and long_upper_shadow and not is_four_price_doji

// 3️⃣ Dragonfly Doji
no_upper_shadow = upper_shadow < 0.05 * total_range
long_lower_shadow = lower_shadow > shadow_ratio * total_range
is_dragonfly_doji = small_body and no_upper_shadow and long_lower_shadow and not is_four_price_doji

// 4️⃣ Long-Legged Doji
long_upper_shadow_legged = upper_shadow > shadow_ratio * total_range
long_lower_shadow_legged = lower_shadow > shadow_ratio * total_range
is_long_legged_doji = small_body and long_upper_shadow_legged and long_lower_shadow_legged and not is_standard_doji and not is_four_price_doji

// === 📈 Visualization of each type of Doji ===
plotshape(is_standard_doji, style=shape.cross, color=color.red, location=location.abovebar, size=size.small, title="Standard Doji")
plotshape(is_gravestone_doji, style=shape.triangleup, color=color.orange, location=location.abovebar, size=size.small, title="Gravestone Doji")
plotshape(is_dragonfly_doji, style=shape.triangledown, color=color.blue, location=location.belowbar, size=size.small, title="Dragonfly Doji")
plotshape(is_long_legged_doji, style=shape.circle, color=color.green, location=location.abovebar, size=size.small, title="Long-Legged Doji")
plotshape(is_four_price_doji, style=shape.square, color=color.purple, location=location.abovebar, size=size.small, title="Four-Price Doji")

// === 📋 Doji Counters ===
var int count_standard_doji = 0
var int count_gravestone_doji = 0
var int count_dragonfly_doji = 0
var int count_long_legged_doji = 0
var int count_four_price_doji = 0

// Increment counters if a Doji is detected
if is_standard_doji
    count_standard_doji += 1

if is_gravestone_doji
    count_gravestone_doji += 1

if is_dragonfly_doji
    count_dragonfly_doji += 1

if is_long_legged_doji
    count_long_legged_doji += 1

if is_four_price_doji
    count_four_price_doji += 1

// === 📋 Counting Table ===
var table doji_table = table.new(position.bottom_right, 7, 5)

// Table headers
if (bar_index == 0)
    table.cell(doji_table, 0, 0, "Doji Type", text_color=color.white, bgcolor=color.blue)
    table.cell(doji_table, 0, 1, "Count", text_color=color.white, bgcolor=color.blue)

// Doji type names
table.cell(doji_table, 1, 0, "Standard Doji", text_color=color.red)
table.cell(doji_table, 2, 0, "Gravestone Doji", text_color=color.orange)
table.cell(doji_table, 3, 0, "Dragonfly Doji", text_color=color.blue)
table.cell(doji_table, 4, 0, "Long-Legged Doji", text_color=color.green)
table.cell(doji_table, 5, 0, "Four-Price Doji", text_color=color.purple)

// Count of each type of Doji
table.cell(doji_table, 1, 1, str.tostring(count_standard_doji), text_color=color.white)
table.cell(doji_table, 2, 1, str.tostring(count_gravestone_doji), text_color=color.white)
table.cell(doji_table, 3, 1, str.tostring(count_dragonfly_doji), text_color=color.white)
table.cell(doji_table, 4, 1, str.tostring(count_long_legged_doji), text_color=color.white)
table.cell(doji_table, 5, 1, str.tostring(count_four_price_doji), text_color=color.white)

table.cell(doji_table, 0, 2, "")
table.cell(doji_table, 0, 3, "")
table.cell(doji_table, 0, 4, "")
table.cell(doji_table, 6, 0, "")
```

# **How It Works**

## **1. Candle Parameters**
- **Body Size**: The difference between the open and close prices.  
- **Upper Shadow**: The difference between the high price and the maximum of the open or close prices.  
- **Lower Shadow**: The difference between the minimum of the open or close prices and the low price.  
- **Total Range**: The difference between the high and low prices.  

---

## **2. Doji Types and Logic**
- **Standard Doji**: The body size is small, and the upper and lower shadows are similar in size.  
- **Gravestone Doji**: The lower shadow is very small, the body is small, and the upper shadow is long.  
- **Dragonfly Doji**: The upper shadow is very small, the body is small, and the lower shadow is long.  
- **Long-Legged Doji**: Both the upper and lower shadows are long relative to the total range.  
- **Four-Price Doji**: The open, close, high, and low prices are all the same.  

---

# **Key Features**
- **Live Visualization**: Detects and marks each type of Doji with a distinct shape and color.  
- **Doji Counter**: Displays a table of how many times each type of Doji has appeared.  
- **Customizable Inputs**: Control the Doji sensitivity for shadows and body sizes.  

---

# **Customization**
## **1. Input Customization**
- Adjust inputs to fine-tune the Doji detection logic.  

## **2. Visual Customization**
- Customize the colors, shapes, and sizes of Doji marks.  
