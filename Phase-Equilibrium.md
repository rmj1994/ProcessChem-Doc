---
title: Phase Equilibrium
summary: >
  One chemical changes state — heated, cooled, compressed, expanded or
  throttled. Give the amount as a quantity for a sealed vessel or as a rate
  for a flowing stream; finds the final state and the heat and work.
---

## What This Models

A substance moving from one state to another, either as a fixed amount in a vessel or piston, or as a steady stream through a device. Both are the same equation of state answering the same question; what separates them is whether you have a quantity or a rate.

## The Amount Decides Which

Enter a mass, a number of moles or a volume and this is a closed system: a fixed amount in a vessel, where the work is n times the change in internal energy. Enter a mass flow, molar flow, volumetric flow or normal flow and it is an open system: a stream through a compressor, turbine, exchanger or valve, where the shaft work is the molar flow times the change in enthalpy. You do not choose between them separately — the amount you have already says which one you mean.

## What Changes With It

Constant volume is offered only for a quantity. A flowing stream has no volume of its own, only a rate, so holding it constant means nothing — and for the same reason a final volume can only be asked for on a quantity basis. Everything else is common to both: constant pressure, constant temperature, adiabatic with an isentropic efficiency, and isenthalpic throttling.

The normal-flow reference defaults to 20 °C and 1 atm and is editable on the [Units](Units-Tab) tab. Check it against your instrument: "normal" conditions are not standardised, and a 0 °C reference reads about 7 % higher in mass terms.

## Method

Given the initial state and the path, the final state is solved directly from the equation of state, and the energy follows from the first law, with the sign convention that positive means energy added to the fluid.

## Key Relations

```
n·(U₂ − U₁) = Q + W        quantity basis (closed system)
ṅ·(h₂ − h₁) = Q̇ + Ẇ        rate basis (open, steady flow)
```

n is the fixed amount; ṅ the flow rate. U is internal energy, h is enthalpy — the open-system form carries h rather than U because a flowing stream does flow work on its surroundings just by moving, and h = U + Pv already accounts for it. Isenthalpic (a throttle) is the special case h₂ = h₁: no work, no heat, and the temperature still changes — the Joule–Thomson effect. Combinations that contradict each other — isenthalpic against a specified final temperature, say — are greyed out rather than silently answered.

## Limitations

One substance or one mixture at a time, with its chemical identity fixed: nothing reacts here. For species turning into one another use [Chemical Equilibrium](Chemical-Equilibrium) or [Reaction](Reaction). Large excursions can push the fluid outside the equation of state's fitted range.
