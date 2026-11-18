<h1 align="center">Preheat</h1>
<p align="center">
  Compiles your games' shaders into your GPU driver's cache before you play, so the game doesn't stop to compile them
  mid-game. Free and open source, for Windows.
</p>

<p align="center">
  <a href="LICENSE"><img alt="Licence: GPL-3.0-or-later" src="https://img.shields.io/badge/licence-GPL--3.0--or--later-blue"></a>
</p>

> [!IMPORTANT]
> **Preheat is an unofficial fork of [SCSKiller](https://github.com/BlueHeisenberg/SCSKiller)** (Shader Compilation
> Stutter Killer) by BlueHeisenberg. It is not made, checked or endorsed by SCSKiller's author. Preheat's builds, bugs
> and anti-cheat behaviour are this fork's own, so please report them [here](https://github.com/Joshspeakman/SCSKiller/issues),
> never to SCSKiller. Official SCSKiller builds come only from
> [SCSKiller's Releases](https://github.com/BlueHeisenberg/SCSKiller/releases).

## Why

A game that meets a new effect has the GPU driver compile its shader on the spot, and the frame waits: that's shader
compilation stutter. Preheat reads the shaders a game ships with, works out the pipelines it will build, and compiles
them into the driver's cache ahead of time, in its own process with the game closed.

## Results

Preheat publishes no measurements of its own yet. Preheat's measured results are in
[Preheat's README](https://github.com/BlueHeisenberg/Preheat#results); they are Preheat's, not Preheat's.

## Features

- **NVIDIA and AMD**, DirectX 12 games, and DirectX 11 games on NVIDIA.
- **Finds your games** in Steam, Epic Games, EA app, GOG, Ubisoft Connect, Xbox (PC), Battle.net, PURPLE, HoYoPlay,
  Gaijin and the Riot Client, plus games you add yourself.
- **Puts games known to stutter on top**, with the reason, and marks games whose engine prepares its shaders itself.
- **Compiles again after a driver update**, which clears the shader cache, on its own if you let it.
- **Optional recorder** for games whose pipelines its files don't give: play a few minutes with it on, then compile. It
  also records alongside a mod that replaces shaders.
- **Frame times per session**: with the recorder on, a game's page graphs your last session and marks shader stutters
  apart from other hitches. They stay on your PC.
- **Play button** that starts the game through its store.
- **Community shader hash database** for Patreon supporters: other players' recordings, so your games are covered
  without recording them first. Sharing yours is opt-in, anonymous and hash-only.
- **Leaves anti-cheat games alone** beyond reading their files: no launching, no injecting, no recorder, except in a
  session you allow per game and confirm every launch, at your own risk: without EasyAntiCheat for ELDEN RING and
  ARMORED CORE VI, or in games with anti-cheat once you turn on "Allow the recorder in games with anti-cheat (at your own
  risk)".

## Install

| Requirement | |
|---|---|
| OS | Windows 10 (version 2004) or 11, 64-bit |
| GPU | NVIDIA or AMD |
| Games | DirectX 12, DirectX 11 on NVIDIA |

Intel GPUs aren't supported yet.

Preheat has no releases yet: build it from source (below). `build/publish.ps1` makes a portable folder; run
`Preheat.exe` from it. Preheat keeps its settings and data in `%LOCALAPPDATA%\Preheat\` (a portable copy: a `data`
folder beside the exe), separate from an official Preheat, so both can be installed side by side. Preheat doesn't update
itself: Preheat's updates are signed for Preheat and would replace Preheat with it, so updating is turned off. Get a new
version from this repository. Turn recording off for your games before you delete Preheat, so the recorder leaves the game
folders.

## How to use it

1. **Open Preheat.** It finds your games and the shaders they ship with.
2. **Queue games and press Compile.** "Add all recommended" is a good start. Keep the game closed while it compiles.
3. **Play**, from your store or with the Play button. Preheat can be closed. Left open, it checks that the compile
   reached the cache the game really uses, and with the recorder on, the game's page shows your session's frame times
   and anything that still compiled.

If a game needs a recording, turn on **Record**, play it for a few minutes, then compile it.


## FAQ

**Can I get banned?** Preheat only reads the files of games with anti-cheat and adds its recorder to them only in a
session you allow and confirm (next question). Its anti-cheat check can still miss a game, so you use Preheat at your
own risk, and its authors are not responsible for bans, crashes or lost data.

**Is it safe with anti-cheat games?** Outside a session Preheat never launches them, injects into them or gives them
the recorder. It only reads their files. A session is allowed per game, confirmed every launch, and at your own risk.
The offline session for ELDEN RING and ARMORED CORE VI runs them offline without EasyAntiCheat when their exe is
started directly: Steam must be running (offline mode is fine), and Preheat adds `d3d12.dll`, `scskiller.cfg` and
`steam_appid.txt` to the game's folder and starts the exe itself. With "Allow the recorder in games with anti-cheat (at
your own risk)" on in Settings, any other supported game can run a session too: Preheat starts the game as usual, with
`d3d12.dll` and `scskiller.cfg` in its folder. Enabling the recorder in games with anti-cheat is at your own risk.
Preheat isn't responsible for bans. Bans from it are not support issues. In both kinds the recorder records
only that process. When the game exits, Preheat takes those files out again (each only while it is still the file it
added) and keeps the recording and the session's frame times, at the next logon or start if Preheat was closed or the
PC crashed. If those files are still there when you start the game online, you could be banned. Don't uninstall
Preheat while the game runs.

**What does it write, and where?** Settings and per-game plans go in `%LOCALAPPDATA%\Preheat\` (the `data` folder of
a portable copy), and the compiled pipelines go in your driver's own shader cache. Game files are never modified. The
optional recorder adds `d3d12.dll` and `scskiller.cfg` to the folder of a game you turn it on for, and turning it off
removes exactly those files. On a new install it goes in no game folder until you close the welcome, whose box sets "Record in all compatible games". It never goes into a game with anti-cheat, and comes out the moment Preheat finds
anti-cheat: when it scans, when the game exits or updates, and every 2 minutes while it runs. `scskiller.cfg` names the
game's exe as it was when Preheat last found no anti-cheat in its folders, and a game records only while its exe is
still that one and no anti-cheat is next to it. Uninstalling Preheat removes these files and the recordings from every
game folder, and a scan removes them from a game Steam uninstalled.

**Does it touch my drivers or their settings?** No. It compiles through DirectX, as the game would.

**Do I need an account?** No. Everything the app does on your PC is free. Signing in with Patreon adds the supporter
features.

**My game isn't detected, or something broke.** Open an [issue on Preheat](https://github.com/Joshspeakman/SCSKiller/issues). Please don't
report Preheat problems to SCSKiller.

## SCSKiller's online features

Preheat keeps SCSKiller's online parts as they are: its planning rules and news feed, and the community shader hash
database for SCSKiller's Patreon supporters, all served by SCSKiller's servers. Preheat names itself to those servers
as Preheat. Support for them belongs to SCSKiller; [SCSKiller's Patreon](https://www.patreon.com/SCSKiller) pays for them.

## Build from source

Visual Studio 2022 (C++ desktop workload with CMake) and the .NET 10 SDK:

```
cmake -S proxy -B proxy/build -A x64
cmake --build proxy/build --config Release
dotnet build SCSKiller.slnx -c Release
```

`build/publish.ps1` builds the distribution into `dist\`. Design: [ARCHITECTURE.md](ARCHITECTURE.md). Contributing:
[CONTRIBUTING.md](CONTRIBUTING.md). Changes: [CHANGELOG.md](CHANGELOG.md). Security issues go through
[SECURITY.md](SECURITY.md), never a public issue.

## Links

- Preheat: https://github.com/Joshspeakman/SCSKiller
- SCSKiller (the original, official builds): https://github.com/BlueHeisenberg/SCSKiller

## Licence

GPL-3.0-or-later ([LICENSE](LICENSE)), with an additional permission for Oodle, the Windows App SDK and graphics driver
libraries ([LICENSE-EXCEPTION.txt](LICENSE-EXCEPTION.txt)). Third-party components:
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md). Code signing: [CODE_SIGNING_POLICY.md](CODE_SIGNING_POLICY.md).

Not affiliated with any GPU maker, engine maker or game publisher. All product names are trademarks of their owners.

### Forks

Preheat is a fork of SCSKiller, Copyright (C) 2026 The SCSKiller authors, under GPL-3.0-or-later; every
SCSKiller copyright notice is kept. SCSKiller's own fork request, which Preheat follows: give a fork its own name, say
it's unofficial and based on SCSKiller, keep the SCSKiller copyright notices, and don't present SCSKiller's measurements
and screenshots as the fork's. A fork's builds, bugs and anti-cheat behaviour are its author's: SCSKiller keeps its
recorder out of anti-cheat games except in a session the user confirms, and can't vouch for a fork that changes that.
Preheat doesn't change that behaviour.

If you fork Preheat, please do the same for both projects. Improvements that fit SCSKiller belong upstream as pull
requests to [SCSKiller](https://github.com/BlueHeisenberg/SCSKiller).
