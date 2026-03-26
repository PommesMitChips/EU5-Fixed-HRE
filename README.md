# EU5 Fixed HRE

Fixes broken Holy Roman Empire mechanics that Paradox shipped but never finished implementing.

## The problem

When you pass *Revoke the Privilegia* (the top reform on the Emperor power track), every HRE member gets an event asking them to swear a loyalty oath. In the base game, agreeing to swear the oath **does absolutely nothing**. No prestige, no subject conversion, no mechanical change of any kind. Refusing works fine and gets you expelled from the Empire, but accepting is completely pointless.

This is not an Early Access placeholder. The game released in November 2024 and is currently on v1.1.10. The mechanic is just broken.

This mod fills in what the oath was clearly intended to do.

## What changes

### Three new imperial subject types

When a member swears the oath, they get converted into an imperial subject type based on what they were before:

| Before oath | After oath |
|---|---|
| Fiefdom | **Imperial Fiefdom** |
| Vassal | **Imperial Vassal** |
| Independent HRE member | **Direct Imperial Vassal** |

All three types cost zero diplomatic capacity and contribute zero strength to liberty desire, so the Emperor actually benefits from consolidating the Empire rather than being punished for it. They are only visible to the Emperor while Revoke the Privilegia is active.

Junior partners in a personal union with the Emperor are left untouched, since personal unions are a separate international organization and reassigning the subject relation would cancel the union.

### Coronation and succession

Direct Imperial Vassals are sworn to the office, not the person. When a new Emperor is crowned, all Direct Imperial Vassal relationships are cleared and reassigned to the new Emperor. Personal unions are preserved through this transfer.

Direct Imperial Vassals are valid candidates in imperial elections. When elected, their vassal status is cleared as part of the coronation.

### If you repeal Revoke the Privilegia

Unlikely, but possible. A new event fires for the Emperor and reverses everything: Imperial Fiefdoms and Vassals revert to their base types, and Direct Imperial Vassals are released back into the Empire as independent members.

### If the HRE is dismantled

The same cleanup runs automatically before the Empire ceases to exist.

## Language support

All 10 languages supported by the base game are included:

Brazilian Portuguese, English, French, German, Japanese, Korean, Polish, Russian, Simplified Chinese, Spanish, Turkish

## Files

| File | What it does |
|---|---|
| `in_game/events/hre.txt` | Full override of the base game event file, modifying `hre.101`, `hre.800`, and `hre.15`, and adding the new repeal event `hre.108` |
| `in_game/common/laws/00_hre_fix.txt` | Adds an `on_deactivate` hook to `revoke_privilegia_policy` |
| `in_game/common/subject_types/00_hre_fixed.txt` | Defines the three new subject types |
| `in_game/common/international_organizations/00_hre_fixed.txt` | Adds Direct Imperial Vassals as valid emperor candidates |
| `in_game/common/resolutions/00_hre_election_fix.txt` | Removes the subject exclusion modifier for Direct Imperial Vassals in elections |
| `main_menu/localization/*/events/fixed_hre_events_l_*.yml` | Event localisation for all supported languages |
| `main_menu/localization/*/fixed_hre_subjects_l_*.yml` | Subject type names and descriptions for all supported languages |

## Compatibility

Requires EU5 v1.1.10 or later. All files except `in_game/events/hre.txt` use partial definitions that load before the base game and merge cleanly. The events file is a full override and will conflict with other mods that modify the base game HRE events.

## Already passed the law?

If you passed Revoke the Privilegia before installing the mod, use the console to catch up:

```
event hre.100
```

This re-fires the loyalty oath event for all current HRE members.

## Why not on the Steam Workshop?

I don't want to tie this to my username. Anyone who wants to upload or maintain it there is welcome to.

## Installation

1. Download or clone this repository
2. Place the `Fixed HRE` folder in your EU5 mod directory: `Documents/Paradox Interactive/Europa Universalis V/mod/`
3. Enable the mod in the EU5 launcher
