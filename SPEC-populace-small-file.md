# Spec: `populace_us_20k` — a small, calibrated Populace artifact

**For:** the agent working on `policyengine/populace` (build pipeline).
**Why:** PolicyEngine tutorials, Colab, and CI need a Populace file small enough to run a national microsimulation in free-tier Colab (~12.7 GB RAM, want < ~6 GB and < ~30 s/sim) while still producing **headline national aggregates within ~1–2% of the full file**. A naive uniform subsample does **not** meet this bar (see findings below) — it needs calibration.

## Findings that motivate this (measured 2026-06-27)

Full Populace US 2024 = **224,026 households / 572,780 people**, 1.2 GB. Against a uniform 5k-household subsample (weights rescaled to preserve total household count), running `policyengine_us` for 2025:

| Metric | Full (target) | 5k uniform sample | Error |
|---|---|---|---|
| Aggregate net income | ~$23T | **$14.3T** | **−38%** |
| Aggregate tax | ~$6T | $3.3T | −45% |
| Aggregate benefits | ~$2T | $1.87T | −6% |

Uniform sampling collapses because income/tax totals are **tail-dominated** — a small random draw misses the rare high-income households. Benefits (broad-based) survive; income/tax do not. **Calibration to national targets is required**, not just reweighting.

## Requirements

1. **Size:** ~20k households (≈ 50k people) as the default; also consider a 10k variant. Name e.g. `populace_us_2024_20k.h5` (mirror the full file's naming/format exactly so it loads through the same path).

2. **Subsampling:** preserve household integrity — when a household is selected, keep all its members and their `tax_unit` / `spm_unit` / `family` / `marital_unit` rows (link via `person_household_id`, `person_tax_unit_id`, etc.). Keep the same HDF5 schema/keys as the full file so `policyengine_us.Microsimulation(dataset=...)` and `pe.us.managed_microsimulation` read it unchanged.

3. **Calibration (the point):** reweight the subsample with **L0 / microcalibrate** to hit national targets so headline aggregates match the full file within ~1–2%. Suggested targets: total population; population by age band and state; aggregate employment income, AGI, net income, federal tax; major program totals (SNAP, SSI, EITC, CTC, Social Security); SPM poverty rate. (This is the method from the IMA L0 subnational-calibration paper — reuse that machinery.)

4. **Validation:** ship a report comparing the 20k file to full Populace on: net income, tax, benefits, SNAP/SSI/EITC/CTC totals, SPM poverty rate, and income deciles (mean net income per decile). Document residual error per metric. Flag where small-N still degrades (expect state-level and fine decile cuts to be the weak spots).

5. **Publish:** as a first-class artifact in `policyengine/populace-us` (same provenance/manifest treatment as `populace_us_2024.h5`), so the managed bundle can reference it by name and `ensure_datasets`/`load_datasets` can fetch it. Add a manifest entry so `pe.us.managed_microsimulation(dataset="populace_us_2024_20k")` works without `allow_unmanaged`.

## Coordination note

A quick **uniform** sample (`populace_us_2024_{5,10,20}k.h5`) already exists locally at
`~/PolicyEngine/ima26-tutorial/` (built by the tutorial work) for testing only — it is **not calibrated** and should not be published. The calibrated artifact above supersedes it.
