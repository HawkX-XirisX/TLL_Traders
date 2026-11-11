The Last Light Trader System

**Trade equipment, supplies, valuables and vehicles in Arma Reforger**

> [!IMPORTANT]
> **Work in progress.** Catalogs, prices and dependencies can change. Verify vehicle ownership, bank settlement and restart behavior with your server's full addon set before relying on vehicle resale.

## Overview

**TLL_Traders** is a configurable trading economy by **XirisX** for The Last Light, Project Ashfall and custom scenarios. Traders are open to all factions. They use your existing **LL bank balance** for purchases and sales. Deposit or withdraw physical LL banknotes at an LL ATM.

[Arma Reforger Workshop](https://reforger.armaplatform.com/workshop/6AA745CE4AB3393D) · [Workshop changelog](https://reforger.armaplatform.com/workshop/6AA745CE4AB3393D/changelog) · [Project Ashfall Discord](https://discord.gg/GH6vQzQ7en)

- [Install](#install)
- [Buy and sell items](#buy-and-sell-items)
- [Trader roster and prices](#trader-roster-and-prices)
- [Buy and sell vehicles](#buy-and-sell-vehicles)
- [Configure a scenario](#configure-a-scenario)
- [Bank recovery and verification](#bank-recovery-and-verification)

## Install

- **Players:** Enable **TLL_Trader System** and the dependencies required by your scenario. Use an LL ATM to deposit banknotes before shopping.
- **Server owners:** Add the trader addon to the existing `game.mods` array. Match the server and client dependency versions. [Bohemia Interactive server config reference](https://community.bistudio.com/wiki/Arma_Reforger%3AServer_Config)
- **Scenario authors:** Open `addon.gproj` in Workbench or add **TLL_Traders** as a project dependency. Resolve dependencies and compile before placing traders.

```json
{
  "modId": "6AA745CE4AB3393D",
  "name": "TLL_Trader System"
}
```

The current source project ID is `TLLTraders`. Its project file declares base Arma Reforger, **LL_ATM**, the **LL Banknote** addons (10, 100, 1,000, 10,000 and 1,000,000), and these TLL addons.

| Dependency | Role | Workshop or project ID |
| --- | --- | --- |
| TLL_LootSystem | Consumables, harvesting tools and valuables | `6A4F61ED4143DA79` |
| TLL_BuildingSystem | Base console, nails and locker kits | `6AB65B2ACF03D981` |
| TLL_VirtualGarage | Vehicle claiming, ownership and garage notebook | `6A6E805B44DBDA09` |
| TLL LL ATM and Banknote Fix | Banking compatibility dependency declared by the current source project | `A7D1F352C61E49BC` |

Separate RHS and Drugs trader addons can extend the base system when included in a scenario. Each has its own dependencies.

## Buy and sell items

1. Approach a trader while alive and interact within **3 metres**.
2. Select **Buy** or **Sell**, choose a category and select an item card to see its preview and price. The menu shows up to 12 matching items per page.
3. Confirm the selected trade. Purchases require sufficient bank funds and compatible inventory space. Sales credit the bank account after the inventory operation succeeds.

The **Sell** tab shows eligible configured items you carry, including equipped items. Selling a weapon or container also removes its fitted attachments, loaded magazine or contents at the configured item price. Unload or empty it first if you want to keep those items.

Use mouse and keyboard or move through the tabs, filters, cards and footer with the D-pad or stick. Controller **MenuSelect** activates the focused control, and **MenuBack** closes the dialog. Item previews use native prefab previews, with dedicated display variants for selected attachments and harvesting tools.

## Trader roster and prices

Prefab files are under `Prefabs/`. Catalogs are under `Configs/Traders/`. Counts refer to entries in the current source project.

| Trader | Entries | Prefab | Catalog |
| --- | ---: | --- | --- |
| Weapons | 59 | `TLL_Trader_Weapons.et` | `WeaponsTrader.conf` |
| RPG | 4 | `TLL_Trader_RPG.et` | `RPGTrader.conf` |
| Explosives | 8 | `TLL_Trader_Explosives.et` | `ExplosivesTrader.conf` |
| Attachments | 46 | `TLL_Trader_Attachments.et` | `AttachmentsTrader.conf` |
| Magazines | 67 | `TLL_Trader_Magazines.et` | `MagazinesTrader.conf` |
| Clothing & Gear | 181 | `TLL_Trader_Clothes.et` | `ClothesAndGearTrader.conf` |
| Tools & Base Building | 12 | `TLL_Trader_Tools.et` | `ToolsTrader.conf` |
| Food & Drinks | 190 | `TLL_Trader_FoodDrinks.et` | `FoodDrinksTrader.conf` |
| Valuables | 20 | `TLL_Trader_Valuables.et` | `ValuablesTrader.conf` |
| Harvest | 2 | `TLL_Trader_Harvest.et` | `HarvestTrader.conf` |
| Wheeled Vehicles | 148 | `TLL_Trader_WheeledVehicles.et` | `WheeledVehiclesTrader.conf` |
| Helicopters | 18 | `TLL_Trader_Helicopters.et` | `HelicoptersTrader.conf` |

An additional `SuppliesTrader.conf` is available as a sample catalog for a custom placement.

- **Weapons and attachments.** Portable weapons are priced by class and the fitted attachments on their catalog prefab. Class bases are 3,000 LL for pistols, 10,000 LL for assault rifles and SMGs, 12,500 LL for sniper rifles, and 15,000 LL for machine guns and launchers. Attachment purchases run from 1,000 to 3,000 LL. The configured weapon and attachment resale prices are half of buy price. M67 and RGD-5 grenades are 2,500 LL to buy and 1,250 LL to sell.
- **Food and drinks.** The catalog has 155 foods and 35 drinks. Pricing starts at 2,000 LL or 200 LL per positive restoration point, whichever is higher. A 10% premium applies when two or more stats each restore at least 10 points. Buy prices round up to the nearest 100 LL. Sell prices are one-third of buy price rounded down to the nearest 100 LL.
- **Tools and base kits.** The Tools trader offers navigation and utility gear, a Base Console, a Garage Console Notebook, and General, Weapon and Military Locker Kits. Each console or kit costs 5,000 LL. A full box of 20 nails costs 10,000 LL. These base-building entries are buy-only.
- **Harvest.** The Pickaxe and Fire Axe each cost 2,500 LL to buy and sell for 1,250 LL.
- **Valuables.** Trade in configured gold and silver collectibles, bars, four harvested crystals, and rare golden rifles. These entries are sell-only by default. For example, a Silver Ingot sells for 7,000 LL and a Gold Bar for 15,000 LL.

## Buy and sell vehicles

Purchases spawn the selected vehicle at the delivery point and automatically claim it through **TLL_VirtualGarage**. Keep the area clear and leave enough room for the body, doors or rotors. Use an open, level site when placing the trader.

| Trader | Default delivery point | Default horizontal sale radius | Marker |
| --- | --- | ---: | --- |
| Wheeled Vehicles | 11 m ahead of the trader | 15 m | P |
| Helicopters | 16 m ahead of the trader | 25 m | H |

The marker identifies the center of the sale zone. The painted ring is smaller than the sale radius. The vehicle origin must be inside the sale radius and within **8 m vertically** of its center.

To sell a vehicle, bring it into the appropriate zone, stop, have everyone exit and open the **Sell** tab. The vehicle must be undestroyed, moving at no more than **1 m/s**, and claimed to your persistent owner identity. Garage PIN access or authorized-driver status alone does not grant sale rights. Finish active garage transfers first. When several eligible vehicles match one entry, the nearest one to the delivery point is sold. Remove any equipment or cargo you want to keep.

Buyable wheeled vehicles cost **50,000–150,000 LL** and helicopters cost **1,500,000–5,000,000 LL**. Buyable vehicles resell for half their listed purchase price. Of the 148 wheeled entries, 41 are sell-only, including 10 LAV, BTR and BRDM variants and 31 specified support or loaded trucks. Vehicle prices and buy/sell availability are set per prefab.

## Configure a scenario

1. Place a supplied trader prefab in World Editor. For a custom trader, copy the example's `TLL_TraderComponent`, replication component and action manager. Keep the `trader` action context and bind `TLL_OpenTraderAction` to it.
2. Assign the catalog through `m_Catalog`. Duplicate an existing catalog through Resource Browser to obtain a unique resource GUID. Use full GUID-qualified prefab references and declare dependencies for modded stock.
3. For vehicle vendors, configure `m_OutputOffset`, `m_SaleRadius` and `m_ShowParkingMarker`. Verify the delivery position and sale zone with your actual map terrain. Supplied legacy offsets migrate to current delivery minimums.
4. Update catalog resources on server and clients, then reload resources or restart the scenario. Catalogs are Workbench resources.

```text
TLL_TraderItem {
 Name "M16A2"
 Prefab "{3E413771E1834D2F}Prefabs/Weapons/Rifles/M16/Rifle_M16A2.et"
 BuyPrice 12000
 SellPrice 6000
 Delivery 0
}
```

Positive integer prices enable the corresponding trade direction. Use `-1` to disable buying or selling. Zero is rejected. When both directions are enabled, the sell price cannot exceed the buy price. Compare equivalent items across vendors when setting prices.

`Delivery 0` trades an inventory item. `Delivery 1` uses the vehicle purchase and resale flow. Optional `PreviewPrefab` changes the card preview while trades continue to use `Prefab`.

Set `WeaponFilters 1` for **All / AR / Sniper / MG / Pistol / SMG**. Category `WeaponFilter` values 1–5 follow that order after All, and 0 infers the group from the category name. With `WeaponFilters 0`, the menu displays **All** plus up to five configured category filters.

## Bank recovery and verification

The server resolves prices from its catalog and validates trade requests. The LL bank reserves the account while the operation settles. Vehicle sales use the garage claim and removal flow. For persistence-tracked vehicles, bank credit waits for a successful world checkpoint. Those sales require saving to be enabled, allowed and idle. The server processes one trader vehicle sale at a time.

If delivery, removal, checkpointing or payment is uncertain, a pending LL bank record may block further trades. For administrator recovery, pause trading on the affected account and compare the `[TLL Trader]` logs, inventory or world state, and the record under `$profile:LL_Banking/`. Confirm what changed and what settled before clearing or reconciling the pending operation.

The published Workshop listing reports successful Workbench compilation and in-game item buying and selling on **Arma Reforger 1.9.0.37**. Local project notes record catalog, pricing and resource checks. Dedicated-server vehicle purchase and resale, remote ownership checks, reconnect/restart, checkpoint failure recovery and physical controller navigation still need verification with your scenario. [Workshop testing notes](https://reforger.armaplatform.com/workshop/6AA745CE4AB3393D)

## Credits and license

**XirisX** develops TLL_Traders for The Last Light and Project Ashfall. The Workshop release is listed under the **Arma Public License (APL)**. [Workshop license listing](https://reforger.armaplatform.com/workshop/6AA745CE4AB3393D)
