# **Pivot Points High & Low Script Documentation**

## **Overview**
This Pine Script indicator detects and plots **pivot highs** and **pivot lows** on a chart. It uses labels and lines to visually represent the most recent pivot points, while ensuring performance optimization by limiting the number of displayed pivots.

---

## **Script Code**

```pinescript
//@version=6
indicator("Pivot Points High & Low", overlay = true)

int legsInput = input(10, title="Legs Input")

// Define the `pivotPoint` UDT containing the time and price of pivots.
type pivotPoint
    int openTime
    float level

// Create empty arrays for storing High and Low pivots
var pivotHighArray = array.new<pivotPoint>()
var pivotLowArray = array.new<pivotPoint>()

// Detect new pivots
pivotHighPrice = ta.pivothigh(legsInput, legsInput)
pivotLowPrice = ta.pivotlow(legsInput, legsInput)

// Add new High pivots to the array
if bar_index > legsInput and not na(pivotHighPrice)
    newPivotHigh = pivotPoint.new(time[legsInput], pivotHighPrice)
    array.push(pivotHighArray, newPivotHigh)

// Add new Low pivots to the array
if bar_index > legsInput and not na(pivotLowPrice)
    newPivotLow = pivotPoint.new(time[legsInput], pivotLowPrice)
    array.push(pivotLowArray, newPivotLow)

// Draw pivot labels and connecting lines
if barstate.islastconfirmedhistory
    int maxPivots = 25  // Maximum pivots to display
    
    // Draw High Pivot Points
    var pivotPoint previousHighPoint = na
    for i = math.max(0, array.size(pivotHighArray) - maxPivots) to array.size(pivotHighArray) - 1
        eachPivot = array.get(pivotHighArray, i)
        label.new(eachPivot.openTime, eachPivot.level, str.tostring(eachPivot.level, format.mintick), 
                  xloc=xloc.bar_time, yloc=yloc.abovebar, textcolor=color.white, 
                  style=label.style_label_center, size=size.small)
        if not na(previousHighPoint)
            line.new(previousHighPoint.openTime, previousHighPoint.level, eachPivot.openTime, 
                     eachPivot.level, xloc=xloc.bar_time, color=color.blue, width=2)
        previousHighPoint := eachPivot

    // Draw Low Pivot Points
    var pivotPoint previousLowPoint = na
    for i = math.max(0, array.size(pivotLowArray) - maxPivots) to array.size(pivotLowArray) - 1
        eachPivot = array.get(pivotLowArray, i)
        label.new(eachPivot.openTime, eachPivot.level, str.tostring(eachPivot.level, format.mintick), 
                  xloc=xloc.bar_time, yloc=yloc.belowbar, textcolor=color.white, 
                  style=label.style_label_center, size=size.small)
        if not na(previousLowPoint)
            line.new(previousLowPoint.openTime, previousLowPoint.level, eachPivot.openTime, 
                     eachPivot.level, xloc=xloc.bar_time, color=color.red, width=2)
        previousLowPoint := eachPivot
```

# **How It Works**

## **1. Inputs**
### **`legsInput`**:
- Determines the number of bars to the left and right to confirm a pivot point.  
- **Example**: If `legsInput = 10`, the pivot is valid only if it is the highest/lowest value among 10 bars on each side.

---

## **2. Pivot Point Detection**
- **`ta.pivothigh`**: Detects pivot highs (local peaks).  
- **`ta.pivotlow`**: Detects pivot lows (local troughs).  

These pivot points are stored in two separate arrays:
- **`pivotHighArray`**: Stores pivot highs.  
- **`pivotLowArray`**: Stores pivot lows.

---

## **3. Drawing Logic**
On the **last historical bar**, the script:
1. Retrieves the **most recent pivot points** (up to a limit of `maxPivots = 25`).  
2. Draws:  
   - **Labels**:  
     - **High pivots**: Above the bar (`yloc.abovebar`).  
     - **Low pivots**: Below the bar (`yloc.belowbar`).  
   - **Lines**: Connect consecutive pivots (blue for highs, red for lows).

---

## **Key Features**

### **Efficient Drawing**:
- Limits the number of pivot points to display (`maxPivots = 25`) to avoid exceeding Pine Script's graphical limits.

### **Custom Visualization**:
- **High pivots**: Displayed with white labels and connected by blue lines.  
- **Low pivots**: Displayed with white labels and connected by red lines.

### **Dynamic Detection**:
- Pivots are detected **dynamically** as the chart progresses and stored in arrays for efficient access.

---

## **Visual Output**

### **High Pivot Points**:
- **Labels**: Appear **above the bar**.  
- **Lines**: Connect consecutive High pivots in **blue**.

### **Low Pivot Points**:
- **Labels**: Appear **below the bar**.  
- **Lines**: Connect consecutive Low pivots in **red**.

---

## **Functions Used**

| **Function**       | **Purpose**                                                     |
|--------------------|-----------------------------------------------------------------|
| `ta.pivothigh`     | Detects local highs (peaks) based on `legsInput`.               |
| `ta.pivotlow`      | Detects local lows (troughs) based on `legsInput`.              |
| `array.push()`     | Adds a new pivot point to the array.                            |
| `array.get()`      | Retrieves a pivot point from the array.                         |
| `label.new()`      | Creates labels at pivot points with customizable appearance.    |
| `line.new()`       | Draws lines connecting consecutive pivot points.                |
| `math.max()`       | Ensures the array index does not go below 0 when limiting pivots.|

---

## **Customization**

You can customize the script as follows:

### **1. Number of pivots displayed**
- Modify `maxPivots` to adjust the number of recent pivots drawn.

### **2. Appearance**
- **Line colors**: Change `color.blue` (highs) and `color.red` (lows).  
- **Label size**: Use `size.small`, `size.normal`, or other predefined constants.

### **3. Pivot Sensitivity**
- Adjust `legsInput` to detect pivots with more or fewer bars.

---

## **Example Settings**

| **Parameter**   | **Default Value** | **Description**                                |
|-----------------|------------------|----------------------------------------------|
| `legsInput`     | 10               | Number of bars on each side for pivot detection. |
| `maxPivots`     | 25               | Maximum number of High and Low pivots to display. |

---

## **Notes**
- Pine Script has a **limit of 50 labels and 50 lines** at any given time.  
- By limiting pivots to the **most recent 25**, the script ensures smooth performance and avoids exceeding graphical limits.

---

## **Output Preview**

| **Visualization**      | **Color**         | **Placement**       |
|------------------------|-------------------|---------------------|
| **High Pivot Labels**   | White Text        | Above the bar       |
| **High Pivot Lines**    | Blue              | Connects pivots     |
| **Low Pivot Labels**    | White Text        | Below the bar       |
| **Low Pivot Lines**     | Red               | Connects pivots     |

---

## **Summary**
This script efficiently detects and visualizes **pivot highs** and **pivot lows** on a chart. It ensures performance optimization by limiting the number of objects drawn and provides customizable visualizations for clarity and usability.


