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
