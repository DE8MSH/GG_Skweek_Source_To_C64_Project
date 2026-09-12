# GG Skweek Source → C64 Project

Source-only repository for the reverse-engineered Sega Game Gear version of **Skweek**, intended as a reference base for a C64 port/reimplementation.

## What is included

The `gamegear/` directory contains the complete 128 KiB Game Gear program/data representation as Z80 assembly source, plus the small independent assembler/build verifier used for the round-trip test.

No original ROM, generated ROM, bank binaries, ZIP archives, screenshots, extracted assets, CSV exports, or build artifacts are committed.

## Verified source round-trip

From `gamegear/` run:

```sh
make verify
```

The build assembles all eight 16 KiB physical banks from text source, joins them in cartridge order, and checks the resulting image against the verified reference SHA-1:

```text
0788c35636abba46beb01acebfd1697cdb54161c
```

A successful build therefore proves that the text source reproduces the analyzed Game Gear ROM byte-identically. The original ROM is **not required** for this SHA-1 verification and is deliberately not included in the repository.

If you legally provide your own copy as `gamegear/rom/skweek.gg`, the verifier additionally performs a direct byte-for-byte comparison.

## Layout

- `gamegear/src/bank00_complete.asm` — fixed Z80 bank 0, code plus classified data
- `gamegear/src/bank01_complete.asm` — fixed Z80 bank 1, code plus classified data/assets
- `gamegear/src/bank02_data.asm` — banked data/assets
- `gamegear/src/bank03_complete.asm` — PSG/audio engine plus music/SFX data
- `gamegear/src/bank04_data.asm` — banked gameplay graphics/data
- `gamegear/src/bank05_data.asm` — banked UI/graphics/data
- `gamegear/src/bank06_data.asm` — 99 level streams and related data
- `gamegear/src/bank07_data.asm` — banked intro/graphics/data
- `gamegear/src/hardware.inc` — Game Gear/SMS hardware symbols
- `gamegear/src/ram.inc` — reverse-engineered RAM symbols
- `gamegear/tools/z80asm_min.py` — independent assembler for this source syntax
- `gamegear/tools/build_from_source.py` — bank builder and SHA-1 verifier

The source comments retain exact original instruction/data bytes as an audit aid, but the assembler ignores comments; the hash check validates the actual mnemonics and data directives.
