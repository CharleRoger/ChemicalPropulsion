# Chemical Propulsion
An overhaul to the stock propellant system, replacing generic LiquidFuel, Oxidizer and MonoPropellant with a handful of real chemicals.
This mod is distinct from RealFuels in that it deals with only a short list of resources — Kerosene, HTP, LqdOxygen, LqdHydrogen, LqdMethane, LqdAmmonia, Hydrazine, NTO, Pentaborane, Diborane and LqdFluorine — for a straightforward enhanced propellant system more in line with Nertea's Cryogenic Engines. In fact, Nertea's mods are a particular target of this overhaul, which can be thought of as a Nertea-like soft alternative to RealFuels.

## Features
### Engine changes
Monopropellant engines and tanks have a choice of two propellants: HTP which is cheap and available at the beginning of career mode, and Hydrazine which is unlocked later and more expensive but yields a significantly higher specific impulse.

LiquidFuel/Oxidizer engines are categorised into one of four types, each of which similarly has a pair "basic" and "advanced" bipropellants with fixed mixture ratios:
- Hypergolic:
  - 2 LqdAmmonia / 3 NTO
  - 7 Hydrazine / 9 NTO
  - 11 Pentaborane / 5 NTO
- Kerolox:
  - 1 Kerosene / 3 HTP
  - 3 Kerosene / 5 LqdOxygen
  - 3 Kerosene / 5 LqdFluorine
- Methalox:
  - 7 LqdMethane / 9 LqdOxygen (a more fuel-rich, more realistic figure than CryoEngines/CryoTanks native 3 LqdMethane / 1 Oxidizer)
  - 7 LqdMethane / 9 LqdFluorine
  - 7 Diborane / 9 LqdOxygen
  - 7 Diborane / 9 LqdFluorine
- Hydrolox:
  - 3 LqdHydrogen / 1 LqdOxygen (roughly equivalent in mass to CryoEngines/CryoTanks native 15 LqdHydrogen / 1 Oxidizer)
  - 3 LqdHydrogen / 1 LqdFluorine

Near Future Launch Vehicles' KR-701 'Cougar' and KR-74 'Lynx' are bimodal hydrolox engines with an additional kerosene-augmented mode, based on their real-world analogues the RD-701 and RD-704:
  - 1 Kerosene / 4 LqdHydrogen / 3 LqdOxygen (equivalent to 1 part kerolox + 2 part2 hydrolox)

Jet engines use Kerosene, with the rocket mode of multimodal engines running on Kerosene/LqdOxygen.

Engines can easily be patched to replace their propellants with one of the combinations above like the following:
```
@PART[partName]:FOR[ChemicalPropulsion]
{
	@MODULE[ModuleEngines*]
	{
		chemTechEngineType = monopropellant // hypergolic, kerolox, methalox, hydrolox, kerohydrolox, keroseneJet, hydrogenJet
	}
}
```
### CryoTanks changes
This mod replaces all CryoTanks fuel switch types to Chemical Technologies tank types. One particular feature of this is the removal of CryoTanks' native 1.5x hydrogen packing density buff, which not-insignificantly affects the use of LqdHydrogen in the game. This is not just an arbitrary change purely motivated by realism. The ~14% higher density of LqdOxygen over Oxidizer and adjusted methalox mixture ratio (higher oxidizer mass fraction) make cryogenic bipropellants much more attractive, removing the need for any sneaky volume buffs in chemical rockets. Hydrolox suffers a little bit, but I've found this actually balances better against their high Isp (particularly when you start getting into exotics like liquid fluorine). Nuclear engines naturally suffer the most, but again, these engines are very high Isp and it should really be expected that you'd need to haul massive tanks everywhere. I've always wanted my CryoTanks to be bigger, personally.

## Dependencies
### Required
- [ModuleManager (4.2.3)](https://github.com/sarbian/ModuleManager)
- [B9PartSwitch (2.20.0)](https://github.com/blowfishpro/B9PartSwitch)
- [Chemical Core (0.4.0)](https://github.com/CharleRoger/ChemicalCore)
- [FuelMixer (0.1.0)](https://github.com/CharleRoger/FuelMixer)
### Supported
- [Cryogenic Engines (2.0.7)](https://github.com/post-kerbin-mining-corporation/CryoEngines)
- [Cryogenic Tanks (1.6.6)](https://github.com/post-kerbin-mining-corporation/CryoTanks)
- [Kerbal Atomics (1.3.4)](https://github.com/post-kerbin-mining-corporation/KerbalAtomics)
- [Near Future Launch Vehicles (2.2.1)](https://github.com/post-kerbin-mining-corporation/NearFutureLaunchVehicles)
- [Restock and Restock+ (1.5.1)](https://github.com/PorktoberRevolution/ReStocked)
- Many other mods implicitly, though might do unexpected things. Let me know what else to support!

If you'd like to add support for other mods yourself, I'll accept any pull requests.

## Compatibility
Backwards compatibility is not guaranteed for any v0.x, use at your own risk. If you find any other mod to be incompatible with this one, please let me know via a github issue.

## License
Distributed under the GNU General Public License.
