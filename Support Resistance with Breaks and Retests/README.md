> https://www.tradingview.com/script/Xeeko6TV-Support-Resistance-with-Breaks-and-Retests/

**The Break and Retest indicator strives to provide a visual aid for spotting areas of continuation and pullbacks. Support and resistance levels are drawn out automatically and have sequential conditions in place to determine a breakout following an eventual retest. Additionally, there are methods in place that try and detect liquidation events and still output a retest.**

**Although there are options to adjust repaint settings, "potential labels" are structured in a way to detect live ongoing retest events and therefore will be the only thing in the script that will be forced to repaint.**


#### 🔳 Settings
* **Lookback Range:** Lookback period to trigger a new support/resistance level when pivot conditions are met.
* **Bars Since Breakout:** How many bars since breakout in order to detect a retest.
* **Retest Detection Limiter:** Whenever a potential retest is detected, the indicator knows that a retest is about to happen. In that given situation, this input grants the ability to raise the limit on how many bars are allowed to be actively checked while a potential retest event is active. For example, if you see the potential retest label, how many bars do you want that potential retest label to be active for to eventually confirm a retest?

#### 🔳 Repaint Options
**By default, the break and retest system uses the current close value to determine a condition. (Repaints by default)**
* **On: Allows repainting**
* **Off - Bar Confirmation:** Prevents repainting and generates alerts when the bar closes. (1 candle later)
* **Off - High & Low:** Prevents repainting, but in return utilizes both the high and low values instead of the close which may yield a higher outcome and inaccurate results.

#### 🔳 How it works
In the background, calculations aren't searching for the perfect retest within the zone but instead focuses its attention towards price fluctuation around the zones. This allows the indicator to yield more results than it would otherwise.
![](https://www.tradingview.com/x/8XHdcWHh)

The chart below provides an example of how potential retests are established. These are updated constantly until a retest is confirmed, and deleted if not. If a potential retest is active and the next candle drops below the value when the potential retest was detected, a retest is placed.
![](https://www.tradingview.com/x/rBMCpuxx)