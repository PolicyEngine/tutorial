# PolicyEngine tutorials

Source for the PolicyEngine tutorials hub — a permanent home for hands-on PolicyEngine tutorials.

Served at **[policyengine.org/tutorial](https://policyengine.org/tutorial)** (proxied from the main site, mirroring `/slides`) and at this project's own Vercel domain. Static site (no build step). Content is served under the `/tutorial` path (so it works both standalone and proxied); notebooks live in `notebooks/` so they open directly in Google Colab via the GitHub integration.

## Contents

| File | Purpose |
|------|---------|
| `tutorial/index.html` | Landing page (lists tutorials; currently features IMA World Congress 2026). Served at `/tutorial`. |
| `notebooks/policyengine_tutorial_ima2026.ipynb` | Colab notebook for the IMA 2026 tutorial — household calculator, reforms, charts, and population analysis with the `policyengine` package. |
| `participant-instructions.md` | Setup instructions shared with conference organisers (markdown for the conference site). |
| `SPEC-populace-small-file.md` | Spec for a calibrated small Populace dataset (`populace_us_20k`) for fast in-Colab population analysis. |

## Open the notebook in Colab

```
https://colab.research.google.com/github/PolicyEngine/tutorial/blob/main/notebooks/policyengine_tutorial_ima2026.ipynb
```

## Adding a tutorial

1. Drop the notebook in `notebooks/`.
2. Add a card to `tutorial/index.html`.
3. Push — Vercel redeploys automatically.

## Local preview

Any static server, e.g. `python -m http.server`, then open `/tutorial/`.
