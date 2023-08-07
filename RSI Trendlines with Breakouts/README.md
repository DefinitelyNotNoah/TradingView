> https://www.tradingview.com/script/YcKrOcXe-RSI-Trendlines-with-Breakouts/

#### A pivot-based breakout indicator that attempts to provide traders with a visual aid for finding breakouts on the RSI. Similar to how we use trendlines on our charts, using them on the Relative Strength Index can also give us a sense of direction in the markets.

This script uses its own pivot-based system that checks for real-time swing levels and triggers a new pivot event after every dip and nth bars. The breakout alerts that are given were not designed to be taken as signals since their purpose is to provide an extra bit of confluence. Because of this, I added no other conditions that try to make the alerts "perfect", but instead, print every breakout that is detected. Despite stating this, I did happen to add a condition that checks the difference in RSI and the breakout value, but that's as far as it'll go. There are alerts built-in to the script, along with adjustable repainting options.

> This script uses an external library that provide an object-oriented way of producing said trendlines developed by me, see here https://www.tradingview.com/script/85fU3JnE-Simple-Trendlines/



#### 🔳 Settings
* **Lookback Range:** Lookback period to trigger a new pivot point when conditions are met.
* **RSI Difference:** The difference between the current RSI value and the breakout value. How much higher in value should the current RSI be compared to the breakout value in order to detect a breakout?
* **RSI Settings**
* **Styling Options**

#### 🔳 **Repaint Options**
* **On**: Allows repainting
* **Off** - Bar Confirmation: Prevents repainting and generates alerts when the bar closes. (1 candle later)

#### 🔳 How it Works
Before a trendline is drawn, the script retrieves the slope between the previous pivot point and the current. Then it adds or subtracts the slope x amount of times (based on the lookback range) from the current pivot value until the current x-axis is reached. By doing this we can get a trendline that will detect a breakout accurately.
![](https://www.tradingview.com/x/EX9PIH97)
The result
![](https://www.tradingview.com/x/3eCxpJLG)

When using the RSI Difference condition, the script will print breakouts whenever the condition is true, because of this dotted lines were added to track where the alert was triggered.
![](https://www.tradingview.com/x/RRAu1zPc)
