# ao486

Aleksander Osman's [ao486](https://github.com/alfikpl/ao486), an x86 core that implements every feature of a 486 SX, taken as a black box.

![maturity](https://img.shields.io/badge/maturity-planned-lightgrey) ![license](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0%20OR%20MulanPSL--2.0-blue) ![upstream](https://img.shields.io/badge/upstream-BSD-lightgrey)

Part of the [Tape-Out](https://github.com/Tape-Out) IP library, wired up by [`xirang`](https://github.com/Tape-Out/xirang). One submodule, not modified: `third_party/ao486`. Only the core under `rtl/ao486` and its memories in `rtl/common` are used; upstream's PC SoC and its Bochs-derived model stay out.

## What this repository adds

The top is `ao486`, with an Avalon-MM memory manager, an Avalon-MM I/O manager and the interrupt handshake. The macros in `defines.v` are included by some files and used directly by others, so the sources form one compilation unit; the fragments under `autogen/` are included, not compiled on their own. Upstream uses more than sixty signals before declaring them, and the manifest allows `slang:UsedBeforeDeclared`.

`pipeline.v` references a signal that exists nowhere, inside `translate_off`. The synthesis path strips such regions, and the receipt skips them too.

```console
$ ran test ao486
```

## Limits

One 486 SX core with no top-level parameters. Upstream's tests compare it instruction by instruction against Bochs and need that simulation setup, so the gate here elaborates the design and checks the declaration.

## License

This repository: 任选其一 [MIT](LICENSE-MIT) · [Apache 2.0](LICENSE-APACHE) · [木兰宽松许可证 第2版](LICENSE-MULAN).

`third_party/ao486` keeps its own terms: BSD for `rtl`, LGPL for the Bochs-derived `bochs486` and `bochsDevs`, which this repository does not use. See its `LICENSE`.
