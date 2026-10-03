# Component sheet versus 3D models

Authority: [Google Sheets — Hardware BOM](https://docs.google.com/spreadsheets/d/1QLaJ-uK42XSZoBPESpl_FkiHE4a3wLdfT5JuzkQpVLM/edit?gid=0#gid=0). Local transcription: [hardware-bom.md](hardware-bom.md).

Audit date: 2026-10-03 (Asia/Manila). Model revision: `10806ec`. All 32 BOM rows were checked against the default component definitions and geometry builders in `index.html`. The freshly retrieved sheet values match the local snapshot.

The sheet governs component selection. This audit marks differences without changing model geometry or wiring. Exact supplier dimensions, RF behavior, electrical operation and enclosure ratings were not verified; a MATCH marker means the component family and stated purpose are represented.

## Model differences

| Sheet row | Mark | Sheet component / requirement | Current model difference | Evidence |
| --- | --- | --- | --- | --- |
| 9 | DIFFERENT | ADXL345 GY-291 accelerometer | SW-420 / LM393 vibration module, with sensitivity trimmer and three-pin header. | [index.html:262](../index.html#L262) |
| 11 | DIFFERENT | IFR18650 3.2 V 1500 mAh cell | Two cells in 1S2P, 3.2 V / 3000 mAh. The sheet has no explicit pack quantity/topology; do not infer that it authorizes the two-cell pack or that it explicitly orders one cell per node. | [index.html:276](../index.html#L276) |
| 12 | DIFFERENT | TP5000 charger set to 3.6 V | BQ25185 power-path board labeled 3.65 V, with IN / SYS / BAT connections; both component identity and charge-voltage label differ. | [index.html:285](../index.html#L285) |
| 14 | MISSING | 5 V wall adapter | Only a cable gland and incoming adapter lead are modeled; no adapter body. | [index.html:296](../index.html#L296) |
| 15 | PARTIAL | Flame-retardant ABS IP65 enclosure | ABS enclosure and IP65 intent are described, but flame-retardant material is not specified. Geometry cannot establish ingress protection or fire performance. | [index.html:202](../index.html#L202) |
| 17 | PARTIAL | 1/4 W 1% resistors; LED resistors and battery-voltage divider | SMD LED resistors appear on the unlisted MCP23017 board. The specified resistor format/tolerance and battery-voltage divider are not explicitly represented. | [index.html:302](../index.html#L302) |
| 18 | MISSING | Electrolytic supply capacitors near survivor ESP32 and radio | No identified electrolytic components in the survivor assembly. The LM2596 capacitors belong to the relay and do not fulfill this survivor-node row. | [index.html:242](../index.html#L242) |
| 19, 29, 35 | PARTIAL | DS3231 AT24C32 RTC module on each node | Each model includes a DS3231 IC and backup-cell holder, but the shared RTC builder has no AT24C32 EEPROM. All three RTC modules are incomplete representations of the named breakout. | [index.html:173](../index.html#L173) |
| 23 | FIT DIFFERENCE | 3 m low-loss N-male-to-SMA coax | The coax control points drop from y=14.4 to y=−7.3: 21.7 display units / 7 units per metre ≈ 3.10 m vertically, before bends. Labels match the BOM; the conceptual route is longer than the stated cable. | [index.html:333](../index.html#L333) |
| 36 | PARTIAL | Wires and assembly consumables | Representative wires and cable ties exist, but M-M/F-F/M-F connector variants and all consumables are not individually represented. Process supplies need not be mistaken for installed electronic modules. | [index.html:293](../index.html#L293) |

## Modeled additions without a BOM line

| Node | Mark | Addition | Evidence |
| --- | --- | --- | --- |
| Survivor | **EXTRA** | MCP23017 I/O expander and associated interrupt/button/LED wiring. | [index.html:303](../index.html#L303) |
| Survivor | **EXTRA** | 3.3 V buck-boost regulator; model sources point to TPS63070. | [index.html:312](../index.html#L312) |
| Survivor | **EXTRA** | Separate 3.3 V power-distribution board. Wiring itself is covered by row 36; this board is not listed. | [index.html:308](../index.html#L308) |
| Survivor | **EXTRA** | Common transparent hinged cover over all three buttons. The individual TRAPPED guard is consistent with row 8. | [index.html:225](../index.html#L225) |
| Relay | **EXTRA** | 12 V input fuse shown inside the junction-box assembly. | [index.html:350](../index.html#L350) |

Wall mounting plate/anchors, gaskets, screw bosses, standoffs, battery straps, console buzzer-driver detail and the steel plate beneath the magnetic base are additional construction details without individually selected BOM SKUs. They are not proof of a different controller/radio/buzzer; their exact purchased implementation remains unspecified.

## Inconsistencies inside the authoritative sheet

| Location | Mark | Sheet discrepancy | Model treatment |
| --- | --- | --- | --- |
| BOM row 22 | **SHEET CONFLICT** | Component name specifies 5.8 dBi, while cost/listing note says 8 dBi. | Model follows the 5.8 dBi BOM name. Do not silently substitute 8 dBi. |
| BOM row 32 | **SHEET CONFLICT** | Component name specifies a 3 dBi magnetic-mount whip, but cost note says a spare 2 dBi whip from row 7. That note does not establish a magnetic base. | Model follows the named 3 dBi magnetic-mount requirement. |
| Candidate row 8 (K:Q) versus BOM row 24 (B:I) | **CANDIDATE DOES NOT MEET BOM** | The Ambitful candidate reaches 3.2 m; the authoritative BOM calls for a 4 m tripod. Candidates are explicitly not in the BOM yet. | The 4 m model follows the BOM. Keep the 3.2 m option marked as a nonconforming candidate. |
| Candidate row 5 (K:Q) versus BOM row 15 (B:I) | **CANDIDATE DOES NOT MEET BOM** | The candidate ABS enclosure is explicitly not flame-retardant, unlike the BOM requirement. | Do not treat that candidate as an approved flame-retardant case. |
| Candidate row 7 (K:Q) versus BOM row 27 (B:I) | **CANDIDATE FIT ISSUE** | The sheet says the 158×90×60 mm candidate is too shallow if the 12 V battery is inside. | The model houses the battery inside the junction box, so this candidate does not establish a valid fit. |

## Representation notes

The survivor battery holders are present inside the battery group, not missing parts. SAFE / NEED HELP / TRAPPED are three parts corresponding to one sheet row; the two LEDs likewise correspond to one row. Console USB and case are separate selectable parts corresponding to one row. Different sidebar counts therefore do not establish a BOM mismatch.

The relay’s ten listed component families are present, subject to the RTC detail omission and coax-fit issue above. Console component families are present, subject to the RTC detail omission and the contradictory antenna listing. The remaining BOM rows marked MATCH in the reference are component-family matches, not verified supplier CAD matches.

**Pending corrections:** align the survivor sensor and charger with the sheet; remove or document the unlisted battery-pack assumption and extra assemblies; represent the missing adapter/capacitors and incomplete resistor/RTC details; resolve sheet-internal antenna/candidate inconsistencies and the coax-fit issue before choosing replacement parts.
