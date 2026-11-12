# Contributing (clean-room rules)

These rules apply to everyone, human or LLM-assisted. Contributions that break them will be removed.

## Allowed inputs

- **Open-source code under an open licence:** the Linux kernel, U-Boot, TF-A, coreboot, oreboot and other open
  projects that drive DesignWare blocks or train DDR PHYs (including open trainers for other PHY families), and
  GPL BSP source published by SoC vendors.
- **Public documentation:** datasheets, talks, papers and mailing-list posts that are publicly available without an NDA.
- **Black-box observation:** register reads and writes on real hardware, the behaviour and margins we measure, and
  the results of running our own code. Register traces of a running closed binary are flagged as such, need the
  maintainer's approval before use, and must never be the only basis for shipped code.

## Forbidden inputs

- Synopsys firmware, PIE images, PhyInit code or vendor DRAM libraries, including anything learned from
  disassembling, decompiling or hex-dumping them.
- Synopsys databooks or any other document under NDA.
- Leaked, confidential or NDA material of any kind.
- Code copied from a source whose licence doesn't permit it.

## Requirements for every contribution

1. **Provenance.** Cite the open source for each interface fact, constant or sequence, as file and line or URL.
2. **Licence.** State it for new files. Code derived from GPL headers keeps the GPL.
3. **Tests and evidence.** Changes come with the test, measurement or hardware log that shows what they do.
4. **LLM-assisted work** follows the same rules. Tell the model the forbidden inputs above, and review its sources
   before submitting.

## Reporting

If you find something in the repository that came from a forbidden input, open an issue. It will be removed and
rewritten clean.
