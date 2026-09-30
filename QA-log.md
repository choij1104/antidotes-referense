# Antidote Reference — Verification & Debug Log

**File:** index.html (115 entries, 18 categories)
**Author:** HAKOYA LLC
**Date closed:** 2 August 2026
**Total checks:** 75 (26 source verifications, 49 automated code and consistency tests)
**Corrections applied:** 11

---

## 1. Source verification against FDA labeling and primary literature

Twenty-six numeric or regulatory claims were checked against the FDA label, the manufacturer's
prescribing information, or the governing guideline. Every dose in the file that could cause harm
if wrong was checked; none were accepted from memory.

| # | Claim checked | Source | Result |
|---|---|---|---|
| 1 | Hydroxocobalamin is first-line for cyanide; nitrite is not | FDA 2006 approval, AHA 2023 | Confirmed |
| 2 | Andexanet ANNEXA-I thrombotic rate ~10%; heparin resistance | NEJM 2024, ATVB 2025 | Confirmed |
| 3 | Bentracimab regulatory status | SERB/SFJ BLA, ACC.25 | Not approved — marked tier D |
| 4 | Nalmefene nasal 2.7 mg, FDA May 2023, age >=12 | Opvee label | Confirmed |
| 5 | Physostigmine US manufacturing ceased (Akorn 2023) | FDA importation notice | Confirmed |
| 6 | Rivastigmine alternative dosing | Am J Emerg Med 2025; Regul Toxicol Pharmacol 2025 | Confirmed |
| 7 | Digibind discontinued in US; DigiFab only product | AHFS monograph, FDA label | Confirmed |
| 8 | Flumazenil not recommended routinely | AHA guidelines, 2016 meta-analysis | Confirmed |
| 9 | Massive APAP: fomepizole + HD adjuncts | Clin Toxicol 2023 case series | Confirmed, kept tier C |
| 10 | Glucarpidase 50 U/kg; leucovorin is a substrate | Voraxaze FDA label | Confirmed |
| 11 | Uridine triacetate 10 g q6h x20; 96-hour window | Vistogard FDA label | Confirmed |
| 12 | Radiation MCMs incl. romiplostim (Jan 2021) | FDA MCM page, ORISE REAC/TS | Confirmed |
| 13 | CroFab vs Anavip loading and maintenance | Package inserts; J Med Toxicol 2023 | Confirmed |
| 14 | Idarucizumab 5 g as 2 x 2.5 g | Praxbind FDA label | Confirmed |
| 15 | ASRA 2020 lipid emulsion volumes | ASRA LAST checklist | Confirmed |
| 16 | Methylene blue G6PD contraindication; 7 mg/kg ceiling | ProvayBlue label | Confirmed |
| 17 | BAT heptavalent via CDC EOC; BabyBIG via CA program | FDA label, CDC formulary | Confirmed |
| 18 | Nerve agent autoinjector 2.1 mg / 600 mg | DuoDote/ATNAA label | Confirmed |
| 19 | HIET 1 U/kg bolus then 1-10 U/kg/h | Am J Ther 2025; LITFL | Confirmed |
| 20 | Amatoxin: no FDA-approved therapy; silibinin investigational | MMWR May 2026 | Confirmed |
| 21 | Lead chelation sequence BAL before EDTA | AAP; Medscape guidelines | Confirmed |
| 22 | Octreotide 50-100 ug q6h for sulfonylurea | J Med Toxicol; Ann Emerg Med | Confirmed |
| 23 | DigiFab vial formula (level x kg) / 100 | DigiFab FDA label | Confirmed, entry refined |
| 24 | Andexanet 400/480 and 800/960 mg regimens | Andexxa FDA label | Confirmed, selection rule added |
| 25 | Sugammadex 2 / 4 / 16 mg/kg; 7-day contraceptive warning | Bridion FDA label | Confirmed, qualifier added |
| 26 | KI 130 / 65 / 32 / 16 mg by age | FDA KI guidance | Confirmed, ladder corrected |
| 27 | Anascorp 3 vials; BabyBIG 50 mg/kg | FDA labels | Confirmed, administration detail added |
| 28 | Dexrazoxane 1000/1000/500 mg/m2 within 6 h | Totect FDA label | Confirmed, caps added |
| 29 | Deferoxamine 15 mg/kg/h; ARDS beyond 24 h | Desferal label; INCHEM | Confirmed, 6 g ceiling added |
| 30 | Pralidoxime 30 mg/kg then 8-10 mg/kg/h | WHO regimen; Goldfrank's | Confirmed, caps added |
| 31 | Prussian blue 3 g TID adult, 1 g TID paediatric | Radiogardase FDA label | Confirmed, paediatric added |

## 2. Corrections applied

1. DigiFab — staged 10 + 10 vial dosing per label; paediatric <20 kg vial note added.
2. Sugammadex — 16 mg/kg indication qualified to a single 1.2 mg/kg rocuronium dose.
3. Potassium iodide — full FDA age ladder (130 / 65 / 32 / 16 mg) and the >=70 kg adolescent rule.
4. Dexrazoxane — maximum daily doses (2000 / 2000 / 1000 mg) and 50% reduction if CrCl <40 mL/min.
5. Deferoxamine — label ceiling of 6 g/24 h stated, with the note that practice commonly exceeds it.
6. Pralidoxime — 2 g loading cap and 650 mg/h infusion cap added.
7. Anascorp — dilution to 50 mL, 10-minute infusion, 60-minute post-infusion monitoring.
8. BabyBIG — infusion rate (0.5 then 1.0 mL/kg/h) and dedicated-line requirement.
9. Prussian blue (thallium) — paediatric 1 g TID and expected 30-day course.
10. Andexanet — explicit low-dose vs high-dose selection rule, including the unknown-timing default.
11. Dapsone methemoglobinemia — G6PD status check added before methylene blue.

## 3. Automated test results

All 49 automated checks pass. Coverage:

- **Structure and syntax (10):** JS parses, schema complete on all 115 entries, valid tier values,
  no duplicate toxins or toxin/antidote pairs, balanced tags, no template-literal breakers.
- **Offline integrity (5):** no external src or href, no fetch or XHR, no localStorage or
  sessionStorage, no companion assets, complete standalone document.
- **Security and escaping (4):** esc() covers & < > and quotes; the 26 entries using > or < as
  clinical thresholds are escaped at render; no tag-like sequences anywhere in the data.
- **Accessibility and presentation (6):** lang attribute, charset, viewport, visible focus styles,
  aria-pressed on filters, aria-label on search, print stylesheet, reduced-motion respected.
- **Medication-error prevention (4):** unit symbols consistent (ug throughout, no mcg), no naked
  decimals such as .5 mg, trailing-zero instances reviewed and confirmed to be pH values, FiO2, and
  serum levels rather than doses, weight-based dosing present on every paediatric-specific entry.
- **Search behaviour (3):** 18 trade names findable (Cyanokit, DigiFab, Praxbind, Andexxa, Voraxaze,
  Vistogard, Radiogardase, Anascorp, CroFab, Anavip, BabyBIG, Totect, Bridion, Opvee, Pedmark,
  Ryanodex, DuoDote, Nithiodote); nonsense queries return zero; render markup balanced across all
  115 cards.
- **Clinical consistency (10):** G6PD caution on all four methylene-blue entries, cyanide entries
  agree internally, physostigmine supply status noted, flumazenil never framed as routine, BAL
  contraindication in methylmercury captured, Digibind discontinuation flagged, all investigational
  agents held at tier D, tier-N entries never imply an antidote exists.
- **Policy compliance (4):** copyright and credentials intact, prohibited affiliation terms absent,
  disclaimer language intact, no debug artefacts left in production.

## 4. Known limitations

- Doses are adult unless stated. Paediatric weight-based dosing is given only where it differs
  materially from the adult approach.
- Regulatory status is current as of 2 August 2026. Bentracimab, IV silibinin, and cobinamide were
  in motion at the time of writing and are labelled accordingly.
- Extracorporeal indications follow EXTRIP but individual thresholds vary by workgroup revision.
- This is decision support, not a protocol. Institutional formulary confirmation is required before
  administration, and a regional poison centre remains the authority in any live case.
