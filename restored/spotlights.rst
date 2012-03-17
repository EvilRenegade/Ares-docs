Spotlights
~~~~~~~~~~

Spotlights would cause an Internal Error whenever they were created.
The error no longer occurs so spotlights can now be used. Spotlights

``[Unit]`` |>| ``HasSpotlight=`` :term:`boolean`
	If set to ``yes``, creates a spotlight from the unit (note that this is now
	available to all of the Big Four types, not just BuildingTypes). When
	attached to a BuildingType, the spotlight still behaves like it used to,
	just circling around, but when it is attached to a different unit type,
	such as a VehicleType, it is fixed to shine straight ahead.
``[Unit]`` |>| ``Spotlight.StartHeight=`` :term:`integer` (leptons)
	Specifies the number of leptons above the ground at which the spotlight will
	be generated. Defaults to 250.
``[Unit]`` |>| ``Spotlight.Distance=`` :term:`integer - leptons`
	The number of leptons ahead of the unit where the spotlight will reach the ground.
	Defaults to 1024.
``[Unit]`` |>| ``Spotlight.AttachedTo=`` :term:`enumeration` (one of ``body``|``turret``|``barrel``)
	The part of the unit that the spotlight will align to in regards to facing.
	If set to ``body`` then the spotlight will be pointed in the direction the
	unit's body is facing, if set to ``turret`` then the spotlight will be pointed
	in the direction the unit's turret is facing. Does not work on BuildingTypes.
	Defaults to ``body``.
``[Unit]`` |>| ``Spotlight.DisableRed=`` :term:`boolean`
	If set to yes then the spotlight will not emit any red light.
	Defaults to ``no``.
``[Unit]`` |>| ``Spotlight.DisableGreen=`` :term:`boolean`
	If set to yes then the spotlight will not emit any green light.
	Defaults to ``no``.
``[Unit]`` |>| ``Spotlight.DisableBlue=`` :term:`boolean`
	If set to yes then the spotlight will not emit any blue light.
	Defaults to ``no``.
``[Unit]`` |>| ``Spotlight.DisableColor=`` :term:`boolean`
	If set to ``yes`` then the spotlight will paint the ground darker, instead of
	brighter, and the disable red/green/blue flags mentioned above will be ignored.

.. versionadded:: 0.1

