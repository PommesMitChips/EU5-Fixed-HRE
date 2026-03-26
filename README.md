# EU5 Fixed HRE

Fixes broken Holy Roman Empire mechanics that Paradox shipped but never finished implementing.

## The problem

When you pass *Revoke the Privilegia* (the top reform on the Emperor power track), every HRE member gets an event asking them to swear a loyalty oath. In the base game, agreeing to swear the oath **does absolutely nothing**. No prestige, no subject conversion, no mechanical change of any kind. Refusing works fine and gets you expelled from the Empire, but accepting is completely pointless.

This is not an Early Access placeholder. The game released in November 2025 and is currently on v1.1.10. The mechanic is just broken.

This mod fills in what the oath was clearly intended to do.

## What changes

### Three new imperial subject types

When a member swears the oath, they get converted into an imperial subject type based on what they were before:

| Before oath | After oath |
|---|---|
| Fiefdom (including PU juniors) | **Imperial Fiefdom** |
| Vassal | **Imperial Vassal** |
| Independent HRE member | **Direct Imperial Vassal** |

All three types cost zero diplomatic capacity and contribute zero strength to liberty desire, so the Emperor actually benefits from consolidating the Empire rather than being punished for it. They are only visible to the Emperor while Revoke the Privilegia is active.

Direct Imperial Vassals are sworn to the office, not the person. When a new Emperor is crowned, they transfer over automatically.

### If you repeal Revoke the Privilegia

Unlikely, but possible. A new event fires for the Emperor and reverses everything: Imperial Fiefdoms and Vassals revert to their base types, and Direct Imperial Vassals are released back into the Empire as independent members.

### If the HRE is dismantled

The same cleanup runs automatically before the Empire ceases to exist.

## Files

| File | What it does |
|---|---|
| `in_game/events/hre_fixed.txt` | Surgically replaces `hre.101`, `hre.800`, and `hre.15` using `REPLACE:`, and adds the new repeal event `hre.108` |
| `in_game/common/laws/20_hre.txt` | Full override of the HRE law file to add an `on_deactivate` hook to `revoke_privilegia_policy` |
| `in_game/common/subject_types/hre_fixed.txt` | Defines the three new subject types |
| `main_menu/localization/english/events/fixed_hre_events_l_english.yml` | Localisation for the new event options |
| `main_menu/localization/english/fixed_hre_subjects_l_english.yml` | Localisation for the new subject type names and descriptions |

## Compatibility

Requires EU5 v1.1.10 or later. The law file (`20_hre.txt`) is a full override, so this mod will conflict with any other mod that also modifies it. Everything else uses surgical replacements and should be more compatible.

## Why not on the Steam Workshop?

I don't want to tie this to my username. Anyone who wants to upload or maintain it there is welcome to.

## Installation

1. Download or clone this repository
2. Place the `Fixed HRE` folder in your EU5 mod directory: `Documents/Paradox Interactive/Europa Universalis V/mod/`
3. Enable the mod in the EU5 launcher
