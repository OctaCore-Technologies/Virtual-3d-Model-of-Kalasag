# Sheet alignment changes

Branch: `feat/sheet-aligned-components`. Baseline: `10806ec`. Authority: [Hardware BOM](https://docs.google.com/spreadsheets/d/1QLaJ-uK42XSZoBPESpl_FkiHE4a3wLdfT5JuzkQpVLM/edit?gid=0), using the supplied 2026-10-03 transcription. The original audit and comparison markers remain a historical record; no live refresh succeeded during this implementation.

| BOM rows | Current representation |
| --- | --- |
| 9 | ADXL345 GY-291 replaces SW-420, comparator and trimmer geometry; eight-pin header and shared I²C are represented. |
| 11, 16 | Three IFR18650 3.2 V / 1500 mAh cells with individual holders, per the requested model layout. Enclosure extended downward for clearance. Sheet quantity/topology remain unspecified; no aggregate capacity or pack interconnects are assumed. |
| 12 | TP5000 with inductor and IN/BAT pads, set to 3.6 V; no SYS terminal. |
| 14 | External 5 V adapter body, prongs and lead. |
| 15 | Flame-retardant ABS IP65 requirement stated on enclosure; geometry does not establish a tested rating. |
| 17 | Six illustrative axial 1/4 W 1% resistors: four LED series resistors and two divider resistors. Values and final connectivity unspecified. |
| 18 | Two representative electrolytic capacitors beside ESP32/radio; quantities, capacitance and voltage ratings unspecified. |
| 19, 29, 35 | All three RTC breakouts include DS3231 and AT24C32 EEPROM geometry/labels. |
| 23 | Coax routed directly to top gland; nominal centerline length checked against 3 m at the declared relay scale. Purchased connector allowances/slack need verification. |
| 36 | Representative installed wiring/cable ties; solder, flux, IPA and other process consumables are not installed modules. |

Other named BOM families remain represented. Removed unlisted additions: MCP23017, 3.3 V buck-boost, distribution board and relay fuse. The common transparent hinged cover is restored as a custom enclosure modification, sharing the front-case selection; it is not a separate BOM part/module. Individual TRAPPED guard is retained. Non-BOM battery alternatives are removed from appearance and setup imports.

## Wiring dependencies and unresolved circuit design

The former charger SYS output fed the buck-boost, which fed the distribution board. The expander supplied button/LED GPIO and RTC I²C. Those dependencies were inspected before removal. TP5000 is represented with charger input and connections to the BMS; cell interconnects and pack-to-BMS leads are omitted pending pack topology; the relay battery now connects directly to LM2596 without the unlisted fuse.

Survivor RTC and ADXL345 share illustrative GPIO20/21 I²C; radio SPI/control nets remain. Load-power connections are omitted because no replacement regulator or power-path circuit is listed. Button/LED and passive connections are omitted pending a complete GPIO allocation and resistor values. These omissions are stated in the website and README. The BOM does not define a complete electrically validated circuit.

## Sheet conflicts retained

Relay antenna follows the named 5.8 dBi requirement, with the contradictory 8 dBi cost/listing note identified separately. Console antenna follows the named 3 dBi magnetic-mount requirement, with the spare 2 dBi note unresolved. The 3.2 m tripod and standard ABS case candidates do not replace the 4 m and flame-retardant ABS requirements. No candidate SKU is treated as approved supplier CAD.

## Local verification

`tests/browser-check.cjs` passed desktop/mobile framing, mouse orbit/height navigation, emulated two-finger pan/pinch, tab persistence, console Hardware/Dashboard, alert acknowledgement/dispatch/reset, BOM component/source checks, coax centerline fit, and exploded wire attachment checks. No browser JavaScript or console errors were captured. Screenshots were saved locally for inspection. No commit or push was made.
