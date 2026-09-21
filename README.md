# 3S 18650 Battery Pack for QRP Radio

A compact, rechargeable 3S 18650 battery-pack prototype for portable QRP radio operation. The project combines a custom PCB, a three-cell battery holder, protection circuitry, USB-C charging input, voltage display, XT30 power output, and a 3D-printed enclosure.

> **Prototype status**  
> The mechanical prototype is complete. Charging, protection, thermal, sustained-load, and field-operation behaviour still require verification. The 5 A figure is a design target, not a verified continuous-output rating.

![Finished 3S 18650 battery pack in its 3D-printed enclosure](media%20files/assembled/IMG_20260920_215517_3_2026-09-20_21-56-50_902.jpg)

## Project Goals

- Use three 18650 lithium-ion cells in series
- Provide up to 12.6 V when the cells are fully charged
- Target up to 5 A output for suitable portable QRP equipment
- Include battery protection and a charging input
- Show battery voltage and charging status
- Provide a compact XT30 power output
- Fit the complete module into a purpose-designed enclosure

## Hardware Overview

The PCB is approximately **78.7 x 64.9 mm**. The three-cell holder uses most of the board area, while the user-facing parts sit around the board edge for access through the enclosure.

| Function | Implementation |
|---|---|
| Battery | Three 18650 cells in series, or 3S |
| Pack voltage | Up to 12.6 V when fully charged |
| Protection | CM1033-DS protection controller and MOSFET switching stage |
| Charging input | USB-C receptacle and charge-control section |
| Charge status | `CHG` and `FULL` LEDs |
| Voltage display | Three-digit panel meter |
| Power output | XT30 connector |
| Controls | Toggle switch and small slide switch |
| Enclosure | Two-part 3D-printed case |

![3D PCB render with the three-cell holder and front-edge connectors](media%20files/3D_PCB_BatteryPack_3S_18651_Rev1.1_2026-09-19.png)

## Circuit Overview

The schematic is included as a PNG for quick reference. The editable EasyEDA Pro project is in `sch/`.

![Schematic for the 3S 18650 battery-pack module](media%20files/SCH_BatteryPack_3S_18651_1-SCH_BatteryPack_3S_18650_Rev1.1_2026-09-19.png)

### Battery and Protection Section

The three-cell holder connects to the battery-protection section. The **CM1033-DS** controller monitors the series-cell connections and works with the **AO4406AL** MOSFET stage to control the protected battery path. This section is intended to disconnect or control the pack under fault conditions.

The protection circuit, MOSFETs, cell wiring, PCB copper, output connector, and the cells themselves must all be checked before use. Do not assume that a protection IC alone makes a battery pack safe.

### USB-C Charging Section

The USB-C receptacle provides the charging input. Its CC resistors identify the board as a basic USB-C power sink. The input passes through fuse **F1** and into the charge-control section built around **U4**, **L1**, **D1**, and associated components.

The schematic labels two LEDs as `CHG` and `FULL`. They provide a simple visible indication of charging state. Verify the actual charge voltage, current, termination, and LED behaviour with suitable test equipment before charging cells in the finished enclosure.

### Display, Switching, and Output

The three-digit meter displays the pack voltage. A toggle switch controls the power output, and the XT30 connector provides the external connection for a suitable radio or other 12 V load.

The pack must only be used with equipment that accepts the voltage range of a three-cell lithium-ion battery pack across its complete discharge range. Check the equipment manual before connecting it.

![PCB layout showing the cell positions and front-edge electrical section](media%20files/PCB_PCB_BatteryPack_3S_18651_Rev1.1_2026-09-19.png)

## Assembly

The build starts with the small surface-mount parts for the protection and charging circuits. Larger parts are then fitted, including the battery holder, USB-C connector, XT30 connector, switches, and voltage-display module.

![Battery-pack PCB, cell holder, solder paste, and front-panel parts before assembly](media%20files/assembling/DSC04764.JPG)

The voltage-display module is mounted on the left side of the PCB. Care is needed when fitting the connectors and switches because their positions must match the enclosure openings.

![Populated battery-pack PCB with the holder, voltage display, USB-C input, switch, and XT30 connector](media%20files/assembling/IMG_20260919_225959_0_2026-09-19_23-00-57_815.jpg)

The raw assembly videos are kept out of the repository to keep clone sizes manageable. The build photos and GIFs in `media files/assembling/` document the assembly sequence.

## Enclosure

The enclosure was designed around the real PCB, holder, display, connectors, and switches. The lower printed part supports the electronics, while the top cover protects the finished assembly. Openings provide access to the USB-C charging port, controls, display, and output connector.

![Open lower enclosure with the 3S battery-pack PCB and cell holder fitted inside](media%20files/assembled/IMG_20260920_215456_2_2026-09-20_21-56-50_886.jpg)

The raw enclosure-design video is kept out of the repository to keep clone sizes manageable. The enclosure photos and CAD files remain available here.

## Repository Contents

```text
cad/
  bottom.3mf                         3D-printable lower enclosure
  bottom.stl                          Lower enclosure mesh
  top.stl                             Upper enclosure mesh
  libraries/3D_PCB_BatteryPack...step PCB STEP model for mechanical checks
gerber/
  Gerber_PCB_BatteryPack_3S_...zip    PCB fabrication archive
media files/
  assembled/                          Finished-pack photos, GIFs, and enclosure video
  assembling/                         Build photos, GIFs, and assembly video
  *.png                               Schematic, PCB layout, and 3D PCB renders
sch/
  ProPrj_BatteryPack_3S_18650_...     EasyEDA Pro project
```

## Opening the Design Files

1. Open `sch/ProPrj_BatteryPack_3S_18650_Module_2026-09-19.epro2` in [EasyEDA Pro](https://pro.easyeda.com/) to inspect the editable schematic and PCB project.
2. Use the Gerber archive in `gerber/` to order the PCB from a board fabricator.
3. Open `cad/top.stl`, `cad/bottom.stl`, or `cad/bottom.3mf` in a slicer before printing the enclosure.
4. Use the STEP model in `cad/libraries/` to check the PCB fit in a mechanical CAD package.

## Safety and Testing

This is a lithium-ion battery project. Build and test it only if you understand the hazards of lithium-ion cells and high-current wiring.

- Use matched cells of the same type, age, and condition.
- Do not charge damaged, swollen, or unknown cells.
- Check cell polarity, connector polarity, and wiring before inserting cells.
- Do not short the pack or exceed the capability of the cells, connectors, wiring, PCB traces, or protection circuit.
- Test charging, protection behaviour, voltage drop, and temperature under controlled conditions before connecting radio equipment.
- Never leave a lithium-ion pack charging unattended.

This repository documents a prototype. It is not a certified battery design and does not guarantee safety, suitability, or electrical performance.

## Planned Field Use

The intended use is a compact power source for a portable QRP station. A future POTA outing will pair the pack with a suitable QRP radio, lightweight antenna, coax, and CW paddle.

## License

No license has been selected yet. Do not assume permission to manufacture, modify, or redistribute these files until a license is added.
