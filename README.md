# LNG_Deal_Feasability_Calculator
Assess financial feasibility of LNG deals

## The Three-Notebook Architecture
lng_feasibility.ipynb          ←── Start here
  Section 8: Export JSON
         │
         │  lng_deal_YYYYMMDD.json
         ▼
lng_feasibility_extended.ipynb  ←── Option A
  Section 1: Load JSON
  Section 7: Export enhanced JSON
         │
         │  lng_deal_extended_YYYYMMDD.json
         ▼
lng_lifecycle.ipynb             ←── Option B
  Phase 1: Load either JSON
  Phases 2–10: Full execution

  ![alt text](image.png)