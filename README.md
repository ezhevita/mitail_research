# MiTail by Tail Company - protocol & research
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
- `TAILU1`
- `TAILU2`
- `TAILU3`
- `TAILU4`

## Handles:
- `0x000C` - begin/end notifications
- `0x000F` - command
- `0x0013` - battery, in decimal %

## Services:
- `0x1800` - Generic Access
    - `0x2A00` - Device Name; READ; `mitail`
    - `0x2A01` - Appearence; READ; `0`?
- `0x1801` - Generic Attribute
    - `0x2A05` - Service Changed; INDICATE
        - `0x2902` - Client Characteristic Configuration Descriptor
- `3af2108b-d066-42da-a7d4-55648fa0a9b6`
    - `c6612b64-0087-4974-939e-68968ef294b0` - NOTIFY, READ; `TAILS1 END`/`TAILS1 BEGIN`
        - `0x2902` - Client Characteristic Configuration Descriptor
    - `5bfd6484-ddee-4723-bfe6-b653372bbfd6` - INDICATE, WRITE; `TAILS1`
        - `0x2902` - Client Characteristic Configuration Descriptor
- `0x180F` - Battery Service
    - `0x2A19` - Battery Level; NOTIFY, READ; `0x4D` (77%)
        - `0x2902` - Client Characteristic Configuration Descriptor
        - `0x2901` - Characteristic User Description
    - `b08fed02-0584-40ef-b006-aff7e0d24e13` - Battery Voltage; NOTIFY, READ; `0x8F1E` (?)
        - `0x2902` - Client Characteristic Configuration Descriptor
        - `0x2901` - Characteristic User Description
    - `5073792e-4fc0-45a0-b0a5-78b6c1756c91` - Charging state; NOTIFY, READ; `CHARGE OFF`/`CHARGE COMPLETE`/`CHARGE ON`
        - `0x2902` - Client Characteristic Configuration Descriptor
        - `0x2901` - Characteristic User Description

## Firmware
Last firmware info available [here](https://thetailcompany.com/fw/mitail).
Version as of writing - 4.0.11, md5: `27311fac5443d865a5d2ac2db6de38db`
