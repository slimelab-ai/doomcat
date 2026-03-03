# doomcat 🐱

**doomcat** is a minimal, clean packaging of the complete DOOM engine based on Chocolate Doom. It preserves full WAD-based DOOM compatibility while providing a streamlined foundation for renderer experimentation.

> doomcat = DOOM + dcat (the renderer integration target)

## What is doomcat?

doomcat is a full, authentic DOOM source port that:
- Accurately reproduces the original DOS DOOM experience
- Plays all classic DOOM WAD files (DOOM, DOOM2, Ultimate DOOM, Final DOOM, etc.)
- Supports Heretic, Hexen, and Strife via the same codebase
- Uses WAD files for all game data (just like the original)

**This is the complete DOOM engine** - not a demo, not a subset. The real deal.

## Origins

doomcat is based on [Chocolate Doom](https://www.chocolate-doom.org/) with minimal modifications:
- Preserved all upstream DOOM compatibility
- Clean build system for easy integration
- Foundation for future renderer experiments (dcat)

## Building on Ubuntu

### Dependencies

```bash
sudo apt update
sudo apt install build-essential cmake libsdl2-dev libsdl2-mixer-dev \
                 libsdl2-net-dev libpng-dev libsamplerate-dev \
                 libfluidsynth-dev fluidsynth
```

### Build with CMake

```bash
mkdir build && cd build
cmake ..
make -j$(nproc)
```

### Build with Autotools (alternative)

```bash
autoreconf -fi
./configure
make -j$(nproc)
```

## Running doomcat

You need a DOOM WAD file to play. Options:

1. **Shareware DOOM** (free): `doom1.wad`
2. **Freedoom** (free replacement): [freedoom.github.io](https://freedoom.github.io/)
3. **Commercial WADs**: `doom.wad`, `doom2.wad`, etc.

```bash
# Play with a WAD file
./src/doomcat-doom -iwad /path/to/doom.wad

# Play E1M1 (Knee-Deep in the Dead)
./src/doomcat-doom -iwad /path/to/doom.wad -warp 1 1

# Play back a demo (for testing/benchmarking)
./src/doomcat-doom -iwad /path/to/doom.wad -playdemo demo1

# Timed demo playback (benchmark mode)
./src/doomcat-doom -iwad /path/to/doom.wad -timedemo demo1
```

## Proof of Concept: E1M1 Demo Playback

To validate the engine works correctly, you can run the built-in demo playback:

```bash
# Using shareware DOOM or Freedoom
./src/doomcat-doom -iwad /path/to/doom1.wad -timedemo demo1

# Expected output shows FPS and successful level completion
```

## Project Structure

```
doomcat/
├── src/           # Core game engine (C)
│   ├── doom/      # DOOM-specific code
│   ├── heretic/   # Heretic support
│   ├── hexen/     # Hexen support
│   └── strife/    # Strife support
├── opl/           # OPL audio emulation
├── pcsound/       # PC speaker sound
├── textscreen/    # Text-mode UI
└── data/          # Game data files
```

## What's Different from Chocolate Doom?

Minimal changes:
- Rebranding to "doomcat" for project identity
- Clean README for easy onboarding
- Build target renamed for clarity

Everything else is pure DOOM engine goodness.

## License

GNU General Public License v2 - see `COPYING.md`

## Credits

doomcat is derived from Chocolate Doom by Simon Howard and contributors.
Original DOOM by id Software.

## Links

- [Chocolate Doom](https://www.chocolate-doom.org/)
- [DOOM Wiki](https://doomwiki.org/)
- [Freedoom](https://freedoom.github.io/) - Free WAD alternative