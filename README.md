# Chemical Propulsion
An overhaul to the stock propellant system, replacing generic LiquidFuel, Oxidizer, MonoPropellant and SolidFuel with a handful of real chemicals.
This mod is distinct from RealFuels in that it deals with only a short list of primary liquid propellants — Kerosene, HTP, LqdOxygen, LqdHydrogen, LqdMethane, LqdAmmonia, Hydrazine and NTO — for a more straightforward and curated propellant system more in line with e.g. Nertea's Cryogenic Engines. In fact, Nertea's mods are a particular target of this overhaul, which can be thought of as a Nertea-like soft alternative to RealFuels.

## Features
### Engine changes
Monopropellant engines and tanks have a choice of two propellants: HTP which is cheap and available at the beginning of career mode, and Hydrazine which is unlocked later and more expensive but yields a significantly higher specific impulse. Solid rockets have a similar progression from PBAN to the slightly more performant HTPB.

Bipropellant engines are categorised into particular fuel-oxidizer combinations with fixed mixture ratios:
- Keroxide:
  - 1 Kerosene / 3 HTP
- Ammonilox:
  - 7 LqdAmmonia / 9 LqdOxygen
- Hypergolic:
  - 7 Hydrazine / 9 NTO
- Kerolox:
  - 3 Kerosene / 5 LqdOxygen
- Methalox:
  - 7 LqdMethane / 9 LqdOxygen (a more fuel-rich, more realistic figure than CryoEngines/CryoTanks native 3 LqdMethane / 1 Oxidizer)
- Hydrolox:
  - 3 LqdHydrogen / 1 LqdOxygen (roughly equivalent in mass to CryoEngines/CryoTanks native 15 LqdHydrogen / 1 Oxidizer)

Near Future Launch Vehicles' KR-701 'Cougar' and KR-74 'Lynx' are bimodal hydrolox engines with an additional kerosene-augmented mode, based on their real-world analogues the RD-701 and RD-704:
  - 1 Kerosene / 4 LqdHydrogen / 3 LqdOxygen (equivalent to 1 part kerolox + 2 parts hydrolox)

LiquidFuel jet engines use Kerosene, with the rocket mode of multimodal engines running on Kerosene and LqdOxygen.

Engines can easily be patched to replace their propellants with one of the combinations above like the following:
```
@PART[partName]:BEFORE[zz_ChemicalPropulsion]
{
	@MODULE[ModuleEngines*]
	{
		// Single propellants
		chemTechPropellant = propellantLqdHydrogen // propellantHTP, propellantPBAN

		// Fuels
		chemTechPropellant = fuelLqdAmmonia // fuelKerosene, fuelHydrazine, fuelLqdMethane, fuelLqdHydrogen

		// Oxidizers
		chemTechPropellant = oxidizerHTP // oxidizerLqdOxygen, oxidizerNTO
	}
}
```
### CryoTanks changes
This mod replaces all CryoTanks fuel switch types to Chemical Technologies tank types. One particular feature of this is the removal of CryoTanks' native 1.5x hydrogen packing density buff, which not-insignificantly affects the use of LqdHydrogen in the game. This is not just an arbitrary change purely motivated by realism. The ~14% higher density of LqdOxygen over Oxidizer and adjusted methalox mixture ratio (higher oxidizer mass fraction) make cryogenic bipropellants much more attractive, removing the need for any sneaky volume buffs in chemical rockets. Hydrolox suffers a little bit, but I've found this actually balances better against their high Isp. Nuclear engines naturally suffer the most, but again, these engines are very high Isp and it should really be expected that you'd need to haul massive tanks everywhere. I've always wanted my CryoTanks to be bigger, personally.

## Dependencies
- [ModuleManager (4.2.3)](https://github.com/sarbian/ModuleManager)
- [B9PartSwitch (2.20.0)](https://github.com/blowfishpro/B9PartSwitch)
- [Community Resource Pack (112.0.1)](https://github.com/UmbraSpaceIndustries/CommunityResourcePack)
- [Chemical Core (1.2.0)](https://github.com/CharleRoger/ChemicalCore)
- [Ignition (1.1.2)](https://github.com/CharleRoger/Ignition)
## Compatibility
Some mods are explicitly patched to work with Chemical Propulsion, while others are patched implicitly or are simply unaffected and have been found compatible.
### Explicit support
- [Alcoholic Aeronautics (1.0.0)](https://github.com/CharleRoger/AlcoholicAeronautics)
- [Cryogenic Engines (2.0.8)](https://github.com/post-kerbin-mining-corporation/CryoEngines)
- [Cryogenic Tanks (1.6.6)](https://github.com/post-kerbin-mining-corporation/CryoTanks)
- [Kerbal Atomics (1.3.4)](https://github.com/post-kerbin-mining-corporation/KerbalAtomics)
- [Kerbal Reusability Expansion (2.9.3)](https://github.com/TundraMods/Kerbal-Reusability-Expansion)
- [Knes (1.9.9)](https://github.com/AstroWell/Knes)
- [Labradoodle (1.0.1)](https://github.com/CharleRoger/Labradoodle)
- [MissingHistory (1.9.3)](https://spacedock.info/mod/1743/MissingHistory)
- [Mk-33 (1.3.2)](https://github.com/Angel-125/Mk-33)
- [Near Future Aeronautics (2.1.2)](https://github.com/post-kerbin-mining-corporation/NearFutureAeronautics)
- [Near Future eXploration (1.1.3)](https://github.com/post-kerbin-mining-corporation/NearFutureExploration)
- [Near Future Launch Vehicles (2.2.2)](https://github.com/post-kerbin-mining-corporation/NearFutureLaunchVehicles)
- [Near Future Spacecraft (1.4.4)](https://github.com/post-kerbin-mining-corporation/NearFutureSpacecraft)
- [OCRAP (1.0.1)](https://github.com/CharleRoger/OCRAP)
- [Restock and Restock+ (1.5.1)](https://github.com/PorktoberRevolution/ReStocked)
- [Shuttle Orbiter Construction Kit (1.1.8)](https://github.com/benjee10/Shuttle-Orbiter-Construction-Kit)
- [Supplementary Electric Engines (1.3.2)](https://forum.kerbalspaceprogram.com/topic/218397-1125-supplementary-electric-engines/)
- [SystemHeat (0.8.1)](https://github.com/post-kerbin-mining-corporation/SystemHeat)
- [Tantares (28.0.0)](https://github.com/Tantares/Tantares)
- [TantaresLV (16.2.0)](https://github.com/Tantares/TantaresLV)
- [TantaresSP (6.0.0)](https://github.com/Tantares/TantaresSP)
- [Tundra Exploration (7.1.1)](https://github.com/TundraMods/TundraExploration)
### Implicit support
- [CryoEngines Extensions (1.0.4)](https://forum.kerbalspaceprogram.com/topic/219145-112x-cryoengines-extensions-new-methane-and-hydrogen-engines-fabriqu%C3%A9-au-canada/)
- [Far Future Technologies (1.4.2)](https://github.com/post-kerbin-mining-corporation/FarFutureTechnologies)
- [Silly Photon Drives (1.1.1)](https://forum.kerbalspaceprogram.com/topic/220997-1125-silly-photon-drives/)
- Many more, though might do unexpected things. Let me know what else to support!

## License
Distributed under the GNU General Public License.
