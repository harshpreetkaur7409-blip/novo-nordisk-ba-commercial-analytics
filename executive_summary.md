# Executive Summary - Commercial & Field Force Performance (Jan-Oct 2026)
*Personal/Academic Project - built on 100% synthetic data; figures are illustrative, not real company performance.*

## Headline
Sales reached **INR 108.9 Cr** across 500 HCPs and 20 territories. Monthly sales grew **14.1%** from Jan to Oct, led by **GLP-1 Weekly** (45% of sales, +2.8% monthly growth). **Premix Insulin** is the only product with falling momentum (-0.2%/month).

## What the data says
| # | Insight | Evidence |
|---|---------|----------|
| 1 | Business is concentrated | Top 20% of HCPs = **50%** of sales; top 5 territories = **37%** |
| 2 | Calls help, with diminishing returns | Controlling for HCP potential: 2nd to 3rd call = **+8.0%** sales vs 5th to 6th = **+4.2%** |
| 3 | Engagement and digital add on top of calls | +10 engagement points = **+5.3%**; +1 digital touchpoint = **+3.9%** |
| 4 | Field productivity varies widely | Sales per call: best **Nagpur** INR 59,612 vs lowest **Chandigarh** INR 25,125 |
| 5 | Revenue leakage is identifiable | **90 HCPs** fell >15% (last 3 vs prior 3 months) - about **INR 1.3 Cr** per quarter at risk |

## Next-best actions (rule-based, HCP-level list in `outputs/hcp_next_best_actions.csv`)
1. **Rescue 90 declining HCPs** - restore call frequency where reps pulled back; add medical/KAM involvement where calls were stable. *KPI: recover 50% of the lost run-rate in 1 quarter.*
2. **Protect 89 key accounts** (top-quintile sales) with a named account plan and scientific engagement. *KPI: zero unplanned decline.*
3. **Activate digital for 35 highly engaged but digitally quiet HCPs** - webinar / e-detailing invites. *KPI: digital touchpoints per HCP, engagement score.*
4. **Re-engage 36 low-engagement HCPs receiving above-median calls** - switch channel or message instead of adding calls. *KPI: engagement score +5 points.*
5. **Reallocate effort from 8 low-return-per-call, above-median-call HCPs** to higher-response accounts (use the diminishing-returns curve). *KPI: sales per call.*

## Caveats
Synthetic data; response model shows association (within-HCP, R2 = 0.39), not proven causation - validate with a field pilot (test vs control territories) before scaling. NBA thresholds are editable in `src/analytics.py`.
