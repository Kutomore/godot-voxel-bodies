# Godot Voxel Bodies

Bodies made of voxels for Godot 4, in GDScript, that move by contracting their own voxels.

The idea:

- A body is a shape of voxels of three kinds: external (the outer layer), internal (the voxels that contract) and solid (the rigid segments the internal voxels pull on). Each voxel has a material, defined by the game as data, that says how strong or resistant it is.
- Movement comes from groups of internal voxels contracting, not from an animation or a velocity set from outside. The library ships the gait: it decides which groups contract and when. Four-legged bodies come first, two-legged ones later.
- Voxels can be removed. A group that has lost internal voxels pulls less, so what the body can still do follows from what is left of it.
- The library reports how much of a body's inside is exposed (internal and solid voxels with a face open to the air), so a game can build its own rules on that number.

What it does not do: it has no concept of damage, health, blood or death, in the same way a `RigidBody3D` has none. Deciding what a hit removes, and what an exposed inside costs, is the game's job.

**Status: nothing is built yet.** This repository holds the project skeleton and the test framework only.

## Requirements

- Godot 4, GDScript. Set up on Godot 4.7.2.
- The tests use [gdUnit4](https://github.com/MikeSchulze/gdUnit4) 6.2.1, vendored under `addons/gdUnit4`.

## Layout

```
addons/voxel_bodies/   the library (empty for now)
addons/gdUnit4/        test framework (third party, MIT), only needed for tests
tests/                 gdUnit4 suites
```

## Tests

Once after cloning, let Godot build its class cache:

```
godot --headless --path . --import
```

Run the tests (exit code 0 when green):

```
godot --headless --path . -s res://addons/gdUnit4/bin/GdUnitCmdTool.gd --ignoreHeadlessMode -c -a res://tests -rd res://reports
```

## Licence

MIT, see [LICENSE](LICENSE). gdUnit4 under `addons/gdUnit4` is by Mike Schulze, also MIT; its licence is in that folder.
