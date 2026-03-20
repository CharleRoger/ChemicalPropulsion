# Tag-patch process

Chemical Propulsion uses several automatic patching stages which each identify the presence of simple variables added to parts via ModuleManager in previous stages and uses them to create functional data on the Part. An overview of the patch stages can be found in `README.md`.

This process can be used, intercepted, hijacked, and bypassed to get the configuration you want onto a part.

## Automatic tags and patches

### First stage tags

Without any bespoke compatibility patches, the tag-patch system modifies many parts by automatically assigning first-stage tags which then activate and propagate to the later stages of the patch process. Some examples include:
- Various kinds of engines using usual propellants like `LiquidFuel`/`Oxidizer`, `MonoPropellant`, `SolidFuel`, or `LqdHydrogen`, and even certain kinds of multi-mode engine, are tagged to use the relevant core Chemical Propulsion propellants.
	- `LiquidFuel`/`Oxidizer` is converted to `Kerosene`/`LqdOxygen` by default, which often happens to be correct but is of course inappropriate for many engines.
- *Any* part with a `RESOURCE` node containing `MonoPropellant`, `LiquidFuel`, `LiquidFuel` and `Oxidizer`, or `LqdHydrogen` has the tank volume computed and tagged on the part.
	- A `chemTechTankType` is additionally automatically tagged on the part if and only if it does not already have one and it has no modules which contain `PROPELLANT` nodes, for example a `ModuleEngines*` à la SRBs and LRBs. This makes sure that only "proper" tanks which don't affect other modules end up with bespoke propellant switches. On combined tank/engine boosters for example, the same propellant switch which controls the `ModuleEngines*` gets plumbed in to the `ModuleIgnitionTankController`.
		- Parts which do other things but nonetheless have independent tanks, e.g. a command pod with a `RESOURCE` node with `MonoPropellant`, are just treated like tanks and thus receive the `chemTechTankType` tag.

### Subsequent stage tags

Subsequent stages will identify the presence of the first-stage tags and create functional modules and other data on the part and sometimes create second-stage tags which are identified by further stages of the process, and so on.

## Manual tags and patches

The main way to interface with the tag-patch system and bypass the auto-computed data is to add/replace/remove tags to a part at certain points in the process, specified with `:FOR[...]` on the top level of the patch. A bespoke patch intercepting the tag-patch process at the right stage can prevent certain automatic tags described above from being added, while allowing any subsequent automatic patching stages which depend on the newly specified data to continue as normal.
- See `chemical-propulsion-Squad.cfg` for example.

Sometimes a little bit of extra plumbing is needed, e.g. for multi-mode engines which are not handled by the automatic patches.
- See `chemical-propulsion-Mk33.cfg` for example.

Sometimes some manipulation of the auto-computed data or extra computation will also need to be done, e.g. for tank volumes.
- See `chemical-propulsion-Benjee10_shuttleOrbiter.cfg` and `chemical-propulsion-ChemicalStorage.cfg` for example.

### B9PartSwitch modules...

By far the most laborious part of writing compatibility patches is dealing with existing B9PartSwitch modules which modify data relevant to Chemical Propulsion.

#### ... which only change tank contents

These should be removed and replaced with the Ignition-based part switching set up by Chemical Propulsion.
- This should be as simple as setting appropriate tank type and volume tags.
	- See `chemical-propulsion-NearFutureAeronautics.cfg` for example.
	- Depending what we find, we might need to add a new tank type.
	- Note that B9PartSwitch tank volumes are specified in stock LFO units which are for some reason five litres, while Ignition uses litres, so a x5 conversion factor must be applied.

#### ... which change other things

These should be retained and modified.
- This should mean we will not need to touch part upgrades or unrelated part changes like active meshes.
- Subtypes...
	- ... which essentially only change the tank contents, but also have model/texture changes:
		- The existing subtypes should be changed to use Chemical Core's single-propellant or Chemical Propulsion's bipropellant B9 tank types, retaining the original subtypes if possible or otherwise at least keeping an equivalent structure.
			- See `chemical-propulsion-NearFutureExploration.cfg` for example.
			- This can get a bit messy!
	- ... which change tank volume:
		- `volumeAdded`, `addedMass` and `addedCost` should be set to zero if present or just removed since `ModuleIgnitionTankController` handles these.
			- See `chemical-propulsion-OCRAP.cfg` for example.
	- ... which modify `ModuleEngines*`:
		- Need to apply the modifications to `ModuleIgnitionEngineController` instead.
			- See `chemical-propulsion-OCRAP.cfg` for example.
	- ... which modify `ModuleRCS*`:
		- Need to apply the modifications to `ModuleIgnitionRCSController` instead.