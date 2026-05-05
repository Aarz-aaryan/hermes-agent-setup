# Pokemon Player — Headless Emulator + RAM Reads

## Concept
Play Pokemon games via a headless emulator (BizHawk, VBA-M, or DeSmuME) with RAM watch scripts for automation. The emulator runs without a display and scripts read/write memory directly.

## Setup

### 1. Choose an Emulator
- **BizHawk** (recommended) — Lua scripting, multi-system, good RAM watches
- **VBA-M** — simpler, works for GBA Pokemon
- **DeSmuME** — for DS Pokemon

### 2. Install emulator + ROM
```bash
# BizHawk (Windows only)
download from https://bizhawk.net/

# VBA-M (Linux)
apt install visualboyadvance-gtk
```

### 3. Get a Pokemon ROM
Place a `.gba` or `.nds` file in a known location.

## BizHawk Lua Scripting

### Basic Lua script to read player position
```lua
-- Connect to BizHawk's Lua API
game = require('gb')

-- Pokemon Red/Yellow memory map (addresses vary by game)
-- Player X position: $D362
-- Player Y position: $D361
-- Map ID: $D35E

while true do
    x = memory.readbyte(0xD362)
    y = memory.readbyte(0xD361)
    map = memory.readbyte(0xD35E)
    
    print(string.format("Position: (%d, %d) | Map: %d", x, y, map))
    
    -- Check for wild Pokemon battle
    battle = memory.readbyte(0xCC5D)
    if battle == 1 then
        enemy_hp = memory.readbyte(0xCC5A)
        player_hp = memory.readbyte(0xCC55)
        print(string.format("BATTLE! Enemy HP: %d | Player HP: %d", enemy_hp, player_hp))
    end
    
    emu.frameadvance()
end
```

### Movement
```lua
-- Press buttons
input = require('input')

-- Walk right
input.set(1, 'P1 Right')
emu.frameadvance()
```

## Common RAM Addresses

### Pokemon Red/Blue/Yellow
- `$D362` — Player X
- `$D361` — Player Y
- `$D35E` — Current Map ID
- `$CC5D` — Battle type (0=none, 1=wild, 2=trainer)
- `$CC5A` — Enemy Pokemon HP (byte)
- `$CC55` — Player Pokemon HP (byte)
- `$CC49` — Player Pokemon species
- `$D058` — Text being displayed

### Pokemon Gold/Silver (Crystal)
- `$D057` — Player X
- `$D058` — Player Y
- `$D05C` — Map ID
- `$CFD3` — Battle type
- `$CFE3` — Enemy HP (16-bit LE)

### Pokemon Ruby/Sapphire/Emerald
- `$D8` — Player X
- `$D9` — Player Y
- `$DA` — Map ID

## GameShark / Action Replay Codes
Gameshark codes modify RAM. Use them to:
- Walk through walls (RAM cheat)
- Catch any Pokemon
- Max stats

```
# Example Gameshark code format (raw)
01FF50D0  # Always catch Pokemon (Pokemon RBY)
```

## Automating Battles

### Catch wild Pokemon
```lua
-- Check for wild battle and throw Pokeball
function catchPokemon()
    if memory.readbyte(0xCC5D) ~= 1 then return end
    
    -- Select Pokeball from menu
    -- (simplified — actual implementation is complex)
    print("Wild Pokemon detected!")
end
```

## Limitations
- Emulators may not be 100% cycle-accurate
- RAM addresses change between game versions
- Some anti-cheat in emulators
- Legality: only use with ROMs you own
