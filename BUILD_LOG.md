# doomcat Build & Test Log

## Build Environment
- OS: Ubuntu 22.04 LTS
- Build Date: 2026-03-03
- Chocolate Doom Version: 3.1.0

## Build Commands

```bash
# Install dependencies
sudo apt install -y build-essential cmake libsdl2-dev libsdl2-mixer-dev \
                     libsdl2-net-dev libpng-dev libsamplerate-dev libfluidsynth-dev

# Build
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
```

## Build Output

Built binaries:
- `chocolate-doom` (1.1MB) - DOOM executable
- `chocolate-heretic` (1.1MB) - Heretic executable
- `chocolate-hexen` (1.3MB) - Hexen executable
- `chocolate-strife` (1.1MB) - Strife executable
- `chocolate-server` (154KB) - Dedicated server
- `chocolate-setup` (392KB) - Setup utility

## Proof of Concept: Demo Playback Test

Tested with Freedoom 0.13.0 WAD:

```bash
xvfb-run -a ./build/src/chocolate-doom \
    -iwad /tmp/freedoom-0.13.0/freedoom1.wad \
    -nosound -timedemo demo1
```

### Result:

```
DEHACKED:549: warning: Cheat sequence longer than supported by Vanilla dehacked
timed 7117 gametics in 303 realtics (822.095703 fps)
```

**Analysis:**
- 7117 gametics processed = ~203 seconds of gameplay at 35 tics/sec
- Processed in 303 realtics (display tics) at 822+ FPS
- Demo completed successfully
- Engine correctly loaded and executed game logic
- WAD parsed, levels accessible, rendering functional

## Run Commands

### With Freedoom (Free WAD):

```bash
# Download Freedoom
wget https://github.com/freedoom/freedoom/releases/download/v0.13.0/freedoom-0.13.0.zip
unzip freedoom-0.13.0.zip

# Play DOOM: Phase 1 (Freedoom)
./build/src/chocolate-doom -iwad freedoom-0.13.0/freedoom1.wad

# Play DOOM: Phase 2 (Freedoom)
./build/src/chocolate-doom -iwad freedoom-0.13.0/freedoom2.wad
```

### With Commercial DOOM WAD:

```bash
# Play DOOM (shareware or registered)
./build/src/chocolate-doom -iwad doom.wad

# Play DOOM II
./build/src/chocolate-doom -iwad doom2.wad

# Play Ultimate DOOM
./build/src/chocolate-doom -iwad doom.wad

# Jump to specific level (E1M1)
./build/src/chocolate-doom -iwad doom.wad -warp 1 1

# Play demo for benchmarking
./build/src/chocolate-doom -iwad doom.wad -timedemo demo1
```

## Build Status

✅ **SUCCESS** - doomcat builds cleanly on Ubuntu 22.04
✅ **SUCCESS** - Engine executes and processes game logic
✅ **SUCCESS** - WAD loading functional (Freedoom validated)
✅ **SUCCESS** - Demo playback completes successfully