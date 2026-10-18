# Agri-PV Geometric Simulator

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23450984.svg)](https://doi.org/10.5281/zenodo.23450984)

A single-file, browser-based simulator for **agrivoltaic (Agri-PV) systems**. One three-dimensional model of the array, in which every module is a separate plate, drives the ground shading, the light available to crops and the front/rear irradiance and electricity yield of every module.

**Run it online:** https://tossaphonpvagri.github.io/Agri-PV_SIM/
**Run it offline:** download `index.html` and open it in a modern browser (Chrome, Edge, Firefox). No installation is needed; Three.js r128 is bundled in the file. Only the NASA POWER climate download needs an internet connection, and a manual-paste option is provided.

> Research software. Results are model estimates; check them against site data before using them for design guarantees.

**Editions.** This repository holds the **Community edition**. It contains the full geometry, shading, crop-light and PV-energy models. The Economics step will be available in a future update, and a **Full edition** will be released in the future.

---

## Using it

The page follows the order of a study, one tab per step. The 3-D view stays on screen throughout, and the side panel and results area change with the tab:

1. **Site & Climate** — coordinates, then monthly NASA POWER climatology.
2. **Layout** — system type, module size and count, pitch, tilt, height and the advanced modes.
3. **Shading & Crop Light** — ground heat map, monthly zone tables, sky-view factor, DLI and GIS rasters.
4. **PV Energy** — module and inverter datasheet values, front/rear irradiance and annual yield.
5. **Economics** (future update) — year-by-year energy with degradation (P50/P90); components with lifetimes, replacement and salvage; real discount rate from inflation; an optional load (24-hour profile or 8,760-value hourly CSV) with TOU, demand charge, net billing or net metering; comparison with a grid-only base case: NPC by component and cost type, NPV, annual worth, IRR, ROI, payback, LCOE and COE, CO₂ avoided, monthly bills and a sensitivity tornado on chosen inputs; custom cost and revenue items, year-by-year values, debt and corporate tax (equity IRR, DSCR), and saved scenarios compared side by side.
6. **Report** (future update) — Word/HTML report built from the latest results.

The interface, the documentation and the generated reports are in English by default; Thai + English can be selected at the top. The **Docs** button opens the model documentation and equations.

## Features

**Geometry**
- Ground-mounted rows, elevated (overhead) rows, vertical bifacial fences and gable roofs, in solid or checkerboard module patterns.
- Module size and gaps, tables, rows, columns, pitch, tilt, azimuth and height are all user-defined.
- Every module is built individually, so gaps between modules always transmit light.

**Ground shading and crop light**
- Beam shading of every ground cell on a 0.25–1 m grid, computed either by centre ray cast or by exact polygon-union area (Sutherland–Hodgman clipping and slab decomposition).
- Time steps are weighted by Haurwitz clear-sky irradiance.
- Per-cell sky-view factor from cosine-weighted hemisphere sampling (6 × 24 rays).
- Agronomic zones: under the modules, between rows, between columns, and the openings of checkerboard layouts.
- Reduction in solar radiation (RSR) and daily light integral (DLI) per zone and month, from NASA POWER climatology and the Erbs diffuse fraction.

**Electricity**
- PV performance chain based on Dobos (2014): Hay–Davies transposition, Fresnel incidence-angle modifier, NOCT cell temperature, part-load inverter efficiency and clipping.
- Inverter can be set from datasheet values.
- Five day types per month (clear to overcast).
- Bifacial rear irradiance at several levels of detail, up to front and rear irradiance ray-traced for **every module**.

**Outputs**
- Shading and SVF heat maps, per-zone tables, per-module maps.
- CSV and GeoTIFF exports, GeoJSON footprints.
- Report builder (Word / HTML).
- Built-in model documentation of every equation, in English and Thai.

## Verification summary

The model is **verified** against analytical and independent software references and compared with published field data; it has not yet been validated with the author's own field measurements.

| Check | Result |
|---|---|
| Sun position vs NREL SPA (solar elevation 5–85°) | RMSE 0.14° (altitude), 0.42° (azimuth) |
| Instantaneous ground shading fraction vs pvlib infinite sheds | RMSE 0.30–0.61 percentage points (≤ 0.21 with the module thickness in the 2-D reference); monthly weighted values within 0.05 points |
| Front irradiance vs PVsyst 8.1 (4 layouts, 998 kWp, Phitsanulok, Thailand) | within +0.6 to +2.3% |
| Specific yield vs PVsyst, same loss assumptions | +1.7 to +3.0% (bifacial rear: 3-D finite array vs PVsyst 2-D infinite sheds) |
| Ground light vs PVsyst "global incident on ground" | RSR within ~1.3 points |
| Published field measurement, lettuce under a 10 kWp array, Chiang Mai (Wicharuck et al., *Sci. Rep.* 15, 39755, 2025) | light reduction 50.1–50.4% simulated vs 49–50% reported |
| Built-in ray tracer vs Three.js ray caster | 99.3% agreement on 600 random rays |

## Limitations

- Weather comes from monthly climatology (NASA POWER), represented by day types. Single years and hourly time series are not simulated.
- Only modules cast shade. Posts, frames, cladding and terrain are not modelled.
- Electrical mismatch under partial shading is not modelled. DC output is linear in the unshaded fraction.
- The crop-light sky model is isotropic, and light reflected onto the crop is not included.

## How to cite

If you use this software, please cite it (see `CITATION.cff`):

> Sa-ard, T. (2026). *Agri-PV Geometric Simulator* (version 158.0) [Computer software]. Zenodo. https://doi.org/10.5281/zenodo.23450984

## AI assistance

Parts of the code, the interface and the documentation were written with the help of an AI coding assistant (Anthropic Claude). The model design, the choice of methods and parameters, the verification against NREL SPA, pvlib and PVsyst, and the comparison with published field measurements were done by the author, who reviewed the code and is responsible for the results.

## License

Community edition: MIT License, © 2026 Tossaphon Sa-ard (see `LICENSE`). The Full edition, planned for a future release, will be distributed under its own terms. Bundled third-party code: [three.js](https://threejs.org) r128 and OrbitControls, MIT License, © 2010–2021 three.js authors (the notice is kept inside `index.html`). The DC, cell-temperature and inverter equations follow Dobos (2014), NREL/TP-6A20-62641; this is an independent implementation and is not NREL software.

---

## ภาษาไทย

**Agri-PV Geometric Simulator** เป็นเครื่องมือจำลองระบบเกษตรร่วมกับโซลาร์เซลล์ (Agri-PV) ที่ทำงานในเว็บเบราว์เซอร์ทั้งหมดในไฟล์เดียว เครื่องมือสร้างแบบจำลอง 3 มิติของแผงทุกแผง แล้วใช้คำนวณ:
- ร่มเงาบนพื้นรายเซลล์
- แสงที่พืชได้รับ (RSR, DLI)
- แสงหน้าและหลังแผงของทุกแผง
- พลังงานไฟฟ้า

**วิธีใช้**
- **ออนไลน์:** เปิดลิงก์ GitHub Pages ด้านบน
- **ออฟไลน์:** ดาวน์โหลด `index.html` แล้วเปิดในเบราว์เซอร์ ไม่ต้องติดตั้งโปรแกรม ต้องใช้อินเทอร์เน็ตเฉพาะตอนดึงข้อมูลภูมิอากาศจาก NASA POWER และมีช่องให้วางข้อมูลเองได้

**รุ่นของเครื่องมือ:** repository นี้เป็นรุ่นทั่วไป (Community edition) มีแบบจำลองเรขาคณิต ร่มเงา แสงพืช และพลังงานไฟฟ้าครบ ขั้นเศรษฐศาสตร์จะเปิดให้ใช้ในการอัปเดตครั้งต่อไป และรุ่นเต็ม (Full edition) จะเผยแพร่ในอนาคต

**ข้อควรทราบ:** เป็นซอฟต์แวร์เพื่องานวิจัย ผลที่ได้เป็นค่าประมาณจากแบบจำลอง ควรตรวจสอบกับข้อมูลจริงของพื้นที่ก่อนใช้ในการออกแบบเชิงพาณิชย์

**การใช้ AI:** โค้ด หน้าจอ และคู่มือบางส่วนเขียนโดยใช้ AI ช่วย (Anthropic Claude) ส่วนการออกแบบแบบจำลอง การเลือกวิธีและค่าพารามิเตอร์ การตรวจสอบเทียบ NREL SPA, pvlib และ PVsyst และการเทียบกับผลวัดภาคสนามที่ตีพิมพ์แล้ว ทำโดยผู้พัฒนา ซึ่งตรวจทานโค้ดและรับผิดชอบต่อผลลัพธ์

**การอ้างอิงและสัญญาอนุญาต:** ดูส่วน *How to cite* และ *License* ด้านบน (MIT License)

**ผู้พัฒนา:** ทศพร สะอาด (Tossaphon Sa-ard)
