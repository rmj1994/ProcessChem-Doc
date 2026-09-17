---
title: Vessel Heater
summary: >
  A sealed rigid vessel is heated or cooled. Finds the resulting pressure,
  phase and liquid level, and flags the liquid-full overpressure hazard.
---

## What This Models

A rigid, sealed vessel whose contents are heated or cooled — fire exposure, solar gain, steam-out, loss of cooling, or an ambient swing. The vessel does not vent and does not change volume, so both the total volume and the mass inside are constant and the molar volume is fixed.

## Inputs

Vessel volume, entered directly or as diameter + tangent-to-tangent length with a head type (2:1 elliptical, hemispherical or flat). Contents given either as a mass or as the initial pressure — if you give the pressure, the mass is back-calculated from the equation of state, and vice versa. Then the initial temperature, and finally the driver: either a heat duty added or removed, or the final temperature you want to reach.

## Method

Constant volume and constant mass fix the molar volume; the final state then follows from the first law with no work term, in either direction.

## Key Relations

```
V_m = V/n                    fixed, from the constant volume and mass
Q = n·(U₂ − U₁)               final temperature given -> duty found
U₂ = U₁ + Q/n                 duty given -> target U, then T solved
```

V_m is the molar volume, fixed for the whole calculation. Given a final temperature, the final state is a T,V_m flash and the duty follows directly. Given a duty instead, the target internal energy U₂ is known and the final temperature is found by root-finding on that same T,V_m flash.

The two-phase region is handled explicitly rather than left to the equation of state: a plain T,V_m flash inside the saturation dome puts the liquid under tension and returns a negative pressure, so the saturation envelope is checked first and a two-phase state is solved at the vapour fraction x satisfying x·V_m,g + (1−x)·V_m,l = V_m — the fraction that reproduces the vessel's own molar volume.

## The Liquid-Full Warning

When heating drives the vapour fraction to zero, the vessel is liquid-full. Past that point there is no compressible vapour space left, and pressure rises almost vertically with temperature — a few degrees more can mean hundreds of bara. The calculation still reports a number, but it is extremely sensitive to both the temperature and the accuracy of the liquid density, so treat it as an indication that relief is required, not as a design pressure.

## Limitations

The vessel is rigid (no elastic expansion of the shell, which in reality relieves a little of the hydraulic pressure rise), perfectly sealed, and uniform in temperature. Vessel wall heat capacity is not included, so a given duty heats the contents faster than it would in reality. There is no relief device — this is the unrelieved case, which is exactly what you size relief against.
