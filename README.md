# PolicyEngine tutorials

Source for **[tutorial.policyengine.org](https://tutorial.policyengine.org)** — a permanent home for hands-on PolicyEngine tutorials.

Static site (no build step) deployed on Vercel. Notebooks live in `notebooks/` so they open directly in Google Colab via the GitHub integration.

## Contents

| File | Purpose |
|------|---------|
| `index.html` | Landing page (lists tutorials; currently features IMA World Congress 2026). |
| `notebooks/policyengine_tutorial_ima2026.ipynb` | Colab notebook for the IMA 2026 tutorial — household calculator, reforms, charts, and population analysis with the `policyengine` package. |
| `participant-instructions.md` | Setup instructions shared with conference organisers (markdown for the conference site). |
| `SPEC-populace-small-file.md` | Spec for a calibrated small Populace dataset (`populace_us_20k`) for fast in-Colab population analysis. |

## Open the notebook in Colab

```
https://colab.research.google.com/github/PolicyEngine/tutorial/blob/main/notebooks/policyengine_tutorial_ima2026.ipynb
```

## Adding a tutorial

1. Drop the notebook in `notebooks/`.
2. Add a card to `index.html`.
3. Push — Vercel redeploys automatically.

## Local preview

Any static server, e.g. `python -m http.server`, then open `index.html`.
