# Lens 4 — Technicals

## HARD GUARDRAIL — read first

Every number in this section (price, support/resistance levels, RSI, MACD,
moving averages, IV, short interest) MUST come from verifiable current
sources retrieved during this session, each with an as-of date. Preferred
source: the `airesearch-data` MCP tool `get_technicals`, which computes
SMA20/50/200, RSI14, MACD, swing support/resistance, 52w range, and volume
ratio deterministically from real candles. If that tool is unavailable,
fall back to web-searchable data with dates. If real market data cannot be
retrieved by either path, output exactly:

> **Technicals: insufficient data — section withheld.** Live price and
> indicator data could not be verified for <TICKER>; no technical read is
> provided rather than an estimated one.

Never reconstruct chart patterns, indicator values, or entry/stop levels
from memory or plausibility. A fabricated-but-professional-looking
technical section is the single most dangerous failure this skill can
produce. This lens also NEVER outputs buy/sell instructions — levels are
descriptive context, not entries.

## Core question

What are price, structure, and flow saying — as a TIMING overlay on the
fundamental thesis, never as a standalone signal. House view: "TA is snake
oil without fundamentals, catalysts, and macro." This section exists to time
entries/exits on a thesis established by the other lenses.

## What to produce in this section

1. **Trend & levels.** Price vs. 50/200-day trend, the 2–3 levels that
   actually matter (prior breakout, high-volume node, ATH), distance from
   52-week high/low.
2. **Float & structure.** Float size, insider/institutional ownership,
   short interest and days-to-cover. Small float + high short interest +
   improving fundamentals = squeeze structure worth noting (the
   profitable-grower variant is the credible one; junk squeezes are not a
   thesis).
3. **Flow reading (if findable).** Unusual volume, dark-pool prints,
   institutional accumulation patterns, options structure — IV level vs.
   realized, skew, where open interest clusters. Elevated IV changes the
   instrument choice (spreads/shares over naked calls); binary event risk
   with cheap vega argues for defined-risk options.
4. **Catalyst calendar.** Dated upcoming events within a tradable window:
   earnings, conferences, index inclusion, lockup expiries, policy dates.

## Output

Trend verdict (uptrend/downtrend/range), key levels, one line on structure
(float/short/IV), and the next dated catalyst. Explicitly subordinate to the
fundamental verdict: note whether technicals suggest acting now, waiting for
a level, or that timing is irrelevant for a long-horizon position.
