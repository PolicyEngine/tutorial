# Tutorial setup — Analysing tax-benefit reform impacts with PolicyEngine

**IMA World Congress 2026 · Tutorial Session 4 · Friday 3 July, 10:30–12:00 · Room F (2300)**
**Presenter:** Max Ghenis (PolicyEngine) — questions about this tutorial or setup: **max@policyengine.org**

---

## TL;DR — there is almost nothing to install

This tutorial is **browser-based**. If you bring a laptop with a modern web browser and can get online, you are ready. Everything core runs at **[policyengine.org](https://policyengine.org)** with no account and no installation.

The optional steps below (a Google account for the notebook; a local Python install; the AI assistant) only matter if you'd like to follow specific parts hands-on. Skip them and you'll still be able to do everything in the browser.

> **A note on countries:** the hands-on examples use the **US** model, whose microdata is fully open. The **UK** model works identically, but its population microdata is not publicly downloadable, so UK population analysis is shown by the presenter rather than run on your own machine.

---

## 1. Required — for everyone (2 minutes)

1. A laptop with a current browser (Chrome, Firefox, Edge, or Safari).
2. Confirm you can reach **[policyengine.org](https://policyengine.org)** and **[app.policyengine.org](https://app.policyengine.org)** on the conference Wi-Fi (Eduroam).
3. *(Optional)* Create a free PolicyEngine account if you'd like to save your work — not required to follow along.

That's it. The household calculator, policy reforms, and population-level impact analysis (budgetary cost, distribution, poverty, winners and losers) all run in the browser.

---

## 2. Recommended — to follow the Python notebook (5 minutes)

Part of the session uses a short **Google Colab** notebook, which runs Python entirely in your browser — nothing is installed on your machine.

1. Make sure you can sign in to a **Google account** (Colab requires one).
2. Open the tutorial notebook — from the tutorial hub at **[policyengine.org/tutorial](https://policyengine.org/tutorial)**, or directly:
   https://colab.research.google.com/github/PolicyEngine/tutorial/blob/main/notebooks/policyengine_tutorial_ima2026.ipynb
3. *(Optional, to save time)* Open it before the session and run the first cell — it installs the `policyengine` package (~2–3 minutes the first time).

If you prefer not to use Colab, you can simply watch this portion; the same results are reproduced in the web app.

---

## 3. Optional — to run locally instead of Colab (advanced)

If you'd rather run on your own machine, you need **Python 3.10 or newer**, then:

```bash
pip install policyengine
```

This installs the unified PolicyEngine package (both US and UK tax-benefit models). Quick check:

```python
import policyengine as pe
result = pe.us.calculate_household(
    people=[{"age": 40, "employment_income": 50_000}],
    year=2025,
)
print(result.household.household_net_income)
```

Population-level microsimulation on the full national dataset is memory-intensive (it runs over ~100,000+ representative households). For the live session we use the web app or a small calibrated sample for that part; full-scale runs are better done after the workshop.

---

## 4. Optional — to try the AI assistant (demo)

PolicyEngine ships a **Claude Code plugin** that drives all of the above from plain-language prompts (e.g. *"What's the poverty effect of raising the Child Tax Credit to $3,000?"*). In the session this is a **demonstration** — you do not need to install anything to follow it.

If you'd like to try it yourself afterwards, you'll need [Claude Code](https://claude.com/claude-code) and an Anthropic account; setup instructions will be linked from [policyengine.org/tutorial](https://policyengine.org/tutorial).

---

## Summary

| You want to… | You need | Install ahead? |
|---|---|---|
| Follow the whole session | Laptop + browser + Wi-Fi | Nothing |
| Run the Python notebook hands-on | A Google account (for Colab) | Nothing (runs in browser) |
| Run Python locally instead | Python ≥3.10, `pip install policyengine` | Optional |
| Try the AI assistant yourself | Claude Code + Anthropic account | Optional (demo only) |

**Questions about this tutorial or the setup: contact Max Ghenis directly at max@policyengine.org.**
