---
title: Heater
summary: >
  Heats or cools a batch or a stream at constant pressure. Give a final
  temperature and it finds the duty, or give a duty and it finds the
  temperature reached — melting and boiling included.
---

## What This Models

A heater or cooler at constant pressure: an exchanger, a steam coil, a trim cooler. The fluid is free to expand as it warms, so the energy that matters is its enthalpy.

That is what separates this from the [Vessel Heater](Vessel-Heater) case. A sealed rigid vessel cannot expand, so heating it raises its pressure and the energy that matters is internal energy instead. Use this one for anything flowing through equipment or held at atmospheric pressure; use Vessel Heater for a closed cylinder or drum.

## Inputs

The amount, given whichever way you have it — a mass, a number of moles or a volume for a batch, or a mass, molar, volumetric or normal volumetric flow for a stream. That choice also decides what the answer is: a quantity gives an energy in kJ, a rate gives a power in kW.

Then the starting temperature and the pressure, and finally either the final temperature (and it reports the duty) or the duty (and it reports the temperature reached). The second direction is solved by root-finding the temperature whose enthalpy change matches the duty you gave.

## Phase Changes Are Included

Unlike the [Thermo](Thermo-Tab) tab, which refuses a range that crosses a melting or boiling point, this case walks the range in segments — integrating the solid, liquid or gas heat capacity as appropriate — and adds the latent heat at each boundary it crosses.

## Key Relations

```
Q = n·Δh                  duty is the enthalpy change, constant P
Δh = ∫Cp dT + Σ L_tr       sensible part plus each latent heat crossed
```

n is the amount (or flow); Cp is the heat capacity of whichever phase the range is in at that point; L_tr is the latent heat added at each melting or boiling point the range crosses. Given a duty instead of a final temperature, the same relation is root-found for the T whose Δh matches it. Heating water from -20 °C to 150 °C gives about 3.13 MJ/kg, of which roughly five sixths is L_tr — melting the ice and boiling the water — rather than the ∫Cp dT term. The duty is reported split into its sensible and latent parts for exactly that reason, and the transition temperatures are shown.

The enthalpy of vaporisation is read at the boiling point rather than at the starting temperature, which matters: water reads 2257 kJ/kg at 100 °C against 2442 kJ/kg at 25 °C.

## Mean Heat Capacity

Cp_mean = (∫Cp dT)/(T₂ − T₁) — reported for checking a duty by hand, and it is the sensible heat divided by the temperature span only. Folding L_tr into it would give a number that looks like a heat capacity, is not one, and is wrong by however much of the duty went into the phase change.

## Limitations

One substance at a time: a mixture boils across a range rather than at a point, so its latent heat cannot be placed at a single boundary. A solid that decomposes rather than melting is refused by name — calcium carbonate calcines to CaO and CO2 rather than turning into a liquid, and the enthalpy of fusion listed against it does not describe anything that happens. Heat capacity correlations extrapolate silently outside their fitted range, so treat a duty far outside ordinary process conditions as indicative.

A handful of common plastics (HDPE, LDPE, polypropylene, PET, PVC) can be entered by name here too, heated over their solid range. None of them has a verified melt-phase model behind it, so a range reaching into or through the melt is refused rather than guessed — real resin properties also vary by grade, which the [Property](Property-Tab) tab's entry for each one says more about.
