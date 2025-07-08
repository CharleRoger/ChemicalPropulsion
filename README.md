# Chemical Propulsion
An overhaul to the stock propellant system, replacing generic LiquidFuel, Oxidizer, MonoPropellant and SolidFuel with a handful of real chemicals.

## Features
### Core design
This mod is distinct from RealFuels in that it deals with only ten primary liquid propellants, for a more straightforward and curated propellant system more in line with e.g. Nertea's Cryogenic Engines. In fact, Nertea's mods are a particular target of this overhaul, which can be thought of as a Nertea-like soft alternative to RealFuels.

The ten core propellants are:

- `Ethanol`
- `LqdOxygen`
- `Kerosene`
- `IWFNA` (Nitric acid)
- `LqdAmmonia`
- `HTP` (High-test peroxide)
- `Hydrazine`
- `LqdMethane`
- `LqdHydrogen`
- `NTO` (Dinitrogen tetroxide)

### Engine changes
Bipropellant engines are categorised into particular fuel-oxidizer combinations with fixed mixture ratios. Any fuel can be paired with any oxidizer, though not all combinations are necessarily configured or available depending on which supported mods you use. The most common bipropellants you'll likely encounter are:

- Keroxide:
  - 1 `Kerosene` / 3 `HTP`
- Hypergolic:
  - 7 `Hydrazine` / 9 `NTO`
- Kerolox:
  - 3 `Kerosene` / 5 `LqdOxygen`
- Methalox:
  - 7 `LqdMethane` / 9 `LqdOxygen` (a more fuel-rich, more realistic figure than CryoEngines/CryoTanks native 3 `LqdMethane` / 1 `Oxidizer`)
- Hydrolox:
  - 3 `LqdHydrogen` / 1 `LqdOxygen` (roughly equivalent in mass to CryoEngines/CryoTanks native 15 `LqdHydrogen` / 1 `Oxidizer`)

Near Future Launch Vehicles' KR-701 'Cougar' and KR-74 'Lynx' are bimodal hydrolox engines with an additional kerosene-augmented mode, based on their real-world analogues the RD-701 and RD-704:

- 1 `Kerosene` / 4 `LqdHydrogen` / 3 `LqdOxygen` (equivalent to 1 part kerolox + 2 parts hydrolox)

Monopropellant engines and tanks have a choice of two propellants: `HTP` which is cheap and available at the beginning of career mode, and `Hydrazine` which is unlocked later and more expensive but yields a significantly higher specific impulse.

Solid rockets have a similar progression from `PBAN` to the slightly more performant `HTPB`.

Liquid fuel jet engines use `Kerosene`, with the rocket mode of multimodal engines running on `Kerosene` and `LqdOxygen`.

### CryoTanks changes
This mod replaces all CryoTanks fuel switch types to Chemical Technologies tank types. One particular feature of this is the removal of CryoTanks' native 1.5x hydrogen packing density buff, which not-insignificantly affects the use of LqdHydrogen in the game. This is not just an arbitrary change purely motivated by realism. The ~14% higher density of LqdOxygen over Oxidizer and adjusted methalox mixture ratio (higher oxidizer mass fraction) make cryogenic bipropellants much more attractive, removing the need for any sneaky volume buffs in chemical rockets. Hydrolox suffers a little bit, but I've found this actually balances better against their high Isp. Nuclear engines naturally suffer the most, but again, these engines are very high Isp and it should really be expected that you'd need to haul massive tanks everywhere. I've always wanted my CryoTanks to be bigger, personally.

### Exotic propellants
Four additional exotic propellants — Pentaborane, Diborane, LqdFluorine and N2F4 — are supported by Chemical Propulsion but are not currently implemented anywhere in the basic setup. In the future, some mods may be patched to make use of these propellants, but for now they are only usable via the opt-in patches provided which add exotic subtypes to the default engine configurations.

### Configuration
Engines and RCS can easily be patched to replace their propellants with one of the supported resources by setting one or more `chemTechPropellant` fields on the module, the values of which are strings composed of a propellant type and a resource name:

- `fuel`: A fuel which should be paired with an oxidizer or used in an air-breathing engine.
  - `Ethanol`
  - `Kerosene`
  - `LqdAmmonia`
  - `Hydrazine`
  - `LqdMethane`
  - `LqdHydrogen`
  - `Pentaborane`
  - `Diborane`
- `oxidizer`: An oxidizer which should be paired with a fuel. Supported resource names:
  - `LqdOxygen`
  - `IWFNA`
  - `HTP`
  - `NTO`
  - `LqdFluorine`
  - `N2F4`
- `propellant`: A single propellant which should not be combined with any specified fuel or oxidizer. All above resources are supported.

```
@PART[partName]:BEFORE[zz_ChemicalPropulsion]
{
	@MODULE[ModuleEngines*]
	{
		// Single propellants
		chemTechPropellant = propellantLqdHydrogen // fuelKerosene, oxidizerLqdOxygen etc.
	}
}
```

## Dependencies

- [ModuleManager (4.2.3)](https://github.com/sarbian/ModuleManager)
- [B9PartSwitch (2.20.0)](https://github.com/blowfishpro/B9PartSwitch)
- [Community Resource Pack (112.0.1)](https://github.com/UmbraSpaceIndustries/CommunityResourcePack)
- [Chemical Core (1.2.0)](https://github.com/CharleRoger/ChemicalCore)
- [Ignition (1.1.2)](https://github.com/CharleRoger/Ignition)

## Compatibility
### Recommended
The following mods are recommended to make the most of core set of propellants.

- [Alcoholic Aeronautics (1.0.0)](https://github.com/CharleRoger/AlcoholicAeronautics)
- [Cryogenic Engines (2.0.8)](https://github.com/post-kerbin-mining-corporation/CryoEngines)
- [Cryogenic Tanks (1.6.6)](https://github.com/post-kerbin-mining-corporation/CryoTanks)
- [Kerbal Atomics (1.3.4)](https://github.com/post-kerbin-mining-corporation/KerbalAtomics)
- [Labradoodle (1.0.1)](https://github.com/CharleRoger/Labradoodle)
- [Near Future Launch Vehicles (2.2.2)](https://github.com/post-kerbin-mining-corporation/NearFutureLaunchVehicles)
- [Near Future Spacecraft (1.4.4)](https://github.com/post-kerbin-mining-corporation/NearFutureSpacecraft)
- [Restock and Restock+ (1.5.1)](https://github.com/PorktoberRevolution/ReStocked)
- [Supplementary Electric Engines (1.3.2)](https://forum.kerbalspaceprogram.com/topic/218397-1125-supplementary-electric-engines)

### Suggested
I would also suggest at least a couple of these mods for more bipropellant rockets and useful tanks, or all of them if you like having hundreds of parts.

- [CryoEngines Extensions (1.0.4)](https://forum.kerbalspaceprogram.com/topic/219145-112x-cryoengines-extensions-new-methane-and-hydrogen-engines-fabriqu%C3%A9-au-canada)
- [Knes (1.9.9)](https://github.com/AstroWell/Knes)
- [Near Future Aeronautics (2.1.2)](https://github.com/post-kerbin-mining-corporation/NearFutureAeronautics)
- [Near Future eXploration (1.1.3)](https://github.com/post-kerbin-mining-corporation/NearFutureExploration)
- [OCRAP (1.0.1)](https://github.com/CharleRoger/OCRAP)
- [Tantares (28.0.0)](https://github.com/Tantares/Tantares)
- [TantaresLV (16.2.0)](https://github.com/Tantares/TantaresLV)
- [TantaresSP (6.0.0)](https://github.com/Tantares/TantaresSP)
- [Universal Storage II Finalized (4.0.2.2)](https://github.com/linuxgurugamer/universal-storage-2)

### Compatible
Some mods are explicitly patched to work with Chemical Propulsion, while others are patched implicitly or are simply unaffected and have been found compatible.

- [Airplane Plus (26.5)](https://forum.kerbalspaceprogram.com/topic/140262-14x-18x-airplane-plus-r264-fixed-issuesgithub-is-up-to-date-dec-21-2019) (courtesy of Ari Lana @ratemisia)
- [Configurable Containers (2.6.2.1)](https://github.com/allista/ConfigurableContainers)
- [Far Future Technologies (1.4.2)](https://github.com/post-kerbin-mining-corporation/FarFutureTechnologies)
- [Firespitter (7.17)](https://github.com/snjo/Firespitter)
- [Grounded - Modular Vehicles (5.0)](https://forum.kerbalspaceprogram.com/topic/171377-110x-grounded-modular-vehicles-r50-mining-modules-rotor-emergency-light-jun-5-2019) (courtesy of Ari Lana @ratemisia)
- [Kerbal Reusability Expansion (2.9.3)](https://github.com/TundraMods/Kerbal-Reusability-Expansion)
- [Kerbalism (3.19)](https://github.com/Kerbalism/Kerbalism)
- [MissingHistory (1.9.3)](https://spacedock.info/mod/1743/MissingHistory)
- [Modular Fuel Tanks (5.13.1)](https://github.com/KSP-RO/RealFuels/tree/master/ModularFuelTanks)
- [Mk-33 (1.3.2)](https://github.com/Angel-125/Mk-33)
- [Probes Before Crew (2.93)](https://forum.kerbalspaceprogram.com/topic/181013-ksp-18-112-probes-before-crew-pbc-version-293)
- [Procedural Parts (2.7.2.0)](https://github.com/KSP-RO/ProceduralParts)
- [Shuttle Orbiter Construction Kit (1.1.8)](https://github.com/benjee10/Shuttle-Orbiter-Construction-Kit)
- [Silly Photon Drives (1.1.1)](https://forum.kerbalspaceprogram.com/topic/220997-1125-silly-photon-drives)
- [SystemHeat (0.8.1)](https://github.com/post-kerbin-mining-corporation/SystemHeat)
- [Tundra Exploration (7.1.1)](https://github.com/TundraMods/TundraExploration)
- [UnKerballed Start (1.3.2)](https://github.com/theonegalen/UnKerballedStart)
- Many more, though might do unexpected things. Let me know what else to support!

## License
Distributed under the GNU General Public License.
