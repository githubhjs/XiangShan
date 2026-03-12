# XiangShan

XiangShan (香山) is an open-source high-performance RISC-V processor project.

中文说明[在此](readme.zh-cn.md)。

## Documentation

XiangShan's documentation is available at [docs.xiangshan.cc](https://docs.xiangshan.cc).

XiangShan Design Document for Kunminghu V2R2 has been published separately. You can find it at [docs.xiangshan.cc/projects/design](https://docs.xiangshan.cc/projects/design/).

XiangShan User Guide has been published separately. You can find it at [docs.xiangshan.cc/projects/user-guide](https://docs.xiangshan.cc/projects/user-guide/) or [XiangShan-User-Guide/releases](https://github.com/OpenXiangShan/XiangShan-User-Guide/releases).

We are using [Weblate](https://hosted.weblate.org/projects/openxiangshan/) to translate documentation into English and other languages. Your contributions are welcome—come and help us improve it!

All XiangShan documents are licensed under the CC-BY-4.0.

## Publications

### MICRO 2022: Towards Developing High Performance RISC-V Processors Using Agile Methodology

Our paper introduces XiangShan and the practice of agile development methodology on high performance RISC-V processors.
It covers some representative tools we have developed and used to accelerate the chip development process, including design, functional verification, debugging, performance validation, etc.
This paper is awarded all three available badges for artifact evaluation (Available, Functional, and Reproduced).

![Artifacts Available](https://github.com/OpenXiangShan/XiangShan-doc/raw/main/publications/images/artifacts_available_dl.jpg)
![Artifacts Evaluated — Functional](https://github.com/OpenXiangShan/XiangShan-doc/raw/main/publications/images/artifacts_evaluated_functional_dl.jpg)
![Results Reproduced](https://github.com/OpenXiangShan/XiangShan-doc/raw/main/publications/images/results_reproduced_dl.jpg)

[Paper PDF](https://github.com/OpenXiangShan/XiangShan-doc/blob/main/publications/micro2022-xiangshan.pdf) | [IEEE Xplore](https://ieeexplore.ieee.org/abstract/document/9923860) | [BibTeX](https://github.com/OpenXiangShan/XiangShan-doc/blob/main/publications/micro2022-xiangshan.bib) | [Presentation Slides](https://github.com/OpenXiangShan/XiangShan-doc/blob/main/publications/micro2022-xiangshan-slides.pdf) | [Presentation Video](https://www.bilibili.com/video/BV1FB4y1j7Jy)

## Follow us

Wechat/微信：香山开源处理器

<div align=left><img width="340" height="117" src="images/wechat.png"/></div>

Zhihu/知乎：[香山开源处理器](https://www.zhihu.com/people/openxiangshan)

Weibo/微博：[香山开源处理器](https://weibo.com/u/7706264932)

You can contact us through [our mailing list](mailto:xiangshan-all@ict.ac.cn). All mails from this list will be archived [here](https://www.mail-archive.com/xiangshan-all@ict.ac.cn/).

## Architecture

The first stable micro-architecture of XiangShan is called Yanqihu (雁栖湖) and is [on the yanqihu branch](https://github.com/OpenXiangShan/XiangShan/tree/yanqihu), which has been developed since June 2020.

The second stable micro-architecture of XiangShan is called Nanhu (南湖) and is [on the nanhu branch](https://github.com/OpenXiangShan/XiangShan/tree/nanhu).

The current version of XiangShan, also known as Kunminghu (昆明湖), is still under development on the master branch.

The micro-architecture overview of Kunminghu (昆明湖) is shown below.

![xs-arch-kunminghu](images/xs-arch-kunminghu.svg)



## Sub-directories Overview

Some of the key directories are shown below.

```
.
├── src
│   └── main/scala         # design files
│       ├── device         # virtual device for simulation
│       ├── system         # SoC wrapper
│       ├── top            # top module
│       ├── utils          # utilization code
│       └── xiangshan      # main design code
│           └── transforms # some useful firrtl transforms
├── scripts                # scripts for agile development
├── yunsuan                # yunsuan submodule of XiangShan
├── huancun                # L2/L3 cache submodule of XiangShan
├── difftest               # difftest co-simulation framework
└── ready-to-run           # pre-built simulation images
```

## IDE Support

### bsp
```
make bsp
```

### IDEA
```
make idea
```


## Generate Verilog

* Run `make verilog` to generate verilog code. This generates multiple `.sv` files in the `build/rtl/` folder (e.g., `build/rtl/XSTop.sv`).
* Refer to `Makefile` for more information.

### Notes for this fork

The generated RTL artifacts in this fork were produced with the following toolchain and command flow:

* Reproducible host environment:
  This build was done from WSL2 on a Windows host, using Ubuntu 24.04.1 LTS (`x86_64`) with Linux kernel `6.6.87.2-microsoft-standard-WSL2`.
* Reproducible filesystem assumption:
  The working tree was placed on the Windows `D:` drive at `D:/temp/XiangShan`, seen from WSL as `/mnt/d/temp/XiangShan`.
* WSL home location:
  In this environment, `/home/hjs` is available from Windows as `\\wsl.localhost\Ubuntu-24.04\home\hjs`.
* Workspace location:
  The repository was cloned under `D:/temp/XiangShan` and accessed from WSL as `/mnt/d/temp/XiangShan`.
* Windows filesystem configuration:
  Because this build was done on a Windows-backed filesystem, NTFS case-sensitivity had to be enabled on `D:/temp/XiangShan` before rebuilding. Without that setting, XiangShan can fail when source files or generated symbols differ only by letter case.
* Base system packages:
  The build environment used `git 2.43.0`, `openjdk-17-jdk`, `make`, `gcc`, `g++`, `curl`, `git-lfs`, and `xz`.
* Git:
  The repository was cloned with `git clone https://github.com/githubhjs/XiangShan/ /mnt/d/temp/XiangShan`.
* Submodule toolchain:
  XiangShan submodules and nested submodules were initialized with `make init`.
* Java toolchain:
  `openjdk-17-jdk` was installed and used as the JVM for `mill` and the Chisel elaboration flow. The JVM in this build reported `openjdk version "17.0.18"`.
* Mill build tool:
  XiangShan pins Mill with `.mill-version`, and this repository specifies Mill `0.12.15`. The build used that pinned version through the project bootstrap flow rather than an arbitrary global version.
* Firtool resolver:
  The firtool path was resolved with `mill -i show xiangshan.resolveFirtoolDeps`, which produced `/home/hjs/.cache/llvm-firtool/1.135.0/bin/firtool`.
* Firtool version:
  The resolved firtool binary reports LLVM/CIRCT toolchain version `22.0.0git`.
* Main RTL generation target:
  Chisel elaboration was run with `make verilog`, which targets `top.TopMain` and writes generated outputs under `build/rtl/`.
* Direct firtool fallback:
  In this environment, `make verilog` produced `build/rtl/XSTop.fir`, but the split SystemVerilog emission had to be completed by directly invoking:
  `/home/hjs/.cache/llvm-firtool/1.135.0/bin/firtool /mnt/d/temp/XiangShan/build/rtl/XSTop.fir -warn-on-unprocessed-annotations -output-annotation-file /mnt/d/temp/XiangShan/build/rtl/circt.anno.json -O=release --disable-annotation-unknown --lowering-options=explicitBitcast,disallowLocalVariables,disallowPortDeclSharing,locationInfoStyle=none --ignore-read-enable-mem --default-layer-specialization=disable --split-verilog -o=/mnt/d/temp/XiangShan/build/rtl`
* Generated RTL outputs:
  The resulting split RTL includes `build/rtl/XSTop.sv` and the rest of the generated `.sv` module set in `build/rtl/`.
* FIR artifact handling:
  The raw FIR file `build/rtl/XSTop.fir` is about 1.2 GB and is too large for a normal GitHub push.
* Compression toolchain:
  The FIR artifact was compressed with `xz -T0 -9 -k -f /mnt/d/temp/XiangShan/build/rtl/XSTop.fir`, producing `build/rtl/XSTop.fir.xz`. The compressor in this environment was `xz (XZ Utils) 5.4.5`.
* Published FIR artifact:
  The compressed FIR file `build/rtl/XSTop.fir.xz` is stored in this fork because it is small enough for normal GitHub upload.
* Decompression:
  Restore the FIR file with `xz -d build/rtl/XSTop.fir.xz`.
* Git LFS note:
  `git-lfs` was installed and tested, but GitHub rejected new LFS object uploads on this public fork. For that reason, the compressed `.xz` artifact is used instead of publishing the raw FIR through LFS.



## Run Programs by Simulation

### Prepare environment

* Set environment variable `NEMU_HOME` to the **absolute path** of the [NEMU project](https://github.com/OpenXiangShan/NEMU).
* Set environment variable `NOOP_HOME` to the **absolute path** of the XiangShan project.
* Set environment variable `AM_HOME` to the **absolute path** of the [AM project](https://github.com/OpenXiangShan/nexus-am).
* Install `mill`. Refer to [the Manual section in this guide](https://mill-build.org/mill/cli/installation-ide.html#_bootstrap_scripts).
* Clone this project and run `make init` to initialize submodules.

### Run with simulator

* Install [Verilator](https://verilator.org/guide/latest/), the open-source Verilog simulator.
* Run `make emu` to build the C++ simulator `./build/emu` with Verilator.
* Refer to `./build/emu --help` for run-time arguments of the simulator.
* Refer to `Makefile` and `verilator.mk` for more information.

Example:

```bash
make emu CONFIG=TLMinimalConfig EMU_THREADS=2 -j10
./build/emu -b 0 -e 0 -i ./ready-to-run/coremark-2-iteration.bin --diff ./ready-to-run/riscv64-nemu-interpreter-so
```

### Run with xspdb 
* Install [picker](https://github.com/XS-MLVP/picker), a verification tool that supports high-level languages.
* Run `make pdb` to build XiangShan Python binaries.
* Run `make pdb-run` to run XiangShan binaries.

Example output and interaction:

```bash 
$ make pdb-run
[Info] Set PMEM_BASE to 0x80000000 (Current: 0x80000000)
[Info] Set FIRST_INST_ADDRESS to 0x80000000 (Current: 0x80000000)
Using simulated 32768B flash
[Info] reset dut complete
> XiangShan/scripts/pdb-run.py(13)run()
-> while True:
(XiangShan) xload ready-to-run/microbench.bin   # Load binary (Tab-compatible)
(XiangShan) xwatch_commit_pc 0x80000004         # set watch point,  
(XiangShan) xistep 3                            # Step to next three instruction commit, it will stop at watch point 
[Info] Find break point (Inst commit), break (step 2107 cycles) at cycle: 2207 (0x89f)
[Info] Find break point (Inst commit, Target commit), break (step 2108 cycles) at cycle: 2208 (0x8a0)
(XiangShan) xpc                                 # print pc info
PC[0]: 0x80000000    Instr: 0x00000093
PC[1]: 0x80000004    Instr: 0x00000113
PC[2]: 0x0    Instr: 0x0
...
PC[7]: 0x0    Instr: 0x0
(XiangShan) xistep 1000000                      # Execute to binary end
[Info] Find break point (Inst commit), break (step 2037 cycles) at cycle: 2207 (0x89f)
[Info] Find break point (Inst commit), break (step 2180 cycles) at cycle: 2207 (0x89f)
...
HIT GOOD LOOP at pc = 0xf0001cb0
```

## Troubleshooting Guide

[Troubleshooting Guide](https://github.com/OpenXiangShan/XiangShan/wiki/Troubleshooting-Guide)

## Acknowledgement

The implementation of XiangShan is inspired by several key papers. We list these papers in XiangShan document, see: [Acknowledgements](https://docs.xiangshan.cc/zh-cn/latest/acknowledgments/). We very much encourage and expect that more academic innovations can be realised based on XiangShan in the future.

## LICENSE

Copyright © 2020-2025 Institute of Computing Technology, Chinese Academy of Sciences.

Copyright © 2021-2025 Beijing Institute of Open Source Chip

Copyright © 2020-2022 by Peng Cheng Laboratory.

XiangShan is licensed under [Mulan PSL v2](LICENSE).
