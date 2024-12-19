# **Marubozu Pattern Detector Documentation**

## **Overview**
The **Marubozu Pattern Detector** is a **Pine Script™ v6** indicator designed to identify and visualize the **Marubozu candlestick pattern**. This pattern is significant in technical analysis as it represents a strong directional movement in price, either bullish or bearish. The indicator highlights Marubozu candles directly on the chart, allowing traders to quickly identify key momentum shifts.

This script detects and highlights **Bullish Marubozu** and **Bearish Marubozu** candles, with customization options for wick tolerance, providing flexibility to identify strict or more lenient definitions of the pattern.

---

## **How It Works**

### **1. Inputs**
The user can customize the **tolerance of wicks** to determine how strict the Marubozu detection should be. The inputs are as follows:

- **Wick Tolerance (%)**: A float input (0% to 100%) that specifies how small the upper and lower wicks must be relative to the total candle size.
  
  **Default**: 5%
  
  **Explanation**: The lower the percentage, the stricter the pattern. For example, a 5% tolerance means the wicks (upper and lower) must be at most 5% of the total candle range.

---

### **2. Pattern Logic**
The script identifies two specific types of Marubozu patterns: **Bullish Marubozu** and **Bearish Marubozu**.

#### **Bullish Marubozu**
A **Bullish Marubozu** is a bullish continuation candle with the following conditions:
1. The closing price is higher than the opening price.
2. The upper wick (High - Close) is less than or equal to the defined wick tolerance.
3. The lower wick (Open - Low) is less than or equal to the defined wick tolerance.

**Logic**:
- **Bullish candle**: `open < close`
- **Upper wick**: `(High - max(Open, Close))` ≤ `percentage_tolerance`
- **Lower wick**: `(min(Open, Close) - Low)` ≤ `percentage_tolerance`

#### **Bearish Marubozu**
A **Bearish Marubozu** is a bearish continuation candle with the following conditions:
1. The closing price is lower than the opening price.
2. The upper wick (High - Open) is less than or equal to the defined wick tolerance.
3. The lower wick (Close - Low) is less than or equal to the defined wick tolerance.

**Logic**:
- **Bearish candle**: `open > close`
- **Upper wick**: `(High - max(Open, Close))` ≤ `percentage_tolerance`
- **Lower wick**: `(min(Open, Close) - Low)` ≤ `percentage_tolerance`

---

### **3. Visual Indicators**
The script highlights Marubozu patterns visually on the chart using **labels** and **icons**.

#### **Labels and Icons**
| **Pattern**          | **Label**  | **Position**     | **Color**     |
|---------------------|------------|-----------------|---------------|
| **Bullish Marubozu** | "M"        | Below the bar   | **Green**     |
| **Bearish Marubozu** | "M"        | Above the bar   | **Red**       |

#### **How it works**
- **Bullish Marubozu**: A green "M" is plotted below the bullish Marubozu candle.
- **Bearish Marubozu**: A red "M" is plotted above the bearish Marubozu candle.

---

## **Code Walkthrough**
Here is the core logic for the **Marubozu Pattern Detector** written in Pine Script v6.

```pinescript
//@version=6
indicator("Marubozu Detector", overlay=true)

// **Input del usuario**
percentage_no_wick = input.float(5, "Wick Tolerance (%)", minval=0, maxval=100)

// **Cálculo del rango de la vela**
totalCandle = math.abs(high - low)          // Tamaño total de la vela (de Low a High)
body = math.abs(open - close)              // Tamaño del cuerpo de la vela (diferencia entre Open y Close)

// **Cálculo de las mechas**
shadowA = high - math.max(open, close)     // Mecha superior (High - máximo de Open y Close)
shadowB = math.min(open, close) - low      // Mecha inferior (mínimo de Open y Close - Low)

// **Cálculo del tamaño relativo de las mechas**
shadowApercent = (shadowA * 100) / totalCandle  // Porcentaje de la mecha superior en relación a la vela total
shadowBpercent = (shadowB * 100) / totalCandle  // Porcentaje de la mecha inferior en relación a la vela total

// **Detección del Marubozu**
marubozuBullish = open < close and shadowApercent <= percentage_no_wick and shadowBpercent <= percentage_no_wick
marubozuBearish = open > close and shadowApercent <= percentage_no_wick and shadowBpercent <= percentage_no_wick

// **Visualización en el gráfico**
plotshape(series=marubozuBullish, location=location.belowbar, color=color.green, style=shape.labelup, text="M", textcolor=color.white, size=size.small)
plotshape(series=marubozuBearish, location=location.abovebar, color=color.red, style=shape.labeldown, text="M", textcolor=color.white, size=size.small)
```

---

## **Key Features**
1. **Accurate Pattern Detection**
   - Identifies both **Bullish Marubozu** and **Bearish Marubozu**.
   - Uses precise wick percentage tolerance logic to ensure strict pattern detection.

2. **Clear Visual Labels**
   - Marks Bullish Marubozu with a green "M" below the bar.
   - Marks Bearish Marubozu with a red "M" above the bar.

3. **Customizable Wick Tolerance**
   - Input allows for user customization of wick tolerance (default: 5%).

4. **User-Friendly Visuals**
   - Uses clear and simple labels directly on the chart.

---

## **Usage Tips**
- **Strict or Loose Marubozu**: Adjust the wick tolerance for more or less strict Marubozu detection.
- **Combine with Indicators**: Use it alongside other indicators like **RSI** or **Moving Averages** to confirm trade entries.
- **Spot Reversals**: Marubozu candles often signal strong trend continuation or reversals, especially on higher timeframes.

---

## **Functions Used**
| **Function**         | **Purpose**                                           |
|---------------------|-----------------------------------------------------|
| `input.float()`      | Creates a user input for customizing wick tolerance. |
| `math.abs()`         | Returns the absolute value of the range and body size. |
| `math.max()`         | Returns the maximum value of open and close.         |
| `math.min()`         | Returns the minimum value of open and close.         |
| `plotshape()`        | Plots visual labels for Bullish and Bearish Marubozu. |

---

## **Summary**
The **Marubozu Pattern Detector** is a precise, user-friendly tool to identify and visualize bullish and bearish Marubozu patterns. With customizable wick tolerance, the script offers flexibility in how strict the detection should be. This tool is ideal for technical traders looking to spot strong momentum candles that could signal trend continuation or reversal points.

