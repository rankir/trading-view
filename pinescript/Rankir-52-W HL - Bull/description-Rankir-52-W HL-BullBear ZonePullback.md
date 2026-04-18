Here's a comprehensive description of your Pine Script indicator:

---

## Rankir-52-W HL — Bull/Bear Zone & Pullback
### Indicator Description

---

### **What This Indicator Does**

This is a **52-Week High/Low tracker** built for Indian equity markets on TradingView. It identifies whether a stock is in a **Bull Zone or Bear Zone** based on how far the current price has fallen from its 52-week high, and provides real-time label annotations directly on the price chart.

---

### **Core Logic**

#### 📐 52-Week High & Low Calculation
- Looks back **252 trading days** (standard Indian market year) to find the highest high and lowest low
- Additionally enforces a **365 calendar day limit** — so even if 252 trading days stretch beyond a year due to holidays, the data stays within a true 52-week window
- Uses a **dynamic lookback** that safely handles stocks with fewer bars than 252 (e.g. recently listed stocks)

#### 🎯 Drop % from 52-Week High
- Formula: `(52W High − Close) / 52W High × 100`
- This is the **primary signal metric** — tells you how far the stock has corrected from its peak
- Also tracks the **previous bar's drop %** to detect zone transitions

#### 📈 Up % from 52-Week Low *(recently added)*
- Formula: `(Close − 52W Low) / 52W Low × 100`
- Shows **how much the stock has recovered from its bottom**
- Only displayed in labels when `Drop % < 15%` — i.e. when the stock is in or near Bull Zone, making it meaningful as a recovery strength indicator

#### ⚡ Intraday Pullback %
- Formula: `(Close − Day's Low) / Day's Low × 100`
- Measures **intraday strength** — how much the stock recovered from its daily low to close
- Displayed in labels only when this exceeds **5%** (significant intraday reversal)

---

### **Zone Classification**

| Zone | Condition | Label Color |
|------|-----------|-------------|
| 🟢 **Bull Zone** | Drop from 52W High ≤ 15% | Green |
| 🔴 **Bear Zone** | Drop from 52W High > 15% | Red |

**Zone Transition Detection** — The indicator specifically watches for the moment a stock **crosses the 15% threshold**:
- Previous bar > 15% drop AND current bar ≤ 15% → **Bull Zone entry** (recovery signal)
- Previous bar ≤ 15% drop AND current bar > 15% → **Bear Zone entry** (breakdown signal)

---

### **What the Chart Labels Show**

Labels appear **only on the last/current bar** to avoid chart clutter.

**On Zone Transition (Bull/Bear crossover):**
```
52W High: ₹1,46,500
Current Drop %: 7.85%
Prev Bar Drop %: 15.36%
Intraday Increase: 7.95%     ← only if > 5%
Up from 52W Low: 23.40%      ← only if Drop% < 15%
```

**On Normal Bar (no transition):**
```
7.85%
Intraday Increase: 7.95%     ← only if > 5%
Up from 52W Low: 23.40%      ← only if Drop% < 15%
```

---

### **Chart Markers**

| Marker | Condition | Position |
|--------|-----------|----------|
| 🔺 Green triangle (up) | Stock hits new 52-week high | Above the bar |
| 🔻 Red triangle (down) | Stock hits new 52-week low | Below the bar |

---

### **Alerts Available**

| Alert | Trigger |
|-------|---------|
| New 52-Week High | Price makes fresh 52W high |
| New 52-Week Low | Price makes fresh 52W low |
| Entered Bull Zone | Stock recovers above −15% threshold |
| Entered Bear Zone | Stock falls below −15% threshold |
| Drop crosses threshold | Configurable custom drop level |
| Recovery crosses threshold | Configurable custom recovery level |
| Intraday pullback | Intraday low-to-close move exceeds threshold |

---

### **User Inputs**

| Input | Default | Purpose |
|-------|---------|---------|
| Period (Trading Days) | 252 | Lookback for 52W High/Low |
| Show Drop % Plot | On | Hidden plot for external use |
| Show Pullback % Plot | On | Hidden plot for external use |
| Drop Alert Threshold | 10% | Custom alert trigger level |
| Pullback Threshold | 5% | Intraday move alert level |

---

### **Practical Use Cases**

1. **Momentum screening** — Stocks with Drop% < 15% are near 52W highs, indicating strength
2. **Bear market exits** — Bear Zone entry alert warns you before a stock breaks down significantly
3. **Recovery confirmation** — Bull Zone entry + high "Up from 52W Low%" together confirm a genuine recovery
4. **Intraday reversal** — 5%+ intraday increase from low signals strong buying interest on that day
5. **Watchlist filtering** — Green label = Bull Zone candidate, Red label = avoid or reduce

---

### **Designed For**
- Indian equity markets (NSE/BSE daily charts)
- Momentum and swing traders
- Portfolio review and stock screening workflows
- Works best on **Daily (1D) timeframe**