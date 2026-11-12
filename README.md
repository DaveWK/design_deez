# design_deez

Open, clean-room replacements for the closed parts of Synopsys DesignWare IP, so SoCs that license it can run on open
code alone.

## Part of the "forbidden secret math" driver series

They make real chips, then keep selling them with drivers they know are broken. Half the features the silicon
supports never make it into the driver at all. Nobody even files bug reports anymore: the $5 dongle just doesn't
work, and it ends up in a drawer. The firmware is locked so nobody else can fix it. The out-of-tree driver rots until
the device is e-waste, and the next product ships with the same problems. This series does the job they keep sweeping under the rug:
well-maintained, feature-complete open replacements, so their code and patent troll behaviours can be deleted and
forgotten.

The closed path stays in use until its open replacement matches it on every feature and measures as good or better.

- [i_hate_realtek](https://github.com/DaveWK/i_hate_realtek): Realtek firmware and drivers
- [i_hate_powervr](https://github.com/DaveWK/i_hate_powervr): PowerVR GPU firmware (Rust)
- [design_deez](https://github.com/DaveWK/design_deez): Synopsys DesignWare (DDR PHY training first)

## Why

DesignWare blocks sit inside a large share of SoCs. Several of them already have good open drivers: DWC3 USB,
DWMAC/stmmac Ethernet, DWC PCIe, the DW UART and dw-hdmi. Others still depend on closed code that runs on every boot.
The worst offender is the **DDR PHY**:
- its training firmware runs on the PHY's embedded microcontroller;
- vendor DRAM libraries contain PIE sequencer images and PhyInit code;
- PHY register sequences ship only as generated tables.

Nobody outside Synopsys and its licensees can audit or fix any of it.

This repository is where the open replacements, register documentation and measurements get built.

## Scope

- **DDR PHY (LPDDR4/LPDDR5): open initialisation and training without the vendor firmware.** That covers PHY
  configuration, command-bus and write-leveling, read and write eye and Vref training, and the hand-over to mission
  mode. Our own measurements are the reference.
- **The PIE sequencer:** what it does at bring-up and at runtime (PHY-initiated updates, frequency changes), and open
  replacements for it.
- **HDMI TX and PHY:** open PHY and PLL configuration that doesn't rely on vendor-generated tables. HDCP is out of
  scope; it needs licensed keys.
- **Register documentation** for each block, with every fact's open source or measurement cited.
- **Parity and benchmark results** against the closed path: training time, eye margins, bandwidth, latency, and error
  rate under stress.

First target: the LPDDR5 DWC PHY in the Allwinner A733 (Radxa Cubie A7A), where open bring-up already works but
training still runs the Synopsys firmware.

## What this repository does NOT contain

- No Synopsys firmware, PIE images, PhyInit code, databooks or vendor DRAM libraries.
- Nothing obtained by disassembling or decompiling them.
- No confidential or NDA documentation.

See [CONTRIBUTING.md](CONTRIBUTING.md). Clean room is the whole point: it keeps the result unencumbered.

## Status

Starting. Contributions are welcome, including LLM-assisted ones, under the rules in CONTRIBUTING.md.

## Licence

MIT unless a file says otherwise. Code derived from GPL-licensed sources keeps their licence, noted per file.
