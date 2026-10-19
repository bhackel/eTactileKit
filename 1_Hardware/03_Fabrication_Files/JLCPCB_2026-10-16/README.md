# JLCPCB manufacturing snapshot — 2026-10-16

These are preserved manufacturing exports for the compact controller, compact switching board, and 16-electrode fingertip flex. They record the exported geometry and reviewed JLC part/placement mappings; they are not regenerated automatically from the Altium projects. Keep this dated snapshot unchanged when preparing a later revision.

The designs derive from [aid-lab-org/eTactileKit](https://github.com/aid-lab-org/eTactileKit), upstream commit [`07af7f2f85e8dbe78840e53e1ab75e6d010936ad`](https://github.com/aid-lab-org/eTactileKit/tree/07af7f2f85e8dbe78840e53e1ab75e6d010936ad). Original contributors are Praneeth Bimsara Perera, Ravindu Madhushan Pushpakumara, Hiroyuki Kajimoto, Arata Jingu, Jürgen Steimle, and Anusha Withana. This derivative retains [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/); see the repository [license](../../../LICENSE.txt). Manufacturing adaptations are described below; no upstream endorsement is implied.

## Files and provenance

| Directory | Fabrication and assembly files | Per-board assembly scope |
|---|---|---|
| [controller](controller/) | `Gerbers.zip`, `JLC_BOM.csv`, `JLC_CPL.csv`, `HAND_FIT.txt` | 43 BOM groups, 42 purchasing codes, 64 Top placements |
| [switching](switching/) | `Gerbers.zip`, `JLC_BOM.csv`, `JLC_CPL.csv` | 5 BOM groups, 11 placements: 6 Top / 5 Bottom |
| [finger16](finger16/) | `Gerbers.zip`, `JLC_BOM.csv`, `JLC_CPL.csv`, `fr4t_0.2.gerber` | One Bottom connector |

Each rigid-board ZIP contains nine Gerber layers and two drill files, byte-identical to its saved Altium manufacturing exports. Controller drills separate plated and nonplated holes; switching drills separate plated round holes and plated slots. Use the ZIP contents together, preserving their shared origin.

The saved native exports are also preserved as [controller Altium_CPL.csv](controller/Altium_CPL.csv), [controller Altium_BOM.xlsx](controller/Altium_BOM.xlsx), [switching Altium_CPL.csv](switching/Altium_CPL.csv), and [switching Altium_BOM.xlsx](switching/Altium_BOM.xlsx). The native CPL report header's absolute local filename was replaced with `Altium_CPL.csv`; the placement tables are unchanged. These are distinct from the JLC upload files. The native workbooks retain their exported component metadata; no reconciliation with ActiveBOM is claimed. Native and JLC CPL coordinates are in millimetres, with no Y flip or coordinate translation.

The flex comes from the upstream `3_Electrode_Design_Tool/3_FabricationTool_App/outputs/PCB_electrodes/Fabrication_Finger_Pad` outputs. Its ZIP retains eleven author manufacturing files byte-for-byte and adds one stiffener layer. Author drill-map drawings are inspection aids and are excluded from the fabrication ZIP.

## Part mappings and hand fitting

The JLC BOMs contain the actual purchasing choices. Native schematic comments, supplier fields, and footprint names can differ; regenerating a native BOM alone does not reproduce these mappings.

- Controller C1/C2 and C8/C11/C15/C25 are separate footprint groups using the same Samsung `CL05B104KO5NNNC` / C1525 part. Both groups must remain included.
- Controller L1 uses `ATB322515-0110-T000` / C415291; the native generic name is `ATB322515`. J3 uses `532610271` / C177225, equivalent to the hyphenated `53261-0271` identifier. OP2/OP3 use `TL072IDR` / C6962.
- Controller DA1 uses `AD5452YRMZ` / C208119 in tubes instead of native `AD5452YRMZ-REEL7`; chip and package are the same. C13/C14/C18/C19 use `C3225X7R2J683KT0L0U` / C342738; some inherited native supplier metadata retains the older `C3225X7R2J683K200AA` name.
- Switching R1 uses the approved `TNPW060360K4BEEA` / C2075155: 60.4 kΩ, 0.1%, retaining the 0603 footprint. All eleven switching components are included for assembly.

Per controller, hand-fit **one TE Connectivity 2307727-2 at J4** and **one regular Seeed Studio XIAO ESP32-S3, SKU 113991114**. Both are omitted from its JLC BOM/CPL. J0 is a solder bridge and has no purchased assembly part. See [HAND_FIT.txt](controller/HAND_FIT.txt).

## JLC placement rotations

These rotations correct the JLC component-library convention; they do not change the physical Altium placements. They are already present in the final CPLs. Do not apply them a second time or assume another assembler uses the same convention.

| Controller reference | Native angle | Final JLC angle |
|---|---:|---:|
| AD1 | 90° | 270° |
| D2 | 270° | 90° |
| DA1 | 90° | 0° |
| IC1 | 0° | 270° |
| OP2, OP3 | 0° | 270° |
| Q5 | 90° | 180° |
| T4 | 90° | 270° |
| U8, VREG | 0° | 270° |

All other controller CPL angles retain the native export values, including L1 = 0°. The final [controller CPL](controller/JLC_CPL.csv) is byte-identical to the reviewed orientation candidate. J1/J2, T1–T3, and R10 lacked rendered JLC models; production placement review remains necessary. R10 is nonpolar.

| Switching reference | Native angle | Final JLC angle |
|---|---:|---:|
| J1, J2 | 0° | 180° |
| U1, U3 — Bottom | 0° | 90° |
| U2, U4 — Top | 180° | 90° |
| J3, J4, J5, J6 | 270° | 270° |
| R1 | 0° | 0° |

Reimporting the [switching CPL](switching/JLC_CPL.csv) reproduced the reviewed alignment on both sides. J3/J4 lacked rendered models and require production placement proof.

## Finger16 connector and stiffener

The connector is **Hirose FH12-16S-1SH(55)** / C3169166. The added assembly reference J1 uses **X144.412776, Y−63.572881 mm, Bottom, 180°**. Negative Y is intentional. All sixteen signal leads and both anchor pads aligned in the reviewed mirrored Bottom preview. Solder tails face the electrode traces (−Y); the mouth/actuator faces the short outer edge (+Y). Author Gerbers do not number the pads, so cable/channel mapping must be established separately.

The only flex fabrication geometry addition is a **TOP FR4 stiffener, nominally 0.2 mm**, behind the Bottom connector. `fr4t_0.2.gerber` defines a 24.0 × 14.7 mm rectangle: X132.412776–156.412776, Y−70.000000–−55.300000 mm. It is already inside the ZIP. Original copper, coverlay/mask, paste, silkscreen, outline, and drills are unchanged. No panelization, mirroring, or translation is baked into this package; vendor panelization requires matching placement handling. Keep the supported connector region unbent.

## Review before future manufacturing

Both rigid boards retain **exposed plated vias overlapping SMD solder joints**. Solder can wick into these holes during reflow. This snapshot does not include a resin-fill/capping change or establish the manufacturer's final treatment. Resolve the affected-via treatment and review the resulting CAM/assembly proof before reusing these files for another order; changing assemblers alone does not remove the geometry.

The flex retains its author's coverlay: nominal connector web width is 0.4 mm with zero opening expansion. Confirm the vendor's actual coverlay interpretation, stiffener side/thickness, stackup, and any merged or expanded windows. Review any proposed geometry changes before approving them.

Recheck part availability, matched MPNs, connector polarity/pin 1, both-side placement proofs, and any panel transforms for future orders. The recorded preview checks do not constitute electrical or body-use qualification; inherited voltage-rating and hardware-testing questions remain unresolved. No safety certification is claimed.
