# AeroWeather Cosmonautics Patch

A small source patch for AeroWeather that prevents its Aeronautics/Sable wind-force integration from pushing contraptions in Create: Cosmonautics' Moon and deep-space dimensions.

## What it changes

The patch adds an early return to `AeronauticsWindForceApplier.applyWindForce(...)` when the active server level is either `rocketnautics:deep_space` or `rocketnautics:moon`.

- Wind forces remain enabled in other dimensions, including the Overworld.
- Both Cosmonautics dimensions are excluded: the Moon and deep space.
- It does not change rocket thrust, gravity, drag, or Cosmonautics' own physics.
- It is a source patch, not a ready-to-install JAR.

## Apply it

Use the AeroWeather source repository and apply the patch before building.

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

## Validation status

The unified diff was checked against a fixture containing the exact target method context and applied successfully with `git apply --check` and `git apply`. A full Gradle build and an in-game test have **not** been run in this environment, so the resulting JAR is not yet verified.

Designed for the AeroWeather source layout with Minecraft 1.21.1 and NeoForge.

## License

This patch modifies AeroWeather source. AeroWeather is licensed under the MIT License; preserve the upstream license and notices when redistributing modified source or binaries.
