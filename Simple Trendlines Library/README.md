> https://www.tradingview.com/script/85fU3JnE-Simple-Trendlines/

#### 📈 Trendlines, made easy.
**Simple Trendlines is a carefully made library that provides an easy and accessible way to draw trendlines on the chart.**

**Containing only 10 properties and 2 methods, the implementation is designed to be understandable through an object-oriented structure and provides developers the opportunity to expand without having to deal with slope calculation while also ensuring that there's no leakage between the trendlines before they're drawn.**

#### Developers only need to provide 5 expressions to get everything up in running. This includes the following but is not limited to
* The x-axis
* Point A (Y1 Value)
* Point B (Y2 Value)
* A condition to draw the line
* A condition to keep the trendline under continuation
  
**Automatic x-axis calculation is not a built-in feature due to the inconsistency it could bring.**

#### 📕 Quick Example

```cpp
import HoanGhetti/SimpleTrendlines/1 as tl

input_len = input.int(defval = 10)
pivotLow = fixnan(ta.pivotlow(input_len, input_len))

xAxis = ta.valuewhen(ta.change(pivotLow), bar_index, 0) - ta.valuewhen(ta.change(pivotLow), bar_index, 1)
prevPivot = ta.valuewhen(ta.change(pivotLow), pivotLow, 1)
pivotCondition = ta.change(pivotLow) and pivotLow > prevPivot 

plData = tl.new(x_axis = xAxis, offset = input_len)
plData.drawLine(pivotCondition, prevPivot, pivotLow)
plData.drawTrendline(close > 0)

plData.lines.trendline.set_style(line.style_dashed)
plData.lines.trendline.set_width(2)
plData.lines.startline.set_width(2)
```
**Excluding the styling at the bottom, that was only 8 lines of code which yields the following result.**
![](https://www.tradingview.com/x/I7Ds0cDs)

#### ⏳ Before continuing

* The library does not support block-scoped execution. Conditions must be declared before and integrated as a parameter. This doesn't limit any capabilities and only involves thinking logically about precedence. It was made this way for code readability and to keep things organized.
* The offset value inside the TrendlineSettings object can potentially affect performance (although very minimal) if you're using strict mode. When using strict mode, it loops through historical values to then do backend calculations.

#### 🔽 Getting Started 🔽

Creating trendlines without a library isn't a hard task. However, the library features a built-in system called strict mode. We'll dive further into this below.

#### Creating an Instance
You can create an instance of the library by calling the `new()` function. Passing an identifier is conventionally mandatory in this case so you can reference properties and methods.
```cpp
import HoanGhetti/SimpleTrendlines/2 as tl 
lineData = tl.new(int x_axis, int offset, bool strictMode, int strictType)
___
int x_axis (Required) // The distance between point A and point B provided by the user.
int offset (Optional) // The offset from x2 and the current bar_index. Used in situations where conditions execute ahead of where the x2 location is such as pivot events.
bool strictMode (Optional) // Strict mode works in the backend of things to ensure that the price hasn't closed below the trendline before the trendline is drawn.
int strictType (Optional) // Only accepts 0 and 1, 0 ensures that the price during slope calculation is above the line, and 1 ensures that the price during slope calculation is below the line.
```

#### The Initial Line
After instantiating the library, we can go ahead use the identifer we made above and create an instance of our initial line by calling the `drawLine()` method.
```cpp
lineData.drawLine(bool condition, float y1, float y2, float src)
___
bool condition (Required) // The condition in order to draw a new line.
float y1 (Required) // The y-value of point A.
float y2 (Required) // The y-value of point B.
float src (Optional) // Determines which value strict mode will actively check for leakage before a trendline is drawn.
// Typically used if you're not referencing OHLC values for your y-values, or you want to check for another value to exceed the line besides using the close value.
```
#### The Trendline
The trendline that gets drawn solely uses the values of the initial line and can be called using the drawTrendline() method. The library enforces a condition as a parameter in order to maintain simplicity.
```cpp
lineData.drawTrendline(bool condition)
___
bool condition (Required) // The condition in order to maintain and continue drawing the trendline.
```

#### ⚙️Features

#### 🔹Automatic Slope Calculation
In the background, the library calculates the next Y2 and X2 values on every tick for the trendline. Preventing the developer from having to do such a process themself.

#### 🔹Object-Oriented
Each object contains manipulative properties that allow the developer to debug and have the freedom they want.

#### 🔹Enforced Error Checking
Runtime errors have been put in place to ensure you're doing things correctly.

#### 🔹Strict Mode & Offset
Strict mode can only be used when the offset value is over 0. It's a feature that's only meant to function under scenarios where a condition executes further than where the X2 is relative to the current bar_index value.

---

Let's think about pivot systems. As you're aware, pivot events are detected based on historical factors. If a swing low occurred nth bars ago, then the pivot condition will execute at the current bar_index instead of executing nth bars back.

Now because of this, what if you wanted to draw a trendline when the pivot event is executed? The offset value takes care of this just as you would when developing your other scripts, basically how we always do bar_index - n. However, what does this mean for strict mode?

The photo below represents the logic behind the execution.
snapshot
When looking at this image, imagine this just happened, the event just executed and the trendline is now drawn. Pay attention to all the values inside the surrounding box. As you can see there are some candles that closed below the trendline before the trendline was drawn.

From what I can see 5-6 candles closed below the trendline during slope calculation. The goal of strict mode is to be a provisional system that prevents such occurrences from happening.
Here's a photo with strict mode on.
![](https://www.tradingview.com/x/qzHVwIiU)


#### 🔹Strict Type
A parameter used in the new() function that acts as a representation of what strict mode should calculate for. It accepts only two values, 0 and 1.
```
0 - Ensures that all candles have closed above the trendline before the trendline is drawn.
1 - Ensures that all candles have closed below the trendline before the trendline is drawn.
```
In the most recent photo above, I used 0 for strict type, since I was wanting to have a clean trendline and ensure that not a single candlestick closed below.
If you want to reference something else besides the close value during strict mode calculation, you can change it in the drawLine() method.
If it's still difficult to understand, think 0 for pivot lows, and 1 for pivot highs.

#### 📕 Methods and Property Inheritance
![](https://www.tradingview.com/x/vGETUjPS)