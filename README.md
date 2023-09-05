# Station Logistics
(WIP) Create station logistics networks to help manage your stations.

(insert pic here)

> Logistics networks: that's how simple it is!

(links etc)

## Quick Start Guide
This mod is yet another approach to the age-old station-to-station supply-chain problem; see below sections for comparisons with other similar mods.

This mod is actually surprisingly simple:
- Pair player-owned stations together to form (bi-directional) logistics links
- Stations prefer to trade with other paired stations

You can now create sprawling logistics networks; e.g., it may look like this:

![Logistics network demo diagram](https://raw.githubusercontent.com/Vectorial1024/v1024_station_logistics/master/images/StationLogistics_IntroductionExample.drawio.png)

Transitioning to the endgame has never been easier:
- Extend your trade range using your trade stations
- Intuitively create long-distance supply lines (see examples below)
- Forget the pain of handcrafting Repeat Orders just to move wares
- No need to micro buy/sell prices again
- A worry-free fallback for you in case other custom trading mods fail

For detailed behavioral info (e.g. what this mod does not intend to do), please see Technical Explanation section.

## Requirements

- SirNukes Mod Support APIs
  - Required: enables you to link stations to form logistics networks
  - Their Steam Workshop page: https://steamcommunity.com/sharedfiles/filedetails/?id=2042901274

## Detailed Introduction

Station-to-station supply chains are not something new. As written in the README of Automated Player Station Logistics (https://github.com/tizubythefizo/X4-AutomatedPlayerStationLogistics):

> [...] Each station is an independent entity that doesn't know or care that it's part of a larger network of faction owned stations. [...]

Many techniques are used by players to achieve a reasonably-working "logistics network", from the simplest trading blacklist (restrict others), to the more complicated techniques involving buy-sell prices, Repeat Orders, custom trading scripts, or a combination of them all. These all have a big problem: they scale poorly when things grow, and (depending on the exact method used), they may not really guide the movement of wares.

It then becomes obvious. How do we guide the movement of wares? Well, we just... tell the game about it! Tell your station managers, for example, "I want you to supply your products to station X"; or, "I want you to source your ingredients from station Y and Z".

It really is that simple. As long as each manager in the network respect these guidelines, a working logistics network is formed.

This mod does not go out of the way to define custom delivery behaviors; instead, it simply makes trades between certain station pairs more attractive to the trader. With this simple trick, station traders can form the backbone of your logistics network, and you can focus on something else, such as defense.

## Technical Explanation

Logicstics links are created between 2 player-owned non-wrecked stations (the "pairing"):
- When station traders are matching trade offers, they will prioritize offer matches between these 2 stations

Stations can be daisy-chained with each other via logistics links to form a logistics network.

This has the following effects:
- Case 1: logistics links between stations with impossible offer matches will not have any special effect
  - Station A sells Energy Cells
  - Station B buys Hull Parts
  - Station A is linked with Station B
  - Since these trade offers are impossible to match, there will be no special effects between A and B even when both are linked together
- Case 2: logistics links between stations with possible offer matches will get prioritized shipments between them
  - Station A sells Energy Cells and buys Refined Metals
  - Station B buys Energy Cells and sells Refined Metals
  - Station A is linked with Station B
  - When Station A is looking for buyers of Energy Cells, it will prefer Station B over other stations; vice versa from Station B's POV
  - When Station A is looking for sellers of Refined Metals, it will prefer Station B over other stations; vice versa from Station B's POV
- Case 3: logistics links between trade stations with possible offer matches will act like a storage balancer between them 
  - Station A buys and sells Hull Parts (i.e., Station A is a trade station)
  - Station B also buys and sells Hull Parts (i.e., Station B is also a trade station)
  - Station A is linked with Station B
  - When Station A is looking for buyers of Hull Parts, it will try the following in order:
    - It will try to sell Hull Parts to linked non-trade stations first
    - If no good offers are found, it will then try to sell Hull Parts to other linked trade stations (e.g. Station B)
  - Vice versa for the other direction

But still, this mod has some caveats:
- Free traders does not look at logistics links when deciding trades
  - This is helpful when, for some reason, there is an extreme shortage/surplus, and your station traders cannot keep up
  - If you want to prevent NPC free traders trading at your stations, then setup trade restrictions

## Some Usage Examples

(WIP)

## Comparing with Other Mods

(WIP)
