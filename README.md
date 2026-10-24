# AeroWeather Cosmonautics Patch

**Version: 0.0.1 — EXPERIMENTAL / NOT YET TESTED IN-GAME**

A patched AeroWeather build that prevents AeroWeather's Aeronautics wind-force integration from applying atmospheric wind forces in Create: Cosmonautics' Moon and deep-space dimensions.

## What it changes

The patch adds an early return to `AeronauticsWindForceApplier.applyWindForce(...)` when the active server level is either `rocketnautics:deep_space` or `rocketnautics:moon`.

- Wind forces remain enabled in other dimensions, including the Overworld.
- Both Cosmonautics dimensions are excluded: the Moon and deep space.
- It does not intentionally change rocket thrust, gravity, drag, or Cosmonautics' own physics.

## Experimental status

The patched source passed `git apply --check` and the GitHub Actions Gradle build completed successfully. **This build has not yet been tested in-game.** Treat it as experimental, back up your server and client files, and report any issues before using it in a long-running world.

Built against the upstream AeroWeather source available when version 0.0.1 was built, targeting Minecraft 1.21.1 / NeoForge. Confirm compatibility with the exact modpack and loader version you run.

## Installation on a dedicated server

1. **Stop the server completely.**
2. Back up the world, server configuration, and current `mods` folder.
3. Download `aeroweather-1.6.4.jar` from the v0.0.1 release assets (or extract it from the GitHub Actions artifact if the release asset is not available).
4. In the server's `mods` directory, remove or move out the original AeroWeather JAR. **Do not keep both the original and patched AeroWeather JARs installed**, as that can load duplicate mod classes.
5. Put the patched `aeroweather-1.6.4.jar` into the server's `mods` directory.
6. Start the server and inspect the startup log for mod-loading errors.
7. Join with a client using the same Minecraft / NeoForge / modpack versions and the matching AeroWeather version. If AeroWeather is installed on clients in your pack, replace the client JAR with the same patched build too, so client and server mod files match.
8. Test a contraption in the Moon and deep space, then test the Overworld to confirm normal wind still works. If anything crashes or behaves unexpectedly, stop the server and restore the backed-up original JAR.

Do not replace the JAR while the server is running. Follow the requirements of your modpack and server host if they differ.

## Building from source

### Linux / macOS

```bash
git clone --depth 1 https://github.com/PostMalloy/AeroWeather.git
cd AeroWeather
curl -L -o disable-wind-in-space.patch https://raw.githubusercontent.com/TheBee-3328/AeroWeather-cosmonautics-patch/main/patches/disable-wind-in-deep-space.patch
git apply --check disable-wind-in-space.patch
git apply disable-wind-in-space.patch
./gradlew build
```

### Windows PowerShell

```powershell
git clone --depth 1 https://github.com/PostMalloy/AeroWeather.git
Set-Location AeroWeather
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/TheBee-3328/AeroWeather-cosmonautics-patch/main/patches/disable-wind-in-deep-space.patch" -OutFile "disable-wind-in-space.patch"
git apply --check disable-wind-in-space.patch
git apply disable-wind-in-space.patch
.\gradlew.bat build
```

The built mod JAR will be in `build/libs/`. Use the JAR produced by your modified build instead of the original AeroWeather JAR; do not install both simultaneously.

If `git apply --check` fails, the AeroWeather source version has changed and the patch needs to be rebased against that version.

## License

This patch modifies AeroWeather source. AeroWeather is licensed under the MIT License; preserve the upstream license and notices when redistributing modified source or binaries.
