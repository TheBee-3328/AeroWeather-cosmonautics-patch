# AeroWeather Cosmonautics Patch

A small source patch for AeroWeather that prevents its Aeronautics/Sable wind-force integration from pushing contraptions in Create: Cosmonautics' deep-space dimension.

## What it changes

The patch adds an early return to `AeronauticsWindForceApplier.applyWindForce(...)` when the active server level is `rocketnautics:deep_space`.

- Wind forces remain enabled in other dimensions.
- It targets the deep-space dimension ID used by Create: Cosmonautics.
- It does not change rocket thrust, gravity, drag, or Cosmonautics' own physics.
- It does not automatically disable wind on the Moon or other planetary dimensions.

## Apply it

This is a **source patch**, not a ready-to-install JAR. Apply it to an AeroWeather source checkout:

```bash
git clone https://github.com/PostMalloy/AeroWeather.git
cd AeroWeather
git checkout master
git apply --check https://raw.githubusercontent.com/TheBee-3328/AeroWeather-cosmonautics-patch/main/patches/disable-wind-in-deep-space.patch
git apply https://raw.githubusercontent.com/TheBee-3328/AeroWeather-cosmonautics-patch/main/patches/disable-wind-in-deep-space.patch
./gradlew build
```

On Windows, use `gradlew.bat build` for the final command. The built JAR will be in `build/libs/`.

If `git apply --check` fails, the upstream source has changed and the patch needs to be rebased against the AeroWeather version you have.

## Compatibility

Designed for the AeroWeather source layout containing `AeronauticsWindForceApplier.java`, Minecraft 1.21.1, and NeoForge. It has not yet been verified in a live Minecraft instance. Test it in a copied instance/world before using it in a main world.

## License

The patch is a modification to AeroWeather source. AeroWeather is licensed under the MIT License; preserve the upstream license and notices when redistributing modified source or binaries.
