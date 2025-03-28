# OptiScaler: Custom Upscaling and Frame Generation for Games

![opti-logo](https://github.com/user-attachments/assets/c7dad5da-0b29-4710-8a57-b58e4e407abd)

## Table of Contents

1. [About](#about)
2. [How It Works](#how-it-works)
3. [Supported APIs and Upscalers](#supported-apis-and-upscalers)
4. [Installation](#installation)
5. [Known Issues](#known-issues)
6. [Compilation and Credits](#compilation)
7. [Wiki](https://github.com/cdozdil/OptiScaler/wiki)

---

## About

OptiScaler enables replacement of built-in DLSS, FSR, or XeSS upscalers in games, allows for optional frame generation, and provides extensive customization options for all GPU users. For example, it can replace DLSS with FSR, or replace FSR with XESS.

**Key Features:**

- Enables XeSS, FSR2, FSR3, FSR4$`^2`$, and DLSS in games with existing upscaler support.
- Allows fine-tuning of upscaling parameters (RCAS & MAS, output scaling, DLSS presets, ratio & DRS overrides, etc.).
- Offers experimental frame generation with HUD ghosting fixes via [**OptiFG**](#optifg-powered-by-fsr3-fg--hudfix-experimental-hud-ghosting-fix).
- Integrates with [**Fakenvapi**](#fakenvapi) for Reflex hooking and Anti-Lag 2/LatencyFlex injection (RDNA1+ only). _Not included_$^3$.
- Supports Nukem's FSR frame generation mod [**dlssg-to-fsr3**](#nukems-dlssg-to-fsr3). _Not included_$^3$.

See [the full feature list](Features.md) for more details.

---

## IGNORE BELOW HERE

---

> [!IMPORTANT]
> Always check the [Wiki Compatibility List](https://github.com/cdozdil/OptiScaler/wiki) for known game issues and workarounds.
> 
> Refer to [OptiScaler Known Issues](#known-issues) for RTSS compatibility notes.

> [!NOTE]
>
> <details>
>  <summary><b>Expand for [1], [2], and [3]</b></summary>
>
> **_[1] XeSS Caveats:_** Unreal Engine's XeSS plugin lacks depth support, so replacing in-game XeSS may break other upscalers (e.g., Redout 2). RCAS sharpening can still reduce blur in UE games.
> **_FSR Inputs:_** FSR 3.1 is fully standardized, but FSR2/3 support depends on game-specific implementations. Unreal Engine games may require [INI tweaks](https://github.com/cdozdil/OptiScaler/wiki/Unreal-Engine-Tweaks).
>
> **_[2] FSR4 Support:_** Preliminary support added via Nightly builds. Check the [FSR4 Compatibility List](https://github.com/cdozdil/OptiScaler/wiki/FSR4-Compatibility-List).
>
> **_[3] Non-Bundled Items:_** See [Installation](#installation) for setup instructions.
>
> </details>

---

## Official Discord Server: [DLSS2FSR](https://discord.gg/2JDHx6kcXB)

_Based on [PotatoOfDoom](https://github.com/PotatoOfDoom)'s [CyberFSR2](https://github.com/PotatoOfDoom/CyberFSR2)._

---

## How It Works

OptiScaler acts as middleware by intercepting game API calls (DLSS2+, NVAPI, XeSS, FSR2+) and redirecting them to the selected upscaling backend. This allows swapping in-game upscalers with alternatives of your choice.

> [!NOTE]
> Press **`Insert`** in-game to open the OptiScaler **Overlay** (shortcut configurable via `OptiScaler.ini`).

![image](https://github.com/user-attachments/assets/e138c979-c5d9-499f-a89b-165bb7cfcb32)

---

## Supported APIs and Upscalers

OptiScaler supports **DirectX 11**, **DirectX 12**, and **Vulkan**, with varying upscaler options per API.
**[OptiFG](#optifg-powered-by-fsr3-fg--hudfix-experimental-hud-ghosting-fix)** is **DX12-only** and detailed separately.

#### DirectX 12

- XeSS (Default)
- FSR2 2.1.2, 2.2.1
- FSR3 3.1 (and FSR2 2.3.2)
- DLSS
- FSR4 (Preliminary)

#### DirectX 11

- FSR2 2.2.1 (Default, native DX11)
- FSR3 3.1.2 (unofficial DX11 port)
- XeSS 1.x, FSR2 2.1.2/2.2.1, FSR3 3.1, FSR2 2.3.2 (via DX12 backend)$`^1`$
- DLSS (native DX11)
- XeSS 2.x (Intel ARC only)

> [!NOTE]
>
> <details>
>  <summary><b>Expand for [1]</b></summary>
>
> _**[1]** DX12 backend incurs a 10-15% performance penalty. Native DX11 FSR 2.2.1 is a Unity backport with partial fixes. **Not supported on Linux** (causes black screen)._
>
> </details>

#### Vulkan

- FSR2 2.1.2 (Default), 2.2.1
- FSR3 3.1 (and FSR2 2.3.2)
- DLSS
- XeSS 2.x

#### OptiFG (FSR3 FG + HUDfix)

Enabled via `FGType=optifg` in `OptiScaler.ini`. **Experimental** and requires HUDless resource detection to avoid ghosting. Compatibility varies per game. Check the [Wiki](https://github.com/cdozdil/OptiScaler/wiki) for incompatible titles.

---

## Installation

> [!CAUTION] > _**Do not use this mod with online games.** It may trigger anti-cheat systems and result in bans!_

> [!IMPORTANT] > **_Use [Nightly builds](https://github.com/cdozdil/OptiScaler/releases/tag/nightly) for the latest features._** > _Debug logging is enabled by default in Nightly builds. Disable it by setting `LogFile=` in `OptiScaler.ini`._

---

### Automated Setup

1. Extract **all** OptiScaler files **next to the game executable** (e.g., `Win64` folder for Unreal Engine games).
2. Run `OptiScaler Setup.bat` for automated renaming.
3. If unsuccessful, follow **Manual** steps below.

---

### Manual Setup

#### Nvidia GPUs

1. Extract files next to the game executable.
2. Rename `OptiScaler.dll` (or `nvngx.dll` in older versions) to a [supported filename](#supported-filenames) (prefer `dxgi.dll`).

> [!NOTE] > _For FSR2/3-only games (e.g., The Callisto Protocol), download `nvngx_dlss.dll` from [TechPowerUp](https://www.techpowerup.com/download/nvidia-dlss-dll/) or [Streamline SDK](https://github.com/NVIDIAGameWorks/Streamline/tree/main/bin/x64)._

#### AMD/Intel GPUs

1. Extract files next to the game executable.
2. Rename `OptiScaler.dll` (or `nvngx.dll` in older versions) to a [supported filename](#supported-filenames).
3. **Either:**
   - Locate `nvngx_dlss.dll` in the game folder, duplicate it as `nvngx.dll`, and place it next to OptiScaler.
   - **Or:** Download `nvngx_dlss.dll`, rename to `nvngx.dll`, and place it next to OptiScaler.

![Installation Example](https://github.com/user-attachments/assets/977a2a68-d117-42ea-a928-78ec43eedd28)

---

#### Nukem's dlssg-to-fsr3

1. Download from [NexusMods](https://www.nexusmods.com/site/mods/738) or [GitHub](https://github.com/Nukem9/dlssg-to-fsr3).
2. Place `dlssg_to_fsr3_amd_is_better.dll` next to OptiScaler and set `FGType=nukems` in `OptiScaler.ini`.
3. **AMD/Intel users:** Install [Fakenvapi](#fakenvapi) to expose DLSS FG.

---

#### Fakenvapi

1. Download [Fakenvapi](https://github.com/FakeMichau/fakenvapi).
2. Place `nvapi64.dll` and `fakenvapi.ini` next to OptiScaler.

> [!NOTE] > **Anti-Lag 2** works only on RDNA GPUs (Windows). Verify functionality via [Anti-Lag 2 SDK](https://github.com/GPUOpen-LibrariesAndSDKs/AntiLag2-SDK?tab=readme-ov-file#testing). **Latency Flex** is cross-vendor.

---

> [!TIP] > **Linux Users:** Add DLL override via:
>
> ```
> WINEDLLOVERRIDES=dxgi=n,b %COMMAND%
> ```

> [!IMPORTANT] > **Do not rename `OptiScaler.ini`.**

#### Supported Filenames

- `dxgi.dll` (preferred)
- `winmm.dll`
- `dbghelp.dll` (Nightly only)
- `version.dll`
- `wininet.dll`
- `winhttp.dll`
- `OptiScaler.asi` (requires ASI loader)

---

> [!NOTE] > **Reshade Compatibility:**
>
> - Place conflicting mods (e.g., Reshade) in a `plugins` subfolder.
> - **Or:** Rename Reshade to `ReShade64.dll` and set `LoadReshade=true` in `OptiScaler.ini`.

![Reshade Setup](https://github.com/cdozdil/OptiScaler/assets/35529761/c4bf2a85-107b-49ac-b002-59d00fd06982)

---

### Legacy Installation (Deprecated)

<details>
  <summary><b>Click to Expand</b></summary>

1. Download the [latest release](https://github.com/cdozdil/OptiScaler/releases).
2. Extract files next to the game executable.
3. Rename `OptiScaler.dll` to `nvngx.dll`.
4. Merge `EnableSignatureOverride.reg` (from `DlssOverrides` folder).

_Note: Overwrites existing `libxess.dll` files. Backup if needed._

</details>

---

### Updating OptiScaler with DLSS Enabler

1. Delete `dlss-enabler-upscaler.dll`.
2. Extract new `OptiScaler.dll` and rename it to `dlss-enabler-upscaler.dll`.
3. Copy the renamed file to the game folder.

---

## Uninstallation

1. Run `DisableSignatureOverride.reg`.
2. Delete:
   - `OptiScaler.dll`/`nvngx.dll`, `OptiScaler.ini`
   - `fakenvapi.ini`, `nvapi64.dll`, `dlssg_to_fsr3` files (if used).
3. Restore original `libxess.dll` or `amd_fidelityfx` files if overwritten.

---

## Configuration

See [Config.md](Config.md) for parameters. Non-Nvidia users: Check [Spoofing.md](Spoofing.md) _(WIP)_.

---

## Known Issues

**In-Game Overlay Not Opening?**

1. Ensure DLSS/XeSS/FSR is enabled in-game.
2. Open the overlay during active 3D rendering (legacy installs).
3. **RTSS Users:** Enable "Detect incompatible 3D APIs" in RTSS or update it. Disable RTSS when using OptiFG.

![RTSS Fix](https://github.com/cdozdil/OptiScaler/assets/35529761/8afb24ac-662a-40ae-a97c-837369e03fc7)

For other issues, refer to [Issues.md](Issues.md) and the [Wiki](https://github.com/cdozdil/OptiScaler/wiki).

---

## Compilation

### Requirements

- Visual Studio 2022

### Steps

1. Clone the repo with submodules.
2. Open `OptiScaler.sln` in Visual Studio 2022.
3. Build the solution.

---

## Credits

- **@PotatoOfDoom** for CyberFSR2.
- **@Artur** for DLSS Enabler integration.
- **@LukeFZ**, **@Nukem**, **@FakeMichau** for modding expertise.
- **@QM**, **@TheRazerMD**, **@Cryio**, and others for testing.
- **DLSS2FSR Community** for support and [compatibility matrix](https://docs.google.com/spreadsheets/d/1qsvM0uRW-RgAYsOVprDWK2sjCqHnd_1teYAx00_TwUY).

**Licensing:** Uses [FreeType](https://gitlab.freedesktop.org/freetype/freetype) under [FTL](https://gitlab.freedesktop.org/freetype/freetype/-/blob/master/docs/FTL.TXT).

