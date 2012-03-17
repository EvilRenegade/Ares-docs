.. index:: Multi Engineer

Multi Engineer
~~~~~~~~~~~~~~

Red Alert introduced a way to balance engineers. By being able to
capture a building only if has been damaged already engineer rushes
became a lot more difficult. If the building could not be captured the
engineer would damage it instead. ``EngineerDamage`` is not present in
Yuri's Revenge. Ares restores this feature.

.. todo::
	Add image here.

``[General]`` |>| ``EngineerCaptureLevel=`` :term:`float` (level)
	Specifies the health level equal to or below the building has to be capture it.
	
``[General]`` |>| ``EngineerDamage=`` :term:`float` (percent)
	If the building can not be captured the engineer will damage it by this
	amount of its full health.

``[General]`` |>| ``EngineerAlwaysCaptureTech=`` :term:`boolean`
	Specifies whether tech buildings can be captured no matter what their current
	health status is.

``[General]`` |>| ``EngineerDamageCursor.*=`` (Cursor)
	Specifies the cursor to indicate an engineer will only damage the building
	instead of capturing it. See :ref:`Super Weapon Cursors <sw-cursors>`.
	Defaults to a previously unused detonator cursor.

.. note::
	Use sensible defaults. Generally, ``EngineerDamage`` should never be
	higher than ``EngineerCaptureLevel`` or there might be situations an
	engineer blows up the building to be captured.

.. seealso::
	See :doc:`multiengineercheckbox` to enable the user to turn the Multi
	Engineer option on and off from the game menu. If the checkbox is not
	enabled, the game will force the settings defined in rulesmd.ini.

.. versionadded:: 0.2

