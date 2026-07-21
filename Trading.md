You are spot on! In trading, a **Take Profit (TP)** order *is* mechanically just a Sell Limit Order set **above** the current market price.

When you set a limit price higher than where the option is currently trading, your broker holds that order until a buyer in the live market is willing to pay your requested price (or better).

Here is how the mechanics break down depending on where you place your limit price relative to the live market:

---

### Sell Limit Above Live Price = Take Profit

* **What happens:** The order stays open in the order book.
* **Execution:** It will only fill if the option's live Bid rises to match or exceed your target price.
* **Risk:** If the option price never reaches your higher target, your order sits unfilled while the option decays or drops in value.

### Sell Limit Below or Equal to Live Price = Immediate Sell

* **What happens:** The exchange sees a buyer already offering *more* than your minimum acceptable price.
* **Execution:** It fills **instantly** at the best available live market price.
* **Why it happened earlier:** Because your screen was delayed by 15 minutes, you set a limit price that you *thought* was above the market, but in reality, it was equal to or below the live price at that exact second.

---

### Key Comparison

| Order Goal | Order Type Used | Trigger Location | Purpose |
| --- | --- | --- | --- |
| **Take Profit (TP)** | **Sell Limit** | **Above** current market price | Lock in gains when price rises to your target. |
| **Stop Loss (SL)** | **Stop Limit / Stop Market** | **Below** current market price | Automatically trigger a sale if price falls to limit losses. |

If you want to set both at the same time on Webull, you can use a **Take Profit / Stop Loss (TPSO) Bracket Order** or an **OCO (One-Cancels-the-Other)** order, which places your high sell limit and your lower stop-loss together.

for webull options when selling closing long call options, you need to manually tweak the limit price or change to market order.

The important distinction is between **what you see** and **what the exchange sees**.

If you're using **OPRA 15-minute delayed options quotes** in Webull:

* **Your displayed bid/ask and last price are delayed by about 15 minutes.**
* **Your market order is still sent immediately to the market and executes against the current, real-time bid/ask**, not the delayed quote you're looking at.

So yes—you can absolutely get "surprised" if you're trading off delayed data.

For example:

* Your screen (delayed) shows an option at **$1.20 bid / $1.30 ask**.
* In reality, 15 minutes later, the market is **$0.75 bid / $0.85 ask**.
* You hit **Sell Market** expecting around $1.20.
* Your order executes around **$0.75** because that's the live market.

The reverse can happen too—you might get a better fill than your delayed quote if the market moved in your favor.

### Why this is especially risky with options

Options can move extremely fast, especially:

* near expiration,
* around earnings,
* when the underlying stock is volatile,
* or when liquidity is thin.

A 15-minute delay can make the displayed price almost meaningless in active markets.

### How to avoid it

Instead of a **market order**, use a **limit order**:

* If you want to sell, enter a limit price (e.g., $1.15).
* The order will only execute at **$1.15 or better**.
* If the live market is below that price, it simply won't fill until buyers are willing to pay your limit.

This protects you from unexpectedly poor executions.

### Did the delayed quote "cause" the bad fill?

Most likely, yes, in the sense that **you made the decision using stale information**. The exchange didn't execute using delayed prices—it executed using the live market. The delayed data only affected what you saw before submitting the order.

If you tell me:

* the stock ticker,
* the option strike and expiration,
* roughly what time you sold,
* and what price you expected versus what you got,

I can help figure out exactly what probably happened.
