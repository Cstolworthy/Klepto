# Klepto

A spiritual successor to [kleptomania](https://www.nexusmods.com/abioticfactor/mods/214) by Terastardig (Nexus, UE4SS), rebuilt for the official mod.io mod support. Klepto covers every object kleptomania did, plus a few more.

An Abiotic Factor mod that adds the **Kleptomaniac** trait. A character with the trait can pack up fixed furniture and appliances that the game normally bolts down: stoves, kitchen cupboards and counters, lockers, sinks, toilets, vending, coffee and slushie machines, water tanks, bunk mattresses and shelves. Items packed this way never break.

> If it isn't nailed down, it's yours. If it is nailed down... it's still yours.

## mod.io

| | |
|---|---|
| Mod ID | **6508756** |
| Game ID | 13105 (Abiotic Factor) |
| Visibility | Private |
| Current version | 1.0 (first uploaded 2026-11-07) |

The same ID is stored in `Klepto7M211/Klepto7M211.abfmod`, which the editor reads when updating the listing, and in `modio.json`.

## Using it

1. Install Klepto from the game's **Mod Browser** on the title screen.
2. Host a world with Klepto enabled.
3. Create a character and pick **Kleptomaniac** (2 points).
4. Hold a screwdriver-type tool (screwdriver, hand drill, power drill, construction gauntlet) and use the normal pack-up action on a fixed item.

Friends who join a world with Klepto enabled are prompted to download it. Only one player needs the trait: the unlock runs on the host, so once anyone has it, everyone in that world can pack the unlocked items.

## How it works

- `Trait_Kleptomaniac` (DT_Traits) grants `Buff_Trait_Kleptomaniac` (DT_BuffsDebuffs).
- The buff's logic object, `Blueprints/BuffObject_Kleptomaniac`, runs on the server when the buff is applied and on every buff tick (once per second).
- Each run finds all `AbioticDeployed_Furniture_ParentBP` actors. For each one whose class is in its lookup list, it sets `CanBePackaged = true`, `DefaultBreakChanceOnPackage = 0` and `DeconstructedItemData` to the matching item row.
- Fixed items that have no inventory item in the base game get a new deployable item row under `DataTables/ItemTable_Deployables/klepto_*`. These rows reuse the game's meshes and the closest existing icons.
- In the game, mod row names carry the prefix `OBXNA_` (for example `OBXNA_klepto_stove_industrial`). The lookup list in the Blueprint uses these full names.

### Unlocked items

| Item | Base-game class | Item row |
|---|---|---|
| Industrial stove | Stove_Industrial_8Spots | klepto_stove_industrial |
| Kitchen stove | Stove_Kitchen_4Spots | klepto_stove_kitchen |
| Coffee machine (×2) | CoffeeMachine_BP, CoffeeMachine_VOTV | klepto_coffeemachine, klepto_coffeemachine_votv |
| Kitchen cupboard | Container_KitchenCabinet | klepto_kitchencabinet |
| Kitchen counter | Container_KitchenCounter | klepto_kitchencounter |
| Kitchen cabinets L/R | Container_VOTV_Kitchen_Bedroom_Cabinet_Left/Right | klepto_votvcabinet_left/right |
| Lockers (×3) | Container_Locker, _Security, _VOTV | klepto_locker, klepto_locker_security, klepto_locker_votv |
| Cubicle shelf | Deployed_CubicleShelf | klepto_cubicleshelf |
| Bunk mattresses (×2) | Deployed_Furniture_RES_Bed_02/03 | klepto_resbed_02/03 |
| Toilets (×2) | Toilet_Office_BP, Deployed_VOTV_Toilet | klepto_toilet_office, klepto_toilet_votv |
| Porta-potty | Toilet_Portapotty | klepto_portapotty |
| Giant water tank | Deployed_WaterTank | klepto_watertank |
| Slushie machine | Slushie_Machine_BP | klepto_slushie |
| Vending machines (×5) | VendingMachine_BP, _KizzCola_Bp, _Snacks_BP, _Snacks_VOTV, _VOTV_Drinks | klepto_vending_* |
| Sinks (×6) | Faucet_Alien, Faucet_Sink_Executive/Industrial/Office_Bathroom/Office_Kitchen, Faucet_VOTV_Sink_Bathroom | klepto_sink_* |
| Unbreakable locker bench | Furniture_Bench_Unbreakable | Bench_Locker (base game) |
| Breakroom table | Furniture_VOTV_CafeteriaTable | Deployable_Table_Cafeteria (base game) |
| Mattress | Deployed_VOTV_Mattress | votv_Mattress (base game) |
| Signal workbench | Deployed_CraftingBench_SIGNAL | klepto_craftbench_signal |
| Salem salvage anvil | Salem_SalvageAnvil | klepto_salvage_anvil |
| GATE charging station | GATE_ChargingStation | klepto_gate_chargingstation |

### Deliberately left fixed

Ladders, tram seats and tram storage, wall turrets, jump pads, punch-card terminals, trader boxes and dispensers, force fields, locked/hackable crates, robot charging modules, and the water-volume actors. Moving these can strand a player or break areas and quests.

## Known limits

- The unlock is world-wide, not per player.
- Items unlocked during a session stay unlocked until their area reloads, even if the trait goes away.
- Moved sinks may still give unlimited water.
- Disabling Klepto on a save removes its items, including any fixed items you've moved.
- Multiplayer has only been tested solo.

## Layout

```
Klepto/                      repo root
  README.md                  this file (must stay OUTSIDE Klepto7M211)
  modio.json                 mod.io IDs and upload history
  listing/                   mod.io listing image and source icons
  Klepto7M211/               the mod project; Upload zips this whole folder
```

Keep `.git`, `.md` files and anything else that shouldn't ship out of `Klepto7M211`. mod.io rejects uploads that contain `.md` files.

## Updating the mod

1. Open `Klepto7M211/Klepto7M211.abfmod` in the Abiotic Factor Mod Editor.
2. Make the changes and test with Play In Editor.
3. Open the Mod Management Tool, choose **Use Existing Mod** with ID `6508756`, bump the version, then Validate and Upload.
4. Add the new version to `modio.json`.
