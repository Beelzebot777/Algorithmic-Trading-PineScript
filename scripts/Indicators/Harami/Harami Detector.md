//@version=6
indicator("Crypto Harami Pattern Detector", overlay=true)

// 🔥 1️⃣ Detectar el patrón de Bullish Harami
bullishHarami = (open[2] > close[2] and close[1] > open[1] and close > open) and open[2] > close[1] and high[1] < open[2]

// 🔥 2️⃣ Detectar el patrón de Bearish Harami
bearishHarami = (open[2] < close[2] and open[1] > close[1] and open > close) and open[2] < close[1] and high[1] > open[2]

// 🔥 3️⃣ Mostrar el patrón Bullish Harami
plotshape(series=bullishHarami, location=location.belowbar, color=color.green, size=size.small, style=shape.triangleup, title="Bullish Harami Confirmation")
plotshape(series=bullishHarami, location=location.belowbar, color=color.green, size=size.small, style=shape.triangleup, offset=-1, title="Bullish Harami Candle")
plotshape(series=bullishHarami, location=location.belowbar, color=color.green, size=size.small, style=shape.triangleup, offset=-2, title="Bullish Harami Intro")

// 🔥 4️⃣ Mostrar el patrón Bearish Harami
plotshape(series=bearishHarami, location=location.abovebar, color=color.red, size=size.small, style=shape.triangledown, title="Bearish Harami Confirmation")
plotshape(series=bearishHarami, location=location.abovebar, color=color.red, size=size.small, style=shape.triangledown, offset=-1, title="Bearish Harami Candle")
plotshape(series=bearishHarami, location=location.abovebar, color=color.red, size=size.small, style=shape.triangledown, offset=-2, title="Bearish Harami Intro")

// 🧮 5️⃣ Contar los patrones detectados
var int bullishHaramiCount = 0
var int bearishHaramiCount = 0

if bullishHarami
    bullishHaramiCount += 1

if bearishHarami
    bearishHaramiCount += 1

// 📋 6️⃣ Crear la tabla en la esquina inferior derecha
var table haramiTable = table.new(position.bottom_right, 3, 3, bgcolor=color.new(color.gray, 90), frame_color=color.gray, frame_width=1)

// 📝 7️⃣ Definir los encabezados de la tabla
if bar_index == 0
    table.cell(haramiTable, 0, 0, "📘 Pattern", text_color=color.white, bgcolor=color.blue)
    table.cell(haramiTable, 0, 1, "📈 Count", text_color=color.white, bgcolor=color.blue)

// 📝 8️⃣ Mostrar la cantidad de Bullish Harami detectados
table.cell(haramiTable, 1, 0, "Bullish Harami", text_color=color.green)
table.cell(haramiTable, 1, 1, str.tostring(bullishHaramiCount), text_color=color.white)

// 📝 9️⃣ Mostrar la cantidad de Bearish Harami detectados
table.cell(haramiTable, 2, 0, "Bearish Harami", text_color=color.red)
table.cell(haramiTable, 2, 1, str.tostring(bearishHaramiCount), text_color=color.white)
