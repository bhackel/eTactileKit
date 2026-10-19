# October 2026 hardware revision

This fork carries the saved eTactileKit hardware changes made on October 14–16, 2026, based on [aid-lab-org/eTactileKit](https://github.com/aid-lab-org/eTactileKit) at commit `07af7f2f85e8dbe78840e53e1ab75e6d010936ad`. The original authors and [CC BY-SA 4.0 license](../LICENSE.txt) are retained. These changes are a manufacturing and sourcing revision, without hardware validation or an endorsement from the original authors.

## Open the projects

- [Controller — E_tactile.PrjPcb](02_PCB_Designs/01_Controller_board/E_tactile.PrjPcb)
- [Switching — Switching_Circuit.PrjPcb](02_PCB_Designs/02_Switching_PCB_HV513/Switching_Circuit.PrjPcb)
- [Finger16 manufacturing files and all JLC upload packages](03_Fabrication_Files/JLCPCB_2026-10-16/README.md)

The controller and switching schematics and PCB documents are the saved edited versions. Existing native libraries and other source sheets are retained in the upstream directory structure. No additional component, placement, routing, or polygon changes were made while organizing this fork.

## Saved native design changes

| Board / references | Saved choice | LCSC code | Notes |
|---|---|---|---|
| Controller T1–T3 | PBHV9050T-QR | C7508533 | Approved transistor substitution |
| Controller R10 | WFCP0402R0200FE66 | C4295137 | 20 mΩ, 0402 |
| Controller C3 | GRM1555C1H102JA01D | C76947 | 1 nF, C0G, 0402 |
| Controller R21 | HPCR0402F24K0K9 | C364976 | Corrected metadata for the existing 24 kΩ value |
| Controller D2 | LMBD3004SLT1G | C2912025 | Approved diode substitution |
| Controller Q5 | SQD40N06-14L_GE3 | C3291003 | Approved MOSFET substitution |
| Switching R1 | TNPW060360K4BEEA | C2075155 | 60.4 kΩ, 0.1%, same 0603 footprint |

Both controller GND polygons were unshelved and repoured during the design work. J1's controller position was checked and retained. The source footprints and routing otherwise retain the audited geometry.

## Altium metadata and manufacturing exports

The JLC purchasing BOMs are separate from the native supplier fields and ActiveBOM. Some native names, packaging suffixes, and supplier entries remain inherited. Use the dated `JLC_BOM.csv` files to identify this revision's actual purchasing choices. The native BOM workbooks are included separately as `Altium_BOM.xlsx`.

The final JLC placement files incorporate the reviewed vendor-specific rotation corrections. These do not modify the native PCB placements. Original Altium placement exports are included as `Altium_CPL.csv`; the manufacturing notes list every angle correction. Regenerating a CPL directly from Altium will require those JLC corrections again.

Finger16 is derived from the author's checked-in fabrication outputs, with one added TOP FR4 0.2 mm stiffener and a connector assembly BOM/CPL. No Finger16 Altium source was edited. The unrelated upstream Two_finger Altium design is not its source.

During relocation, absolute document and output-directory paths in the two project/output-job settings were made relative. Text project, output-job, and BOM metadata use LF line endings; schematic, PCB, and library binary files retain their saved bytes. The controller's generated `CAMtastic1.Cam` tab reference was removed because it contained absolute import paths. Generated CAM imports, hierarchy caches, editing history, local reports, and personal procurement records are not part of this revision.

The switching project retains upstream references to missing `Components/HV513-QFN.SchLib` and `.PcbLib`. Those files were absent from the original working project too; this move did not remove them. Existing PCB footprints and the other native libraries are included.

Historical upstream fabrication folders and PDFs are still present. Use the dated [JLCPCB snapshot](03_Fabrication_Files/JLCPCB_2026-10-16/) for the exports associated with these changes. Its manifest records SHA-256 hashes for the preserved files.

## Manufacturing status of this revision

The rigid-board Gerbers still contain open plated vias overlapping SMD solder joints. No resin filling or copper capping was added in this revision, and order review approval does not establish the final via treatment. The flex coverlay, stiffener side, and connector placement also require the manufacturer's production-proof review. See the manufacturing notes for the recorded limits and the items to review before another build.
