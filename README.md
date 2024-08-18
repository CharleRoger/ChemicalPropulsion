# Immersive Chemical Propulsion
An overhaul to the stock propellant system, replacing generic LiquidFuel, Oxidizer and MonoPropellant with a handful of real chemicals.
This mod is distinct from RealFuels in that it only deals with six resources — Kerosene, LqdOxygen, LqdHydrogen, LqdMethane, Hydrazine and NTO — for a straightforward enhanced propellant system more in line with Nertea's Cryogenic Engines. In fact, Nertea's mods are a particular target of this overhaul, which can be thought of as a Nertea-like soft alternative to RealFuels.

LiquidFuel/Oxidizer engines and tanks are set to fixed ratios for the following propellant mixtures:
 - 2 Hydrazine / 3 NTO
 - 3 Kerosene / 5 LqdOxygen
 - 3 LqdHydrogen / 1 LqdOxygen
 - 7 LqdMethane / 9 LqdOxygen
 - 1 Kerosene / 4 LqdHydrogen / 3 LqdOxygen (equivalent to 1/3 kerolox + 2/3 hydrolox)
Exotic fuel mixtures are also provided, but not used for anything (yet):
 - 3 Pentaborane / 7 LqdFluorine
 - 3 LqdHydrogen / 1 LqdFluorine

Engines can easily be patched to replace their propellants with one of the combinations above like the following:
```
@PART[partName]:FOR[ImmersiveChemicalPropulsion]
{
    @MODULE[ModuleEngines*]
    {
        icPropellantType = Hydrazine_NTO // Kerosene_LqdOxygen, LqdHydrogen_LqdOxygen, LqdMethane_LqdOxygen, Kerosene_LqdHydrogen_LqdOxygen, Pentaborane_LqdFluorine, LqdHydrogen_LqdFluorine
    }
}
```

## Dependencies
### Required
- [ModuleManager (4.2.3)](https://github.com/sarbian/ModuleManager)
- [B9PartSwitch (2.20.0)](https://github.com/blowfishpro/B9PartSwitch)
- [Immersive Chemical Core (0.1.0)](https://github.com/CharleRoger/ImmersiveChemicalCore)
- [Cryogenic Tanks (1.6.6)](https://github.com/post-kerbin-mining-corporation/CryoTanks)
### Supported
- [Cryogenic Engines (2.0.6)](https://github.com/post-kerbin-mining-corporation/CryoEngines)
- [Kerbal Atomics (1.3.3)](https://github.com/post-kerbin-mining-corporation/KerbalAtomics)
- [Near Future Launch Vehicles (2.2.1)](https://github.com/post-kerbin-mining-corporation/NearFutureLaunchVehicles)
- [Restock and Restock+ (1.4.5)](https://github.com/PorktoberRevolution/ReStocked)
- Many other mods implicitly, though might do unexpected things. Let me know what else to support!

If you'd like to add support for other mods yourself, I'll accept any pull requests.

## License
Distributed under the GNU General Public License.