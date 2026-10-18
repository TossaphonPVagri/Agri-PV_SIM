# Changelog

## 157.0 — 2026-10-15

### Fixed
- **English mode is complete.** About 120 texts that were still shown in Thai, or only partly translated, now have English: NASA POWER fetch status, unit labels, cross-check and error messages; PV energy progress and Level C / rear-light diagnostics; layout warnings; tooltips and accessibility labels; the hidden crop-light module text; and five texts whose English had lost words (e.g. "NASA POWER monthly", "No (full GHI)").
- Text drawn on images now follows the language: sun-path date labels and layout dimensions in the 3-D view, and the month, time, zone and colour-scale labels of the saved heat-map image.
- The monthly shading CSV (`AgriPV_MonthlyShading_….csv`) is written in English in English mode (headers, labels, month names and the export date).
- Accessibility labels that the code changes later (e.g. the 3-D view controls button) are translated as well as tooltips.
- The Docs "Expand/Collapse" button and the 3-D library loading and error screen follow the language.

### Tested before this release (both editions)
English mode after running every step (fetch, heat map, monthly table, SVF, light raster, exports, sun paths, PV energy at four light-model levels, self-test, economics with sensitivity and scenarios, report, Docs): no Thai text on screen, in tooltips or labels, in the monthly CSV or in the Word report. Switching Thai → English → Thai works. Results unchanged (heat map 36.8 %).

## 156.0 — 2026-10-09

### Added
- **Economics documentation**: a new Docs tab "7. Economics" (Thai and English) with the workflow and equations [E1]–[E14] — lifetime energy, today's money and discounting, costs, replacement and salvage, custom items, hourly load balance and bills (net billing, net metering), NPC/NPV/IRR/ROI/LCOE/COE, crop revenue, debt and tax, sensitivity and scenarios, limitations and the verification result — and references [22]–[26].

### Fixed
- Switching the language now redraws the economics results and charts (they stayed in the previous language until the next calculation).
- On a phone, the economics chart cards fit the screen (they were 380 px wide in a 341 px area).
- The panel type in step 2 (monofacial/bifacial) and the bifaciality φ in step 4 now follow each other: choosing "Bifacial" sets φ to 70 % (edit it from the datasheet) and φ > 0 sets the panel type to bifacial. Before, choosing "Bifacial" in step 2 did not change the energy.
- The monthly shading table CSV is named `AgriPV_MonthlyShading_….csv` (was `AgriPV_Report_….csv`).

### Changed
- README: the verification summary lists the checks against NREL SPA and pvlib, and states that the field data are published measurements, not the author's own.

### Tested before this release (both editions)
Layouts (ground, gable, checkerboard, portrait); heat map, monthly table, SVF; every export (cell CSV, heat-map GeoTIFF, footprint GeoJSON, PNG and 12-month PNG, SF ASC and GeoTIFF, latitude-band CSV, light GeoTIFF, per-module and per-cell CSV, economics CSV); PV energy at all levels, bifacial, datasheet inverter, gable; self-test 1,531 kWh/kWp; economics with load, net metering, debt and tax, custom items, yearly values, scenarios and sensitivity; project save and load with all of these (identical result); Thai and English, dark mode, phone width; Word report with all 16 sections (30 pages, 19 images, none wider than the page) and HTML report. Community edition: all 16 locked buttons produce no file, project files save and load.

## 155.0 — 2026-10-09

### Fixed
- The Scenarios card and the Run card with "Calculate economics" showed on every step: since 151.0 a stray closing tag ended the economics input block early. They now appear only in the Economics step (and are locked in the Community edition). No calculation is changed.

## 154.0 — 2026-10-09

### Changed
- The last internal uses of the old model name are renamed (the generic inverter option value and the part-load function). The name now appears only in the published title of reference [13]. A project file saved with the old option value opens with the generic inverter curve. Results are unchanged.

## 153.0 — 2026-10-09

### Changed
- The name of the former reference model is no longer used in the interface, the documentation, the report or the code. The PV energy equations are unchanged and are credited to their source, Dobos (2014) (reference [13], whose published title is kept). The generic inverter option is now called "generic curve". Results are unchanged (1,421 kWh/kWp with the default layout; self-test 1,531 kWh/kWp).

## 152.0 editions — 2026-10-09

### Changed
- The simulator is built in two editions from the same source (`make_editions.py`). This repository's `index.html` is the **Community edition**: the Economics step, the report builder and all file exports (CSV, PNG, GeoTIFF, ASC, GeoJSON) are removed from the code and shown as a locked preview with a watermark; the economics charts and tables there are a static sample. Saving and loading project files still work. The **Full edition** is distributed separately.

## 152.0 — 2026-10-09

No calculation was changed.

### Added
- **Financial dashboard in the Economics step**: the 3-D view is replaced by a row of key figures (NPV, IRR, LCOE, discounted payback, CAPEX, year-1 energy, and NPV after tax, equity IRR and COE when they apply) and charts: cash flow by cost type (compared with the base case or system only), cumulative discounted cash flow, NPC by component, annual energy, average day of PV and load, monthly bill with and without PV, debt balance and cumulative equity cash flow, NPV tornado, and NPV by scenario (after tax when financing or tax is used). Other steps keep the 3-D view; the tables stay in the results pane below.
- **Net billing and net metering as choices of PV use**: net billing (hourly; surplus paid at the export price), net metering (monthly netting per TOU period), sell all at the feed-in tariff, or zero export, each with a short explanation. Net billing, net metering and zero export ask for a load. Projects saved with the earlier "self-consume + net metering" setting open as net metering.

### Fixed
- The sensitivity inputs are laid out as rows, so each input's name is visible next to its low and high change.

## 151.0 — 2026-10-09

Flexible financial analysis. The shading and energy models are unchanged and the default results are the same as in 150.0.

### Added
- **Custom costs and revenues**: any number of items, each with a name, a type (capital, O&M, replacement, revenue or grant), an amount in THB, THB/kWp, THB/kWh of delivered energy, THB/rai, % CAPEX or THB/tCO₂ avoided, a start and end year (N = last year), a repeat interval (0 = once) and an escalation rate. Examples: insurance, panel cleaning, carbon credit, investment grant, monitoring system, decommissioning. Each item has its own row in the NPC summary.
- **Year-by-year values**: a table to enter, for any year, the feed-in tariff, export price, on-peak and off-peak rates, Ft, crop price, land rent and energy (% of the model). Blank cells use the settings and escalation (shown in grey); columns can be pasted from Excel.
- **Financing and tax** (nominal money): debt share of the year-0 capital, interest, tenor, equal payments or equal principal, cost of equity; corporate income tax with straight-line depreciation, BOI tax holiday and loss carry-forward. Results: project NPV and IRR after tax, equity NPV and IRR, equity payback, minimum and average DSCR, total tax and interest, and a yearly table.
- **Scenarios**: save all inputs of the Economics step under a name, load them back, and compare NPV, annual worth, IRR, payback, LCOE, NPC, NPV after tax and equity IRR on the same energy result, with a chart. Scenarios are saved in the project file.
- **Sensitivity on chosen inputs**: tick the inputs (CAPEX, O&M, energy, electricity prices, discount rate, project lifetime, degradation, land rent, crop price and yield, load, loan interest, debt share, tax rate) and give each its own low and high change.

All of it is in the report and the CSV export. Checked against an independent Python calculation (custom items, yearly overrides, 2 % inflation, 70 % debt, 20 % tax with a 3-year holiday): NPV, IRR, LCOE, after-tax NPV and IRR, equity NPV and IRR, DSCR, tax and interest agree to within 6 THB of input rounding.

## 150.0 — 2026-10-09

### Changed
- **Lifetimes are free inputs from 1 to 100 years**: project lifetime, PV lifetime and inverter lifetime (were capped at 50 and 60 years). A value with decimals is rounded to whole years in the box, so the box shows what is calculated.
- **Schedule shown under the inputs**: the years in which the PV and the inverter are replaced and the remaining life credited as salvage at the end of the project, updated while typing.

### Fixed
- After a PV replacement within the project, the energy now restarts with new modules (first-year and annual degradation counted from the new installation). It used to keep degrading from year 1. With the defaults (25-year project and PV) nothing changes.

## 149.0 — 2026-10-09

Financial analysis to the level of HOMER Pro's economics. The shading and energy models are unchanged.

### Added
- **Real and nominal money**: nominal discount rate and inflation give the real discount rate i = (i′ − f)/(1 + f); prices are in today's money with real escalation (separately for sale prices and purchase prices). IRR is shown real and nominal.
- **Components with lifetimes**: PV (lifetime, replacement cost) and inverter (lifetime, replacement cost) are replaced every lifetime within the project, and the last unit's remaining life is credited as salvage at the end (straight line). Other capital (grid connection, permits) and fixed O&M were added.
- **Base case and comparison** (HOMER "compare economics"): the base case buys all electricity from the grid and can also farm the same area in the open field. Results: NPC of the system and of the base case, present worth (NPV), annual worth, IRR, ROI, simple and discounted payback, operating cost, LCOE of the PV and COE (cost of electricity served, with PV and grid only), and CO₂ avoided (grid emission factor, TGO 2022 data by default).
- **Cost summary**: NPC by component (PV, inverter, other, land, grid, crop) and cost type (capital, replacement, O&M, electricity, crop, salvage), with annualised values.
- **Grid**: rate schedule presets (PEA small general service TOU, and PEA TOU with demand charge, below 22 kV), demand charge on the monthly on-peak peak, service charge, export price, and net billing (hourly) or net metering (monthly, per TOU period). A monthly bill table shows purchases, sales, peak demand, energy and demand charges, sales credit, and the bill with and without PV.
- **Sensitivity**: one input at a time by ± a chosen percentage (CAPEX, O&M, energy yield, electricity prices, discount rate, crop price, load); tornado chart of NPV and a table with NPV, IRR and LCOE.
- **Charts**: cash flow by cost type (system only, or compared with the base case), annual energy, cumulative discounted cash flow, average-day PV and load, tornado. All are in the report; the CSV export has every yearly column and the sensitivity table.

### Changed
- The inverter is now replaced every lifetime (12 and 24 years with the defaults) with salvage at the end, instead of once. With the defaults this changes NPV by about −500 THB.
- Negative numbers use the minus sign U+2212 so Word does not break them across lines.

Checked against an independent Python calculation for two cases (no load; load with demand charge, 2 % inflation, escalation, fixed O&M and other capital): NPV, annual worth, IRR (real and nominal), ROI, LCOE, COE, NPC and salvage agree to within 5 THB of input rounding.

## 148.0 — 2026-10-08

### Added
- **Load and self-consumption** in the Economics step. The load is either a 24-hour profile (presets: daytime pumping, greenhouse fans and cooling, cold storage, household, flat, or custom; daily kWh, weekend factor and 12 monthly factors) or an hourly CSV of 8,760 values in kW (a template can be downloaded; 8,784 values from a leap year are accepted).
- **How the PV electricity is used**: sell all at the tariff (the load figures are for reference), self-consume and export the surplus at an export price, or self-consume with zero export (the surplus is curtailed and LCOE uses the self-consumed energy).
- **TOU energy rates**: on-peak Mon–Fri 09:00–22:00 and off-peak, plus Ft. The defaults are the PEA small general service TOU rates below 22 kV and Ft for Sep–Dec 2026. VAT, the service charge, the demand charge and public holidays are not included.
- **Results**: self-consumption and self-sufficiency, exported or curtailed energy, grid import, the energy bill with and without PV, a monthly table, and an average-day chart of PV and load (by month or the annual average) with hover values. The report section and the CSV export include them.

### Changed
- Both PV engines also record the AC energy in each clock hour for each NASA day type. The monthly and annual results are unchanged (1,421 kWh/kWp with the default layout).
- Report charts for economics are drawn at a size where the text stays readable on the page, and the tables no longer show "-0".

## 147.0 — 2026-10-08

### Added
- **Economics step** (new tab 5): year-by-year energy over the project life with first-year and annual degradation (P50 and P90 from an uncertainty σ); CAPEX from THB/Wp × a structure multiplier (ground 1.00, vertical 1.20, elevated 1.35, or custom), OPEX with escalation, inverter replacement, land rent, tariff with escalation, discount rate; optional crop revenue from the cultivated zones (lettuce quadratic Yrel from the PAR-weighted RSR of the monthly shading table, zone SVF and NASA POWER). Results: NPV, IRR, LCOE, simple and discounted payback, lifetime energy, two charts with hover values, a year-by-year table and CSV export. Defaults follow the financial parameter set of the nationwide study (CAPEX 18.85 THB/Wp, OPEX 2.79 %/yr, FiT 2.1679 THB/kWh, r 6.4 %, 25 years).
- Report section **Lifetime & Economics** (key results, charts, table, method and assumptions).

The shading and energy models are unchanged; NPV, IRR and LCOE were checked against an independent calculation (identical to the reported digits).

## 146.0 — 2026-10-08

Report builder. No calculation was changed.

### Added
- **PV Energy section** in the report: key results (annual energy, specific yield, PR, bifacial PR, front and rear irradiation), a monthly table, the settings used (irradiance-model level, module, transposition, day model, losses, inverter and its losses), and a warning when the layout changed after the energy run. The executive summary includes the annual energy.

### Changed
- **Images fit the page**: each capture is measured and given width/height, so Word and print keep it inside an A4 page; the 12-month maps form a 3 × 4 table on one page.
- **Survey-sheet look**: cover title block (project, location, system, date, tool version), ink rules, IBM Plex type, print page breaks; Word output on a plain white page.
- **Content**: report title "Agrivoltaic System Assessment"; assumptions and limitations rewritten for crop light, PV energy and the verification results; the monthly shading table is built from the data (no duplicated bilingual headers).

## 145.0 — 2026-10-08

Remaining fixes from the function audit. No change to the shading or energy model (self-test 1,531 kWh/kWp).

### Fixed
- **Pitch shorter than the row depth** (for example after switching to portrait): the rows used to overlap silently and GCR came from the stale pitch. The pitch is now raised to the row's ground depth (rows touching), a warning explains it under Row Spacing, and GCR follows the real pitch.
- **NASA POWER regional fetch** failed with HTTP 422 when the area, or the last tile of a split, was narrower than 2°. Requests are widened to 2° and points whose 1° cell lies outside the chosen area are dropped.
- **Report file name** no longer reads "AgriPV_Report_Report_…" when no project name is set.
- **English**: the inverter card (DC/AC warning, summary, string-design table), "kWh/m²/yr" and "kWh/yr" units and the greenhouse row labels are translated; phrases now also match at the edges of a text node.

## 144.0 — 2026-10-08

GIS raster exports on the NASA POWER grid. The shading model is unchanged (self-test 1,531 kWh/kWp).

### Changed
- **Default raster grid = NASA POWER 1° grid** (97–106°E, 5–21°N, cell centres at x.5°), the same grid as the radiation data used for crop light. The GHI 9 arc-sec and PVOUT 30 arc-sec grids can still be chosen.
- **Latitude-band shading runs in the background** with a progress line; the page stays responsive (longest pause under 1 s) and results are cached, so a second export with the same settings is instant.

### Fixed
- Monthly SF GeoTIFF and ASC exports were always refused with the default grid (23 million cells); with the NASA grid they produce 9 × 16 cells in about 15 s.
- The light-availability GeoTIFF computed shading at every 0.1° band for all 12 months (about 30 minutes with the page frozen); it now computes only the NASA point latitudes for the selected month (about 17 s, instant when cached).
- English mode: text whose bracket holds Thai, such as "(per-cell เรขาคณิต)" or "(ไม่มีวัน zenith)", was cut to a single word.
- The latitude-band CSV file name now states the grid cell size instead of always "GHIgrid".

## 143.0 — 2026-10-08

Appearance and one display fix; no calculation was changed (self-test 1,531 kWh/kWp, ray tracer 99.3%, as before).

### Fixed
- **Sun Position tile** now shows the altitude and azimuth live as the month and time change (it stayed at 0° since version 102). Azimuth is shown as a bearing from north (90° = east).

### Changed
- **"Survey sheet" design**: drafting paper with a grid, ink rules, square corners, a title block with the sheet number of the active step, and the steps as a sheet index. IBM Plex Sans Thai for text and IBM Plex Mono for numbers.
- **Paper is the default**; the dark option is now a drafting board instead of the slate theme.
- Inline colours follow the theme, emoji are removed from the interface, and the 3-D view background matches the paper.
- The dark drafting board is kept quiet: mid-grey rules, unframed buttons, no page grid, and a lighter ground grid in the 3-D view (default opacity 0.5).

## 142.0 — 2026-10-08

- No institutional affiliation is shown: this is a personal project of the author. Footer, README and CITATION.cff updated. No other change.

## 141.0 — 2026-10-08

Language only; no calculation was changed.

### Added
- **English documentation**: the seven model-documentation tabs, the zone definitions and the equation summary are written out in English and switch with the language setting.
- **English reports**: in English mode the Word/HTML report is produced in English, with English dates.

### Changed
- Long sentences that have no English text are no longer cut into fragments in English mode.
- The Thai documentation no longer refers to equations "above" (they now sit in the Docs drawer).

## 140.0 — 2026-10-08

- Author affiliation updated to SGtech (School of Renewable Energy and Smart Grid Technology), Naresuan University. No other change.

## 139.0 — 2026-10-08

Interface only; no calculation was changed.

### Changed
- **Workflow tabs**: Site & Climate → Layout → Shading & Crop Light → PV Energy → Report. The 3-D view stays visible; the side panel and the results area show the active step.
- **Shorter header**: name and version only; the author credit moved to the footer. One KPI strip replaces the two rows of statistics.
- **Heat-map controls** moved off the 3-D view into the Shading & Crop Light step.
- **Docs drawer**: model documentation, zone definitions and the equation summary open from the header instead of filling the end of the page.
- **English by default** (Thai + English selectable). Tooltips, status lines, result tables and pop-up messages are translated as well; the compass shows N/S/E/W.

### Removed
- The "planned" Crop Light card (crop light is calculated in the Shading & Crop Light step).

## 138.0 — 2026-10-07 (first public release)

### Fixed
- **Rear-side beam irradiance in the climatology engine** (bifacial levels A, B, B+ and C). It was always zero: the front angle-of-incidence cosine was clamped to ≥ 0 before the rear term used its negative. Effect on vertical east–west bifacial arrays at level B+: specific yield from 1,060 to 1,303 kWh/kWp, now consistent with the per-module level D (1,284) and PVsyst (1,247). Tilted south-facing rows are barely affected. Level D (every module) was already correct.
- **Default module rating** changed from 550 to 600 Wp, consistent with the default module size (2,382 × 1,134 mm). The installed capacity, and therefore the total kWh, follows this value.

### Added
- **Bifacial performance ratio** shown next to the front-only PR: E_AC / (H_POA,front + φ · H_POA,rear), as in PVsyst. The front-only PR can exceed 100% for vertical bifacial arrays.

## Earlier development (summary)
- 137 — inverter from datasheet values (two-parameter efficiency fit), five clearness day types per month.
- 136 — front and rear irradiance ray-traced for every module (level D) with a dedicated plate ray tracer.
- 135 — ground light resolved per cell for the rear-side view factors (level C).
- 134 — built-in model documentation window.
- 133 — ground light availability and rear-beam blocking in the bifacial model; gable roofs split by side.
- 128–132 — electricity module based on Dobos (2014), front/rear irradiance, per-zone albedo.
- 126–127 — gaps between modules; every module built individually (no merged slabs).
- 114–122 — per-cell geometric sky-view factor; PVsyst GCR definition; equation references.
- 116 — Three.js bundled inline (works offline).
