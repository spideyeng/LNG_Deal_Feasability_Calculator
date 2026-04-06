# LNG Deal Feasibility Calculator

Assess financial feasibility of LNG deals — from origination through settlement.

Three interactive Jupyter notebooks that chain together via JSON exports, covering deal evaluation, credit/IFRS 9/approval workflows, and full post-trade lifecycle execution.

---

## Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook, JupyterLab, or Google Colab

Core dependencies (`numpy`, `pandas`, `matplotlib`, `scipy`, `ipywidgets`) are **auto-installed** by each notebook's Cell 0 on first run — no manual `pip install` needed.

### Running in Google Colab

1. Upload the notebook to [colab.google](https://colab.research.google.com/)
2. **Runtime → Run all**
3. Widgets (sliders, buttons) work out of the box
4. JSON exports trigger a browser download dialog automatically

### Running in Local Jupyter

1. Clone the repo:
   ```
   git clone https://github.com/spideyeng/LNG_Deal_Feasability_Calculator.git
   cd LNG_Deal_Feasability_Calculator
   ```
2. Launch Jupyter:
   ```
   jupyter notebook
   ```
3. Open any notebook and **Kernel → Restart & Run All**
4. Cell 0 installs `widgetsnbextension` / `jupyterlab-widgets` automatically. **If sliders don't render on the first run, restart the notebook server once** — they will work on all subsequent runs.
5. JSON exports render a clickable download link directly in the output cell.

---

## The Three-Notebook Architecture

```
lng_feasibility.ipynb          ←── Start here
  Section 8: Export JSON
  │
  │  lng_deal_YYYYMMDD.json
  ▼
lng_feasibility_extended.ipynb ←── Option A (pre-trade)
  Section 1: Load JSON
  Section 7: Export enhanced JSON
  │
  │  lng_deal_extended_YYYYMMDD.json
  ▼
lng_lifecycle.ipynb            ←── Option B (post-trade)
  Phase 1: Load either JSON
  Phases 2–10: Full execution
```

Each notebook reads the JSON produced by the one before it. You can also enter values manually at any stage if you don't have the upstream JSON.

---

## Notebook 1 — `lng_feasibility.ipynb`

**LNG Deal Financial Feasibility Analyser** — core deal evaluation.

| Section | What it does |
|---|---|
| 1. Cargo & Volume Parameters | Vessel capacity, LNG density, calorific value, BOG rate, voyage days |
| 2. Pricing Formula | Buy/sell price structures (JCC, JKM, TTF, fixed), FX rate |
| 3. Shipping, Terminal & Cost Structure | Freight, regasification, storage, brokerage, insurance |
| 4. Risk Parameters | Hedge ratio/price, VaR confidence/horizon, stress test shocks |
| 5. Full Analysis Engine | Computes P&L, breakeven, NPV, VaR, credit utilisation |
| 6. Full Feasibility Report | Visual dashboard with Go/No-Go verdict |
| 7. Multi-Scenario Comparison | Side-by-side comparison of 4 user-defined scenarios |
| 8. Export Deal Sheet | Saves all inputs + results as JSON |

**Output:** `lng_deal_YYYYMMDD.json`

---

## Notebook 2 — `lng_feasibility_extended.ipynb` (Option A)

**Extended Deal Evaluation** — credit, IFRS 9, netback, vessel selection, and approval workflow.

| Section | What it does |
|---|---|
| 1. Load Deal | Imports JSON from Notebook 1 (or manual entry) |
| 2. Credit & Counterparty Check | Rating, exposure limits, Altman Z-score, payment history |
| 3. IFRS 9 Hedge Accounting | OCI vs P&L split, effectiveness testing |
| 4. Multi-Destination Netback | Compare delivered economics across destinations (Japan, Korea, China, Europe, India) |
| 5. Vessel Selection & Laycan | Pick vessel, schedule laycan window, canal transit |
| 6. Deal Approval Workflow | Simulated sign-off from trader, risk, credit, head of trading |
| 7. IFRS 9 Adjusted P&L Summary | Approval-ready P&L with OCI treatment + enhanced JSON export |

**Output:** `lng_deal_extended_YYYYMMDD.json`

---

## Notebook 3 — `lng_lifecycle.ipynb` (Option B)

**Deal Lifecycle — Execution to Settlement** — post-trade operations with full GL journal entries.

| Phase | What it does |
|---|---|
| 1. Load Confirmed Deal | Imports JSON from Notebook 1 or 2 |
| 2. Bill of Lading & Title Transfer | BL data entry, inventory recognition |
| 3. In-Transit Lifecycle & Accruals | Daily BOG accrual, freight accrual, cross-month detection |
| 4–5. Discharge, Outturn & Demurrage | NOR, outturn quantity, demurrage calculation |
| 6. Invoice Generation | Formal invoice from outturn data, AR posting |
| 7–8. GL Journal Ledger & Cash Settlement | Full double-entry ledger, AP/AR settlement, trial balance |
| 9–10. Month-End Close & Final P&L | Checklist, reconciliation, final P&L waterfall |

---

## JSON Export — Colab vs Local

Both environments are fully supported. The notebooks auto-detect where they're running:

| Environment | What happens on export |
|---|---|
| **Google Colab** | Browser download dialog opens automatically |
| **Local Jupyter** | A clickable download link appears in the cell output |

The JSON file is also saved to the working directory in both cases, so it's available for the next notebook in the chain.

---

## Quick Reference — Key Input Ranges

| Parameter | Typical Range | Notes |
|---|---|---|
| Vessel Capacity | 65,000 – 266,000 m³ | Standard = 138,000–155,000 m³ |
| LNG Density | 0.42 – 0.50 t/m³ | Depends on gas composition |
| Calorific Value | 19.0 – 23.5 MMBtu/t | Higher = richer gas |
| BOG Rate | 0.08% – 0.15%/day | Modern vessels at lower end |
| JCC Slope | 0.13 – 0.16 | Long-term Asia SPA norm |
| JKM Spot | $8 – $20/MMBtu | Market dependent |
| TTF Equivalent | $6 – $25/MMBtu | European benchmark |
| Voyage Charter | $1.50 – $5.00/MMBtu | Spot rate volatile |
| Regasification | $0.20 – $0.80/MMBtu | By terminal type |
| Hedge Ratio | 50% – 100% | Trader's market view |
| VaR Confidence | 95% – 99% | Risk appetite |

---