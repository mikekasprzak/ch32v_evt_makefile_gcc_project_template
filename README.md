# WCH CH32V EVT with GCC and Makefile support

This project will generate a project and GCC Makefile for official WCH EVT packages.

It will extract the EVT packages and setup Link.ld according to your MCU. For ease of use, it bundles the CH32V EVT packages from WCH, including:

- [CH32V003EVT.ZIP](https://www.wch.cn/downloads/CH32V003EVT_ZIP.html) V2.0 2024-10-28
  + CH32V003J4M6
  + CH32V003A4M6
  + CH32V003F4U6
  + CH32V003F4P6
- [CH32X035EVT.ZIP](https://www.wch.cn/downloads/CH32X035EVT_ZIP.html) V1.8 2024-11-07
  + CH32X035R8T6
  + CH32X035C8T6
  + CH32X035G8U6
  + CH32X035G8R6
  + CH32X035F8U6
  + CH32X035F7P6
  + CH32X033F8P6
- [CH32V103EVT.ZIP](https://www.wch.cn/downloads/CH32V103EVT_ZIP.html) V2.6 2024-06-27
  + CH32V103C6T6
  + CH32V103C8U6
  + CH32V103C8T6
  + CH32V103R8T6
- [CH32V20xEVT.ZIP](https://www.wch.cn/downloads/CH32V20xEVT_ZIP.html) V2.2 2024-11-08
  + CH32V203F6P6
  + CH32V203G6U6
  + CH32V203K6T6
  + CH32V203C6T6
  + CH32V203F8P6
  + CH32V203F8U6
  + CH32V203G8R6
  + CH32V203K8T6
  + CH32V203C8T6
  + CH32V203C8U6
  + CH32V203RBT6
  + CH32V208GBU6
  + CH32V208CBU6
  + CH32V208RBT6
  + CH32V208WBU6
- [CH32V307EVT.ZIP](https://www.wch.cn/downloads/CH32V307EVT_ZIP.html) V2.7 2024-11-08
  + CH32V303CBT6
  + CH32V303RBT6
  + CH32V303RCT6
  + CH32V303VCT6
  + CH32V305FBP6
  + CH32V305RBT6
  + CH32V307RCT6
  + CH32V307WCU6
  + CH32V307VCT6
  + CH32V317xxxx
- [CH32V006EVT.ZIP](https://www.wch.cn/downloads/CH32V006EVT_ZIP.html) V1.4 2025-03-11
  + CH32V002xxxx
  + CH32V004xxxx
  + CH32V005xxxx
  + CH32V006xxxx
  + CH32V007xxxx
  + CH32M007xxxx

## Usage

This script assumes you have the MounRiver `riscv-none-embed-*` or a different `riscv-none-elf-*` toolchain installed and added to your path.
To generate the gcc/makefile project for a specific part, do the following:

```bash
./generate_project_from_evt.sh <part>
```
If you want to change to another part from same family after project generated, use `./setpart.sh <part>`.

If you do not know which part you should specify, run `./generate_project_from_evt.sh` without arguments for a list of supported parts.


The script will generate or extract the following files:

```bash
/Makefile                     # Makefile for building the project
/User/main.c                  # Main C file from the `GPIO_Toggle` example
/User/*                       # Other files from the `GPIO_Toggle` example
/Examples/*                   # All other examples found in the EVT package (NOTE: can ignore)
/CH32V_firmware_library/*     # Support library code for the current part
```

The basic `GPIO_Toggle` project is now setup, and can be found in the `/User/` folder. You should modify the `User` program to suit your part, 
if say the default pin used isn't available (i.e. a CH32V002A4M6 doesn't have an exposed D0 pin, so you might choose D4 instead).

Then type `make` to build the project.

The `<part>.elf` / `<part>.bin` / `<part>.hex` will be generated at 'build' dir and can be programmed to target device later.

Some helpful flashing commands are available. You can run `make isp` or `make wlink` to program the binary to the attached device, 
using the `wchisp` and `wlink` tools respectfully. It's assumed you have these tools installed and available in the path.

## Note

Please refer to [this tutorial](https://github.com/cjacker/opensource-toolchain-ch32v) to setup the ch32v dev environment.

And you must use [this latest WCH OpenOCD](https://github.com/cjacker/wch-openocd).
