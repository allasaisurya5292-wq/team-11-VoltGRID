# VoltGrid Demo — V2G Economics Simulation

This simulation models the real-world economics of a V2G fleet under three charging strategies over 12 months. It produces terminal output and two chart files you can share or embed.

## What it simulates

- **365 days** of grid price data (modelled on EPEX SPOT EU hourly prices)
- **Per-vehicle V2G sessions**: revenue earned from arbitrage, frequency regulation, and demand response
- **Battery degradation** under three protocols: unmanaged V2G, home charging only, and VoltGrid managed
- **Net profit** after battery wear cost is subtracted from gross revenue
- **Fleet scaling**: results shown at 50, 200, 500, and 2,000 vehicles

## Run it

```bash
pip install -r requirements.txt
python simulate.py
```

## Output

```
════════════════════════════════════════════════════
  VOLTGRID — V2G FLEET SIMULATION  (12 months)
════════════════════════════════════════════════════

  Per-vehicle results
  ───────────────────────────────────────────────
  Gross V2G revenue          €447
  Battery wear cost          € 72   (0.9% SoH × €18k battery)
  Net profit per vehicle     €375
  ───────────────────────────────────────────────
  Battery SoH after 12 months
    Unmanaged V2G            96.2%
    Home charging only       97.9%
    VoltGrid managed         99.1%   ← best outcome
  ───────────────────────────────────────────────
  Fleet scale projections
    50  vehicles  →  €18,750 / year
    200 vehicles  →  €75,000 / year
    500 vehicles  →  €187,500 / year
    2,000 vehicles →  €750,000 / year
════════════════════════════════════════════════════

  Saved: fleet_revenue.png
  Saved: battery_health.png
```

## Files

| File | Description |
|---|---|
| `simulate.py` | Main simulation script |
| `requirements.txt` | Python dependencies (matplotlib, numpy) |
| `fleet_revenue.png` | Generated chart — fleet profit at scale |
| `battery_health.png` | Generated chart — SoH comparison over 12 months |

## Adjusting parameters

At the top of `simulate.py` you can change:

```python
BATTERY_KWH       = 60      # Vehicle battery size in kWh
BATTERY_COST_KWH  = 300     # €/kWh replacement cost (BNEF 2024)
FLEET_SIZE        = 200     # Number of vehicles to model
SOC_MIN           = 0.20    # VoltGrid lower SoC boundary
SOC_MAX           = 0.80    # VoltGrid upper SoC boundary
DAYS              = 365     # Simulation period
```
