# Emergency Department Suite

A unified collection of clinical decision support tools designed for offline use in the Emergency Department.

## Modules

| Module | Description |
|--------|-------------|
| 🫀 **ECG Decision Support** | Tachycardia algorithm, ECG measurement calculator, pattern recognition |
| 🏥 **ICU Admission Suite** | 22-section admission form with qSOFA, SOFA, APACHE II, SBAR handover |
| 🫁 **ER Airway Assistant** | RSI workflow, drug calculator, failed airway algorithm, cricothyrotomy |
| 📋 **Consultant Assistant** | Complaint-based workflows: fever, breathlessness, DKA, trauma, stroke |
| 💉 **T2DM Navigator** | Type 2 diabetes medication selection, HbA1c targets, complications screening |

## Features

- **Works Offline** — PWA with service worker, no internet required after first load
- **Mobile-First** — Designed for use on phones and tablets at the bedside
- **Print Support** — Configurable margins for hospital letterhead (up to 80mm top margin)
- **Word Export** — All modules export to .doc format for clinical notes
- **Unified Hub** — Single entry point to access all tools

## Printing on Hospital Letterhead

All modules support adjustable print margins:
- **Top margin**: Set to ~65mm (2.5 inches) to clear hospital header
- **Left margin**: Adjust if paper has a ruled left border
- Settings persist during the session

## Deployment

### GitHub Pages
1. Push to GitHub
2. Go to Settings → Pages → Source: main branch
3. Site deploys at `https://username.github.io/repo-name/`

### Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase deploy
```

## Local Use

Open `index.html` in any browser. No server required.

## Changelog

### v1.3 (2026-09-02)
- **DKA/HHS workflow integrity:** definitive biochemical DKA/HHS/mixed/euglycaemic classification now takes priority over symptom-weighted diagnosis scoring when sufficient biochemical data are entered.
- **Insulin safety:** HHS insulin output is now potassium-gated; K+ <3.5 mmol/L explicitly prevents insulin initiation.
- **Trajectory support:** added previous glucose/time inputs to display observed glucose fall without automatic insulin escalation.
- **Osmolality:** added optional measured osmolality input and incorporated it into HHS hyperosmolarity/resolution logic.
- **Electrolytes:** added phosphate input and a conditional severe-hypophosphatemia warning; routine phosphate replacement is not recommended.
- **Order consistency:** active management summary now follows the biochemical pathway and avoids contradictory HHS insulin/K+ instructions.
- **Validation:** all HTML JavaScript modules pass syntax validation; DKA/HHS engine test cases pass for DKA, K+ safety gate, HHS, euglycaemic DKA, osmolality and glucose trajectory.

### v1.2 (2026-09-02)
- **DKA/HHS clinical engine:** glucose entry/display standardized to **mg/dL**; effective and total osmolality calculations corrected for mg/dL input.
- **DKA/HHS classification:** deterministic DKA, HHS, mixed DKA/HHS and euglycaemic DKA logic added.
- **Ketones:** explicit urine-ketone fallback plus optional β-hydroxybutyrate input; urine ketones are not used to declare DKA resolution.
- **Safety gates:** potassium-dependent insulin hold, dynamic fluid-tolerance warning, no routine insulin bolus, and no automatic insulin doubling.
- **Resolution/transition:** state-based DKA/HHS resolution panels and patient-specific active management summary added.
- **PWA cache:** service-worker cache bumped to v17 so updated modules are refreshed.

### v1.1 (2026-08-25)
- **Bug fix:** Airway module dark mode CSS selector corrected (`.dark` instead of `dark`)
- **Bug fix:** ECG module now has `<link rel="manifest">` for PWA install support
- **Bug fix:** Consult module removed `user-scalable=no` for better accessibility
- **Improvement:** Diabetes module state saves now debounced (150ms) for better performance
- **Improvement:** Consistent home navigation across all modules

## ⚠️ Disclaimer

These are clinical reference tools — not a substitute for clinical judgment. Always verify doses and protocols against your local institutional guidelines.


## Pass 3 — DKA/HHS trajectory and workflow audit (2 Sep 2026)
- Removed the ambiguous “Observed glucose fall” display from the primary diagnostic banner and replaced it with an optional, explicitly labelled glucose trajectory.
- A calculated glucose change is presented only as an observation, never as a DKA treatment target.
- DKA trajectory interpretation prioritizes acid-base/ketone response; HHS trajectory interpretation incorporates glucose and osmolality safety.
- If prior glucose/time data are absent, the UI reports insufficient trajectory data rather than inventing a rate.
- Formal consultation output uses the same trajectory interpretation.
- JavaScript syntax validation passed after changes.
