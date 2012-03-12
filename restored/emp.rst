.. index:: EMP; Ares reintroduces EMP to YR with a more versatile system.

===
EMP
===

Vehicles affected by EMP (Electromagnetic Pulse) are paralyzed in a
similar manner to a Chrono Legionnaire erasing a unit. Unlike the
Chrono Legionnaire however, EMP'd vehicles can still be attacked by
other units.
EMP paralysis affects units and buildings in various ways (given they
are not immune to EMP, see below):


+ Primary effect: units will not respond to any commands. They will
  stop moving and will not attack anything.
+ Hovering units (such as the Robot Tank) will land.
+ Units display the animation specified by
  ``[General]`` |>| ``EMPulseSparkles=EMP_FX01``. Note that the :file:`emp_fx01.shp` file
  that comes with Red Alert 2 is in the Tiberian Sun palette and needs
  to be converted.
+ Voxel-based units are darkened (SHP-based units are not).
+ Buildings that can undeploy into vehicles (e.g. MCVs) still can, but
  the resulting vehicle will remain EMP'd until the effect wears off.
+ Aircraft will immediately crash.
+ Power plants cease to produce power.
+ Factories will stop working.
+ Base defenses will not be able to fire their weapon.
+ Gap Generators will stop emitting radar gap.
+ Laser Fence Posts will stop emitting laser fences.
+ Robot Control Centers will stop working.
+ Super weapon buildings will shut down and the super weapons
  themselves will stop charging, if they have
  ``[SuperWeapon]`` |>| ``IsPowered=yes`` set.
+ Radar buildings will stop providing radar.
+ SpySat buildings will stop to reveal the map.
+ Units that spawn other units will cease to do so. If the spawner
  unit has launched any aircraft then the aircraft will immediately
  crash.
+ Slave Miner slaves will stop working.
+ Units that are in their unloading state (such as ore harvesters
  depositing ore or Siege Choppers transforming) will only become EMP'd
  once they have finished unloading.
+ Harvesters that were in the middle of harvesting when hit by EMP
  will resume harvesting after EMP wears off.
  
.. note::
	Tiberian Sun used the weapon's ``Damage`` flag to determine how long
	the EMP effect would last. Ares, however, uses 2 new flags
	(``EMP.Duration`` and ``EMP.Cap``) to provide greater control. The weapon's
	Damage will be delivered independently from EMP paralysis (so a weapon
	can both damage and paralyze its target). Tiberian Sun also used the
	flag ``EMEffect=yes``, which is not used in Ares.

Using EMP
---------
The game keeps track of how much longer each unit will remain
paralyzed. Each unit essentially has a hidden EMP counter that counts
down frame by frame until it reaches zero, at which point the unit
will be re-activated. This counter is what gets modified by EMP
warheads.

``[Warhead]`` |>| ``EMP.Duration=`` :term:`integer` (frames)
	Determines how many frames are added to or subtracted from the target's EMP counter if the weapon hits.

``[Warhead]`` |>| ``EMP.Cap=`` :term:`integer` (frames)
	Defines a limit for the target's EMP counter. The weapon will ensure the
	target's EMP counter does not end up higher than this through the attack.
	
.. admonition:: Quickstart

	If you want a warhead to EMP a target for ten seconds, set ``EMP.Duration=150`` on the warhead.

.. important::
	``Verses`` do not affect the duration or cap of an EMP weapon, they solely
	decide whether the effect is applied at all. If the ``Verses`` are ``0%`` or
	negative, no EMP effect is applied, if they are positive, the effect as declared
	by ``EMP.Duration=`` and ``EMP.Cap=`` is applied.

Different Flag Combinations
---------------------------
+-------------------------+----------------------------------------------------------------+----------------------------------------------------------------+
|                         | ``EMP.Duration`` is positive                                   | ``EMP.Duration`` is negative                                   |
+-------------------------+----------------------------------------------------------------+----------------------------------------------------------------+
| ``EMP.Cap`` is positive | The EMP counter is increased by the value of ``EMP.Duration``, | The EMP counter is reduced by the value of ``EMP.Duration``.   |
|                         | up to, but not beyond the value of ``EMP.Cap``.                | If this value is still greater than ``EMP.Cap`` then the EMP   |
|                         |                                                                | counter is reduced further so that it is equal to ``EMP.Cap``. |
+-------------------------+----------------------------------------------------------------+----------------------------------------------------------------+
| ``EMP.Cap`` is zero     | The EMP counter is increased by the value of ``EMP.Duration``. | ``EMP.Duration`` is ignored. The EMP counter will be set to    |
|                         |                                                                | zero and the unit will re-activate.                            |
+-------------------------+----------------------------------------------------------------+----------------------------------------------------------------+
| ``EMP.Cap`` is -1       | The EMP counter is set to the value of ``EMP.Duration``, unless| The target's EMP counter is reduced by the value               |
|                         | the counter is already higher than that.                       | of ``EMP.Duration``.                                           |
+-------------------------+----------------------------------------------------------------+----------------------------------------------------------------+

.. note::
	-1 is the only supported negative value for ``EMP.Cap``. Values smaller than that should not be used and will be rejected by support staff.

Examples
--------
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| Target's EMP counter | ``EMP.Duration`` | ``EMP.Cap`` | Result                                                             |
+======================+==================+=============+====================================================================+
|  0                   |  10              | 20          | EMP counter will be set to 10.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 15                   |  10              | 20          | EMP counter will be set to 20.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 60                   |  10              | 20          | EMP counter will remain at 60.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 25                   |  10              | 0           | EMP counter will be set to 35.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
|  5                   |  10              | -1          | EMP counter will be set to 10.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 20                   |  10              | -1          | EMP counter will remain at 20.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 50                   | -10              | -1          | EMP counter will be set to 40.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
|  7                   | -10              | -1          | EMP counter will be set to zero and the unit will re-activate.     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 50                   | -10              | 70          | EMP counter will be set to 40.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| 50                   | -10              | 20          | EMP counter will be set to 20.                                     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
|  7                   | -10              | 20          | EMP counter will be set to zero and the unit will re-activate.     |
+----------------------+------------------+-------------+--------------------------------------------------------------------+
| Any                  | Any Negative     | 0           | The EMP counter will be set to zero and the unit will re-activate. |
+----------------------+------------------+-------------+--------------------------------------------------------------------+

Immunity
--------
.. admonition:: Quickstart

	If you want a unit to be immune to EMP, set ``ImmuneToEMP=yes`` on the unit.

``[TechnoType]`` |>| ``ImmuneToEMP=`` :term:`boolean`
	Specifies whether or not the TechnoType is immune to the effects of EMP.
	
Default Value
~~~~~~~~~~~~~
The default immunity status is determined based on the following rules:

**BuildingTypes**
	``ImmuneToEMP`` defaults to ``no`` for BuildingTypes that
	have ``Powered=yes`` and a negative ``Power=`` value set. ``ImmuneToEMP``
	defaults to ``no`` for BuildingTypes that provide one or more of the
	following special functions:
	
		+ Radar
		+ Super weapons
		+ Undeploy into a vehicle (e.g. Construction Yards)
		+ Powers vehicles (e.g. Robot Control Centre)
		+ Gap Generator
		+ Sensors
		+ Laser Fence Posts
	  
	``ImmuneToEMP`` defaults to ``yes`` for all other BuildingTypes. For
	instance, power plants and pillboxes are immune to EMP by default, as
	well as SpySat buildings and factories.

**InfantryTypes**
	``ImmuneToEMP`` defaults to ``yes`` for InfantryTypes unless ``Cyborg=yes``
	is set (in which case ``ImmuneToEMP`` defaults to ``no``).

**VehicleTypes** and **AircraftTypes**
	``ImmuneToEMP`` defaults to ``no`` for VehicleTypes and AircraftTypes unless
	``Organic=yes`` is set (in which case, ``ImmuneToEMP`` defaults to ``yes``).
	  
Manually setting ``ImmuneToEMP`` always overrides the default. EMP immunity can
also be granted via the new veteran/elite ability ``EMPIMMUNE``. Just set
``VeteranAbilities=EMPIMMUNE`` or ``EliteAbilities=EMPIMMUNE`` on the TechnoType.
EMP immunity also respects ``TypeImmune``, ``AffectsAllies`` and ``AffectsEnemies``
on the warhead.

Unit-based Multiplier
---------------------
``[TechnoType]`` |>| ``EMP.Modifier=`` (multiplier)
	If the EMP effect ``Duration`` is positive, it will be multiplied by this factor.
	You can create units that are more or less prone to the Electromagnetic Pulse.
	``EMP.Modifier`` defaults to ``100%``.

.. seealso::
	:doc:`../new/destroyunitsbyemp` to learn how to crash flying TechnoTypes.

.. versionadded:: 0.1

