# Tomb Raider: Definitive Edition — Atmosphère / EdiZon Cheats

| | |
|---|---|
| **Game** | Tomb Raider: Definitive Edition |
| **Title ID** | `0100092021C80000` |
| **Build ID** | `4A8345806827F954` |
| **Cheat file** | `4A8345806827F954.txt` |
| **Format** | Atmosphère cheat (dmnt) — works with EdiZon / Breeze / Eden |

> ⚠️ These cheats only work on build `4A8345806827F954`. If the game is updated, code addresses change and the cheats will not work.

> ⚠️ Status: built from static analysis of `exefs/main`, **not fully tested in-game**.

---

## Cheat List

| # | Name | Effect |
|---|---|---|
| 1 | **Infinite Ammo & Items (Max on Pickup)** | Ammo/items are not consumed when used. Picking up ammo fills that ammo type to max capacity. |
| 2 | **No Reload** | Magazine/clip does not decrease when firing, including alt-fire ammo (e.g. grenade launcher). |
| 3 | **Infinite HP (Scripted Deaths Still Apply)** | Normal damage (bullets, arrows, melee, fire) does not reduce Lara's HP. Scripted damage (fatal falls, wolf QTE) and damage ≥ max HP still apply so the game does not soft-lock. Player only — enemies can still die. |
| 4 | **Max Salvage (99999)** | Salvage is set to 99999 whenever the game reads it (opening the camp / upgrade menu). |
| 5 | **Max XP (999999)** | XP is set to 999999 when the game reads or processes XP. Earn XP once to trigger level-ups and gain skill points. **Experimental.** |

---

## Installation

### Eden (emulator)

1. Copy `4A8345806827F954.txt` to:
   ```
   eden\user\load\0100092021C80000\<AnyName>\cheats\4A8345806827F954.txt
   ```
   Example: `eden\user\load\0100092021C80000\Cheats\cheats\4A8345806827F954.txt`
2. Right-click the game → **Properties** → **Add-Ons** tab.
3. Tick the cheats you want → OK → launch the game.

### Switch (Atmosphère + EdiZon)

1. Copy `4A8345806827F954.txt` to your SD card:
   ```
   /atmosphere/contents/0100092021C80000/cheats/4A8345806827F954.txt
   ```
2. Launch the game, open the EdiZon overlay (Tesla), and enable the cheats you want.

### Disabling

Turn the cheat off and **restart the game**. These cheats patch game code in memory, so disabling them while the game is running does not restore the original code.

---

## Notes

- **Infinite Ammo:** if your ammo is already 0 when enabling the cheat, pick up ammo once — it fills to max immediately.
- **No Reload:** if the clip is empty when enabling the cheat, reload once first.
- **Infinite Ammo & Items** also applies to crafting items that use the same consume function.
- **Max XP** may make the XP percentage display look odd if it exceeds the level table. Disable it if the game crashes.
- Not available yet: **No Recoil** (likely controlled by weapon data in the `.tiger` files, not code) and **99 Skill Points** (no direct skill point field found; use Max XP instead).

---

## Technical Details

Offsets are relative to the `main` module base. Code caves use the unused tail of the `.text` segment page at `0xD75500`–`0xD76000` (mapped, zero-filled).

| Cheat | Location | Original instruction | Patch |
|---|---|---|---|
| Infinite Ammo | `0xA39C9C` (ConsumeItem) | `sub w8, w8, w22` | `nop` |
| Max on pickup | `0xA315E8` (ModifyAmmo clamp) | `csel w24, w8, w26, lo` | `mov w24, w26` |
| No Reload | `0xA35758` (fire, clip `weapon+0xD0`) | `str w8, [x26, #0xd0]` | `nop` |
| No Reload (alt) | `0xA357C8` (alt ammo `weapon+0xD8`) | `str w8, [x26, #0xd8]` | `nop` |
| Infinite HP | `0x48D370` (ModifyHealth apply) | `ldp w25, w24, [x19, #0x1c]` | branch to cave: negative delta → 0 when owner is the player (`[inst+0x5E]` bit 10), unless raw flag (`w20`) is set or damage ≥ max HP |
| Max Salvage | `0xD4FDA0`, `0xD50364`, `0xAECA04`, `0xBF57EC`, `0x667C94` | `ldr wN, [xM, #0x2514]` | branch to cave: write 99999 to `player+0x2514` |
| Max XP | `0xABFA88`, `0xD4FC24` | `ldr wN, [xM, #0x2508]` | branch to cave: write 999999 to `player+0x2508` |

Data layout found:

| Field | Description |
|---|---|
| `player+0x2478` | inventory pointer |
| `player+0x2508` | total XP |
| `player+0x2510` | level |
| `player+0x2514` | salvage |
| `inventory+0x50` | ammo count hash map (node: `+0x8` key, `+0xC` count u16) |
| `inventory+0x78` | ammo capacity hash map (default 100) |
| `weapon+0xD0` | rounds in clip |
| `healthcomp+0x1C` / `+0x20` | current HP / max HP |
| `main+0x27E2640` | player list pointer (element 0 = local player) |
