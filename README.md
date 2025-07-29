# Chemical Propulsion
An overhaul to the stock propellant system, replacing generic LiquidFuel, Oxidizer, MonoPropellant and SolidFuel with a handful of real chemicals.

## Features
### Core design
This mod is distinct from RealFuels in that it deals with only a small set of primary liquid propellants, for a more straightforward and curated propellant system more in line with e.g. Nertea's Cryogenic Engines. In fact, Nertea's mods are a particular target of this overhaul, which can be thought of as a Nertea-like soft alternative to RealFuels.

Each propellant has a part upgrade which provides switch subtypes on relevant parts when unlocked in the tech tree. Most propellants only appear in game if a using-mod is present, while the following six are used in a pure stock configuration:

- `LqdOxygen`
- `Kerosene`
- `HTP` (High-test peroxide)
- `Hydrazine`
- `LqdHydrogen`
- `NTO` (Dinitrogen tetroxide)

### Engine changes
Bipropellant engines are categorised into particular fuel-oxidizer combinations with fixed mixture ratios. Any fuel can be paired with any oxidizer, though not all combinations are necessarily configured or available depending on which supported mods you use. The bipropellants used in stock are:

- Keroxide:
  - 1 `Kerosene` / 3 `HTP`
- Hypergolic:
  - 7 `Hydrazine` / 9 `NTO`
- Kerolox:
  - 3 `Kerosene` / 5 `LqdOxygen`
- Hydrolox:
  - 3 `LqdHydrogen` / 1 `LqdOxygen`

Monopropellant engines and tanks have a choice of two propellants: `HTP` which is cheap and available at the beginning of career mode, and `Hydrazine` which is unlocked later and more expensive but yields a significantly higher specific impulse.

Solid rockets have a similar progression from `PBAN` to the slightly more performant `HTPB`.

Liquid fuel jet engines use `Kerosene`, with the rocket mode of multimodal engines running on `Kerosene` and `LqdOxygen`.

Some mod engines have bespoke propellant configurations which are not typical monopropellants or bipropellants. For example, Near Future Launch Vehicles' KR-701 'Cougar' and KR-74 'Lynx' are bimodal hydrolox engines with an additional kerosene-augmented mode, based on their real-world analogues the RD-701 and RD-704:

- 1 `Kerosene` / 4 `LqdHydrogen` / 3 `LqdOxygen` (equivalent to 1 part kerolox + 2 parts hydrolox)

### CryoTanks changes
This mod replaces all CryoTanks fuel switch types to Chemical Technologies tank types. One particular feature of this is the removal of CryoTanks' native 1.5x hydrogen packing density buff, which not-insignificantly affects the use of LqdHydrogen in the game. This is not just an arbitrary change purely motivated by realism. The ~14% higher density of LqdOxygen over Oxidizer and adjusted methalox mixture ratio (higher oxidizer mass fraction) make cryogenic bipropellants much more attractive, removing the need for any sneaky volume buffs in chemical rockets. Hydrolox suffers a little bit, but I've found this actually balances better against their high Isp. Nuclear engines naturally suffer the most, but again, these engines are very high Isp and it should really be expected that you'd need to haul massive tanks everywhere. I've always wanted my CryoTanks to be bigger, personally.

### Configuration
Engines and RCS can easily be patched to replace their propellants with one of the supported resources by setting one or more `chemTechPropellant`, `chemTechFuel` or `chemTechOxidizer` fields on the module, the values of which are a resource name:

- `chemTechFuel`: A fuel which should be paired with an oxidizer or used in an air-breathing engine.
  - `Ethanol`
  - `Kerosene`
  - `Aniline`
  - `LqdAmmonia`
  - `Hydrazine`
  - `LqdMethane`
  - `LqdHydrogen`
  - `Pentaborane`
  - `Diborane`
- `chemTechOxidizer`: An oxidizer which should be paired with a fuel. Supported resource names:
  - `LqdOxygen`
  - `IWFNA`
  - `HTP`
  - `NTO`
  - `LqdFluorine`
  - `N2F4`
- `chemTechPropellant`: A single propellant which should not be combined with any specified fuel or oxidizer. All above resources are supported, plus the following:
  - `Water`
  - `LqdCO2`
  - `LqdCO`
  - `LqdNitrogen`

For example, the following patch converts a multimode engine with a pure LiquidFuel mode and a LiquidFuel-Oxidizer mode to use LqdHydrogen and LqdOxygen:
```
@PART[partName]:BEFORE[zz_ChemicalPropulsion]
{
	@MODULE[ModuleEngines*]:HAS[@PROPELLANT[LiquidFuel],!PROPELLANT[Oxidizer]]
	{
		chemTechPropellant = LqdHydrogen
	}

	@MODULE[ModuleEngines*]:HAS[@PROPELLANT[LiquidFuel],@PROPELLANT[Oxidizer]]
	{
		chemTechFuel = LqdHydrogen
		chemTechOxidizer = LqdOxygen
	}
}
```

## Extras
Some patches for additional propellant options are provided in the Extras folder.

### Keroxide
Adds HTP as an oxidizer option to all kerolox engines, which is more expensive and yields slightly lower Isp than LqdOxygen, but has two main advantages:

- An ignition mechanism is not required as the hot gases produced by the catalytic decomposition of HTP ignite on contact with Kerosene
- HTP is much denser than LqdOxygen and has a higher oxidizer-fuel mixture ratio with Kerosene, so the volumetric impulse is actually slightly higher than that of kerolox

### Hypergolics
Adds an alternative pair of cheaper, lower-performance fuel and oxidizer to all hypergolic engines:

- `Aniline` - Low-tech alternative to Hydrazine
- `IWFNA` (Nitric acid) - Low-tech alternative to NTO

### Exotics
Adds four exotic propellants which are unlocked late in the tech tree and can replace certain conventional propellants for increased thrust and Isp:

- `Pentaborane` - Can be used in place of Hydrazine as a hypergolic fuel or Kerosene as a jet fuel
- `Diborane` - Can be used in place of LqdMethane as a cryogenic fuel
- `N2F4` - Can be used in place of NTO as a hypergolic cryogenic oxidizer
- `LqdFluorine` - Can be used in place of LqdOxygen as a cryogenic oxidizer

### Nuclear
Adds four high-thrust, low-Isp propellant options to nuclear thermal rockets (multipliers vs. LqdHydrogen):

- `Water` - +92% thrust, -58% Isp
- `LqdCO2` - +142% thrust, -69% Isp
- `LqdCO` - +158% thrust, -72% Isp
- `LqdNitrogen` - +158% thrust, -72% Isp

## Dependencies

- [ModuleManager (4.2.3)](https://github.com/sarbian/ModuleManager)
- [B9PartSwitch (2.21.0.1)](https://github.com/KSPModStewards/B9PartSwitch)
- [Community Resource Pack (112.0.1)](https://github.com/UmbraSpaceIndustries/CommunityResourcePack)
- [Chemical Core (1.4.0)](https://github.com/CharleRoger/ChemicalCore)
- [Ignition (1.2.0.1)](https://github.com/CharleRoger/Ignition)
- [Space Dust Next (3.0.0)](https://github.com/NerdyBoy709/SpaceDustNext) (only if using [Space Dust](https://github.com/post-kerbin-mining-corporation/SpaceDust))

## Compatibility
### Recommended
The following mods are recommended to make the most of core set of propellants.

- [Alcoholic Aeronautics (1.0.0)](https://github.com/CharleRoger/AlcoholicAeronautics)
- [Cryogenic Engines (2.0.8)](https://github.com/post-kerbin-mining-corporation/CryoEngines)
- [Cryogenic Tanks (1.6.7)](https://github.com/post-kerbin-mining-corporation/CryoTanks)
- [Kerbal Atomics (1.3.4)](https://github.com/post-kerbin-mining-corporation/KerbalAtomics)
- [Labradoodle (1.0.1)](https://github.com/CharleRoger/Labradoodle)
- [Near Future Launch Vehicles (2.2.2)](https://github.com/post-kerbin-mining-corporation/NearFutureLaunchVehicles)
- [Near Future Spacecraft (1.4.4)](https://github.com/post-kerbin-mining-corporation/NearFutureSpacecraft)
- [Restock and Restock+ (1.5.1)](https://github.com/PorktoberRevolution/ReStocked)
- [Supplementary Electric Engines (1.3.2)](https://forum.kerbalspaceprogram.com/topic/218397-1125-supplementary-electric-engines)
- [VABOrganizer (1.1.0)](https://github.com/post-kerbin-mining-corporation/VABOrganizer)

### Suggested
I would also suggest at least a couple of these mods for more bipropellant rockets and useful tanks, or all of them if you like having hundreds of parts.

- [BlueSteel (1.3)](https://github.com/AstroWell/BlueSteel)
- [CRE (2.3)](https://github.com/Tantares/CRE)
- [CryoEngines Extensions (1.0.4)](https://forum.kerbalspaceprogram.com/topic/219145-112x-cryoengines-extensions-new-methane-and-hydrogen-engines-fabriqu%C3%A9-au-canada)
- [Knes (1.9.9)](https://github.com/AstroWell/Knes)
- [Near Future Aeronautics (2.1.2)](https://github.com/post-kerbin-mining-corporation/NearFutureAeronautics)
- [Near Future eXploration (1.1.3)](https://github.com/post-kerbin-mining-corporation/NearFutureExploration)
- [OCRAP (1.0.1)](https://github.com/CharleRoger/OCRAP)
- [Space Dust (0.5.5)](https://github.com/post-kerbin-mining-corporation/SpaceDust)
- [Taerobee (1.4.3.0)](https://github.com/zer0Kerbal/Taerobee)
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
- [SystemHeat (0.8.2)](https://github.com/post-kerbin-mining-corporation/SystemHeat)
- [Tundra Exploration (7.1.1)](https://github.com/TundraMods/TundraExploration)
- [UnKerballed Start (1.3.2)](https://github.com/theonegalen/UnKerballedStart)
- Many more, though might do unexpected things. Let me know what else to support!

## License
Distributed under the GNU General Public License.
