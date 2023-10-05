# MiTail by Tail Company - protocol & research

## TODO
- Reverse-engineering of the firmware
    - Useful tools:
        - [Working bin2elf converter](https://github.com/yawor/esp32_image_parser/tree/app_image) (plus [this patch](https://github.com/tenable/esp32_image_parser/pull/11.patch))
        - [Working Ghidra disassembler/decompiler plugin](https://github.com/Ebiroll/ghidra-xtensa)

## Firmware
Last firmware info available [here](https://thetailcompany.com/fw/mitail).
Version as of writing - 4.0.11, md5: `27311fac5443d865a5d2ac2db6de38db`

## Mobile applications
- Android - written in Qt5 (whyyy ;_;), https://github.com/OpenTails/CRUMPET-Android
- iOS - written in Swift, can't say much

<details>
    <summary>just use https://github.com/OpenTails/CRUMPET-Android/wiki/Tail-Command-Protocol, idk why i didn't google for that</summary>

## Services:
- `0x1800` - Generic Access
    - `0x2A00` - Device Name; READ; `mitail`
    - `0x2A01` - Appearence; READ; `0`?
- `0x1801` - Generic Attribute
    - `0x2A05` - Service Changed; INDICATE
- `3af2108b-d066-42da-a7d4-55648fa0a9b6`
    - `c6612b64-0087-4974-939e-68968ef294b0` - Command responses; NOTIFY, READ; `TAILS1 END`/`TAILS1 BEGIN`
    - `5bfd6484-ddee-4723-bfe6-b653372bbfd6` - Command requests; INDICATE, WRITE; `TAILS1`
- `0x180F` - Battery Service
    - `0x2A19` - Battery Level; NOTIFY, READ; `0x4D` (77%)
    - `b08fed02-0584-40ef-b006-aff7e0d24e13` - Battery Voltage; NOTIFY, READ; `0x8F1E` (?)
    - `5073792e-4fc0-45a0-b0a5-78b6c1756c91` - Charging state; NOTIFY, READ; `CHARGE OFF`/`CHARGE FULL`/`CHARGE ON` (or `CHARGING`?)

## Commands
- `TAILS1` - Slow wag 1
- `TAILS2` - Slow wag 2
- `TAILS3` - Slow wag 3
- `TAILEP` - High Wag
- `TAILER` - Stand Up!
- `TAILET` - Tremble Erect
- `TAILFA` - Fast wag
- `TAILHA` - Happy wag
- `TAILHM` - Home Position
- `TAILSH` - Short wag
- `TAILT1` - Tremble 1
- `TAILT2` - Tremble 2
- `TAILU1`/`TAILU2`/`TAILU3`/`TAILU4` - user presets
- `VERA` - Request firmware version
    - Response: `VER 4.0.11 GT0`
- `SHUTDOWN` - Power off the gear
- `LEDOFF` - Stop Lights (for Glow Tip)
- `PING` - responds with `PONG`
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
- `SPEED SLOW`/`SPEED FAST` - commands for EarGear, "Be Calm"/"Be Excited"

### Unknown commands (found in firmware):
- `USERMOVE`
- `USERLEDS`
- `LOWBATT` - not sure if this is an actual command
- `OTA`
- `HWVER`
- `GLOWTIP TRUE`/`GLOWTIP FALSE` - probably toggles the glowing tip of the tail, can't test due to the model that doesn't have one
- `TASKU`
- `STOPNPM`
- `CONFRD` - reading the configuration
- `CONFWR` - writing the configuration
    - Configuration: `Received config: ver %hhu, minsToSleep %hhu, minsToNPM %hhu, minNPMPauseSec %hhu, maxNPMPauseSec %hhu, groupsNPM %hhu.` - what does NPM stand for?

</details>
