# Mosca Hand Threshold Evaluator — Educational Edition

**Live:** https://darrenbender.com/mosca-hand-threshold/
**© 2026 ProteQC Limited. All rights reserved.**

The interactive companion to the law-review article *Post-Quantum Negligence*.
It implements the **Mosca Hand Threshold Form: R < P(W)** — the Learned Hand
Formula (*United States v. Carroll Towing Co.*, 159 F.2d 169 (2d Cir. 1947))
rearranged to threshold form (R = B/L), with the probability read as **P(W)**:
the mass of the CRQC-arrival distribution (from the Quantum Threat Timeline
Reports) falling inside the organization's vulnerability window
W = [today, migration-start + Y + X]. D (*cryptographic procrastination*, per
the Mosca-Gómez formulation) slides W's right edge daily until migration
commences. The tool renders the exposure area, computes the crossing date t*,
the procrastination premium, and produces a timestamped documentation block.

The thesis of the article — and of this tool — is **documented contemporaneous
analysis**: survey-data changes land here as data commits, so the repository
history is itself a record of what the best evidence said, and when.

## Structure

```
mosca-hand-threshold/
├── index.html            The evaluator (all logic and styling; no build step)
├── data/
│   ├── manifest.json     Lists the dataset files the loader fetches
│   ├── qttr-2026.json    QTTR (Mar 2026) — current default
│   ├── qttr-2024.json    QTTR 2024
│   └── mosca-2015.json   Mosca 2015 historical point estimates
├── fonts/                Self-hosted DM Sans + JetBrains Mono (variable, latin)
├── ProteQC_logo.png      ProteQC® registered-mark logo
├── favicon-*.png         Lotus mark favicons
└── og-image.png          Social preview card (1200×630)
```

## Updating for a new report cycle (data commit, no code change)

1. Copy an existing `data/qttr-*.json` as the template for the new year.
2. Fill in `key` (sort-descending picks the default report — use the year),
   `label`, `sub`, `published` (ISO date; anchors all elapsed-time math),
   and `anchors`: `{ "yearsFromPublication": [optimistic%, pessimistic%] }`,
   computed from the report's Appendix A.4 raw bin counts using the report's
   own cumulative assignments (EU 1/0, VU 5/1, U 30/5, N 70/30, L 95/70,
   VL 99/95, EL 100/99 %). Include `"0": [0, 0]`. Record the raw counts in
   `rawBins` and describe the computation in `provenance`.
3. Add the filename to `data/manifest.json`.
4. Commit the two files together as a data commit, e.g.
   `data: add QTTR 2027 (n=NN, published YYYY-MM-DD)`.

The report selector, default-report choice, and awareness presets in the UI
build from these files at load; no other edits are required. Prior curves stay
selectable as history-on-demand.

**Do not recompute or "correct" published anchor values in place** — a
correction is itself a data commit with its reasoning in the message.

## Verifying locally

Serve over HTTP (the data loader uses `fetch`, which `file://` blocks):

```sh
python3 -m http.server 8734 --directory ..   # then open localhost:8734/mosca-hand-threshold/
```

Regenerate the OG card after visual changes (headless Chrome):

```sh
chrome --headless=new --screenshot=og-raw.png --window-size=1200,900 \
  --hide-scrollbars --virtual-time-budget=6000 <local URL>
# crop to 1200×630 from y=30
```

## License & contact

Free use permitted for educational and academic purposes, research and
non-commercial analysis, personal risk assessment, and sharing with proper
attribution ("Developed by ProteQC Limited (ProteQC.com)"). Permission
required for commercial use, paid services, white-labeling, or removal of
attribution. Provided "AS IS", no warranty; educational framework, not legal
advice.

- Commercial licensing: licensing@ProteQC.com
- Enterprise advisory: advisory@proteqc.com
- https://ProteQC.com
