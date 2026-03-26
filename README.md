# EU5 Fixed HRE

A mod for **Europa Universalis V** (v1.1.10+) that fixes broken Holy Roman Empire mechanics Paradox shipped but never implemented.

## What's broken in the base game

### Revoke the Privilegia — shipped empty

Passing *Revoke the Privilegia* (the top reform of the Emperor power track) fires `hre.101` for every HRE member, prompting them to swear an oath of loyalty. In the base game, Option A — swearing the oath — **does nothing**. It is a completely empty effect: no prestige, no subject conversion, no mechanical consequence. Option B (refusing) expels the member from the Empire as intended, but accepting is pointless.

This mod fills in what Option A was clearly designed to do.

## What this mod does

### Three new imperial subject types

When an HRE member swears the loyalty oath after *Revoke the Privilegia* passes, they are converted to an appropriate imperial subject type based on their current status:

| Before oath | After oath |
|---|---|
| Fiefdom (incl. PU junior) | **Imperial Fiefdom** |
| Vassal | **Imperial Vassal** |
| Independent HRE member | **Direct Imperial Vassal** (sworn to the Emperor personally) |

All three types:
- Cost **0 diplomatic capacity** for the overlord
- Contribute **0 strength** toward liberty desire calculations
- Spread institutions between overlord and subject at a mild rate
- Are only visible to the HRE Emperor while *Revoke the Privilegia* is active

**Direct Imperial Vassals** are transferred to a new Emperor automatically on coronation (`hre.800`), keeping them tied to the office rather than the person.

### Repeal of Revoke the Privilegia

If the Emperor repeals *Revoke the Privilegia*, a new event (`hre.108 — The Privilegia Restored`) fires and reverses the conversions:

- Imperial Fiefdoms revert to Fiefdom
- Imperial Vassals revert to Vassal
- Direct Imperial Vassals are released as independent HRE members

### HRE Dissolution

If the Holy Roman Empire is dismantled (`hre.15`), the same cleanup runs automatically — all imperial subject types are reverted or released before the Empire ceases to exist.

## Files modified / added

| File | Type | Purpose |
|---|---|---|
| `in_game/events/hre.txt` | Full override | Fills in `hre.101.a`, adds emperor coronation transfer (`hre.800`), adds repeal event (`hre.108`), adds dissolution cleanup (`hre.15`) |
| `in_game/common/laws/20_hre.txt` | Full override | Adds `on_deactivate` to `revoke_privilegia_policy` to fire `hre.108` on repeal |
| `in_game/common/subject_types/hre_fixed.txt` | New file | Defines `imperial_vassal`, `direct_imperial_vassal`, `imperial_fiefdom` subject types |
| `main_menu/localization/english/events/fixed_hre_events_l_english.yml` | New file | Localisation for new event options |
| `main_menu/localization/english/fixed_hre_subjects_l_english.yml` | New file | Localisation for new subject type names and descriptions |

## Compatibility

- Requires **EU5 v1.1.10** or later
- Fully overrides `hre.txt` and `20_hre.txt` — **incompatible with any mod that also modifies these files**
- Does not touch any other base game files

## Installation

1. Download or clone this repository
2. Place the `Fixed HRE` folder in your EU5 mod directory:
   `Documents/Paradox Interactive/Europa Universalis V/mod/`
3. Enable the mod in the EU5 launcher
