# Lens 1 — Supply Chain & Value Flow

Methodology distilled from Serenity ([@aleabitoreddit](https://x.com/aleabitoreddit))'s
AI/semiconductor supply-chain framework. Full distillation with dated examples:
[WOOK98/serenity-aleabitoreddit](https://github.com/WOOK98/serenity-aleabitoreddit)
— install that skill alongside this plugin for maximum depth.

## Core question

Where does this company sit in its value chain, and is it (or does it depend
on) a **bottleneck** — a sole/near-sole-source chokepoint that downstream
buyers must pay through rather than design around?

## What to produce in this section

1. **Map the chain explicitly.** Trace from end demand down to inputs, e.g.:
   hyperscaler capex → ASICs/GPUs → optical transceivers → InP epiwafer →
   InP substrate → indium feedstock. Place the company on the map. Never
   conflate layers (substrate ≠ epiwafer ≠ foundry ≠ laser ≠ transceiver ≠
   module) — layer confusion is the #1 quality failure of this section.
2. **Bottleneck test.** Sole/near-sole source? Qualified substitutes and how
   long a competitor's qualification cycle would take? Real pricing power?
   Distinguish quantity constraints from price power — a monopolist doesn't
   need more volume, just higher prices.
3. **BOM share logic.** Estimate what % of the downstream system's bill of
   materials this component represents. Cheap components (single-digit % of
   BOM) in critical paths are ideal: buyers pay through price hikes rather
   than cut capex.
4. **Demand driver.** Is the chain's TAM expanding on hyperscaler AI capex /
   physical-AI capex, or is it a legacy/cyclical market wearing an AI story?
5. **Evidence over narrative.** Prefer OSINT signals: conference slides,
   SEC filings, investor decks, customer/partner-page changes, job postings,
   signed take-or-pay contracts. A signed multi-year contract from a
   creditworthy counterparty (Mag7-grade) is the strongest single datapoint;
   customer concentration in a cash-burning counterparty is the opposite.
6. **Priced or not.** Is institutional coverage still behind the supply-chain
   evidence (edge), or already in (crowded/frontrun)?

## Anti-patterns to flag

- Confident commentary that conflates supply-chain layers.
- "Shovel seller" theses that stop at the obvious large-cap instead of
  tracing upstream.
- ARR/contract claims with no counterparty quality check.

## Output

A short chain diagram (text arrows are fine), the bottleneck verdict
(is / feeds / is hostage to a bottleneck — or none), and the 2–3 strongest
pieces of chain evidence with dates.
