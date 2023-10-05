# MiTail by Tail Company - protocol & research

## TODO
- Reverse-engineering of the firmware
    - Useful tools:
        - [Working bin2elf converter](https://github.com/yawor/esp32_image_parser/tree/app_image) (plus [this patch](https://github.com/tenable/esp32_image_parser/pull/11.patch))
        - [Working Ghidra disassembler/decompiler plugin](https://github.com/Ebiroll/ghidra-xtensa)
    - There are more commands in the firmware (not listed below), also potentially dangerous, like `FORMATNVS`

## Firmware
Last firmware info available [here](https://thetailcompany.com/fw/mitail).
Version as of writing - 4.0.11, md5: `27311fac5443d865a5d2ac2db6de38db`

## Services:
- `0x1800` - Generic Access
    - `0x2A00` - Device Name; READ; `mitail`
    - `0x2A01` - Appearence; READ; `0`?
- `0x1801` - Generic Attribute
    - `0x2A05` - Service Changed; INDICATE
- `3af2108b-d066-42da-a7d4-55648fa0a9b6`
    - `c6612b64-0087-4974-939e-68968ef294b0` - used for notifications about commands execution; NOTIFY, READ; `TAILS1 END`/`TAILS1 BEGIN`
    - `5bfd6484-ddee-4723-bfe6-b653372bbfd6` - used for sending commands; INDICATE, WRITE; `TAILS1`
- `0x180F` - Battery Service
    - `0x2A19` - Battery Level; NOTIFY, READ; `0x4D` (77%)
    - `b08fed02-0584-40ef-b006-aff7e0d24e13` - Battery Voltage; NOTIFY, READ; `0x8F1E` (?)
    - `5073792e-4fc0-45a0-b0a5-78b6c1756c91` - Charging state; NOTIFY, READ; `CHARGE OFF`/`CHARGE COMPLETE`/`CHARGE ON`

## Commands
- `TAILEP` - High Wag
- `TAILER` - Stand Up!
- `TAILET` - Tremble Erect
- `TAILFA` - Fast wag
- `TAILHA` - Happy wag
- `TAILS1` - Slow wag 1
- `TAILS2` - Slow wag 2
- `TAILS3` - Slow wag 3
- `TAILSH` - Short wag
- `TAILT1` - Tremble 1
- `TAILT2` - Tremble 2
- `VERA` - Request firmware version
    - Response: `VER 4.0.11 GT0`
- `SHUTDOWN` (or `UTDOWN`?) - Power off the gear
- `STOPAUTO` - Stop Casual Mode
- `AUTOMODE` - Start Casual Mode:
    - Example: `AUTOMODEG1 G2 G3 G4  T29 T98 T240`
    - G - categories, joined by space
        - `G1` - Calm and Relaxed
        - `G2` - Fast and Excited
        - `G3` - Frustrated and Tense
        - `G4` - EarGear Poses
    - T - timings
        - First - minimal pause
        - Second - maximum pause
        - Third - ?, seems to be constant, 240

## Unknown commands (found in firmware):
- `TAILHM`
- `TAILU1`/`TAILU2`/`TAILU3`/`TAILU4` - probably user presets, probably aren't used in the current app version
