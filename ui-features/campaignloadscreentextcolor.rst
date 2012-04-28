.. index:: LoadScreenText.Color;Campaign load screen text color customizable per mission.

===============================
Campaign Load Screen Text Color
===============================

Yuri's Revenge always draws single player campaign load screen texts
in red. Ares uses the correct values, inferred by the mission name
prefix. You can override these defaults for each mission using this
new missionmd.ini tag. 

``[Mission]`` |>| ``LoadScreenText.Color=`` (Color scheme)
	Text on the campaign loading screens for this mission will be drawn using
	this color from the ``[Colors]`` list.
	For example, ``LoadScreenText.Color=AlliedLoad``.

.. versionadded:: 0.2
