---
title: Chemical Equilibrium
summary: >
  Enter any set of components and amounts; finds which compounds are most
  stable at a chosen temperature and pressure, with the composition, phases
  and heat duty.
---

## What This Models

Chemical reaction equilibrium. You give a feed — any components, in mass or moles — and the calculation finds the combination of compounds with the lowest total Gibbs energy at your final temperature and pressure, conserving every element.

This is a different question from the other two Thermo modes. They hold the chemical identity fixed and move temperature, pressure and energy around. Here the species turn into one another and the answer is a composition.

## How To Use It

Choose how many components you have, name each one and give its amount. Tick 'Specify total amount' if you would rather enter a composition than absolute quantities: with it ticked your amounts are treated as proportions and scaled to the total, so 1 and 3 against a total of 100 kg mean 25 kg and 75 kg.

Then open 'Participating species'. The app lists every compound your feed's elements could form and which it has thermodynamic data for. Tick the ones you want to allow. Small molecules are shown first and selected by default, because those are the species that actually appear at equilibrium — a large hydrocarbon is never an equilibrium product of combustion. Use 'Show all' and the search box to reach anything else.

## Method

Each species' own Gibbs energy at temperature is built from its standard enthalpy of formation, its absolute entropy and its heat capacity, and the feed settles into whatever combination of species makes the total lowest, one balance per element.

## Key Relations

```
Gᵢ(T) = Hf,298 + ∫Cp dT − T·(S°₂₉₈ + ∫(Cp/T) dT)     per species
minimise  Σ nᵢ·μᵢ   subject to one balance per element
μᵢ = Gᵢ + RT·ln(yᵢP)     gas — depends on how much is present
μᵢ = Gᵢ                  solid/liquid — pure phase, unit activity
```

Hf,298 and S°₂₉₈ are the formation enthalpy and absolute entropy at 298.15 K; the two integrals carry each up to your temperature. μᵢ is the chemical potential the minimisation actually balances element-by-element, numerically, not by hand. A condensed phase's μᵢ does not depend on how much of it is present, which is why a solid either survives or disappears entirely rather than settling at some intermediate amount — only a gas's does, through the yᵢP mixing term.

The heat duty is the full energy balance: enthalpy of the products at the final temperature, less enthalpy of the feed at its own temperature. It therefore includes both the heat of reaction and the sensible heat.

## About The Initial Pressure

It does not affect this result, and the field is not pretending otherwise. Feed enthalpy is pressure-independent for an ideal gas and for a condensed phase, so an isothermal-isobaric equilibrium depends only on the final pressure. It is still recorded, for completeness alongside the other conditions on the sheet.

## The Limitation That Matters Most

Only the species you tick can form. Gibbs minimisation finds the best combination of what it is given, so an unticked compound simply cannot appear, and its absence from the answer means nothing at all. If you expect a product and do not see it, check it was selected before concluding it is not favoured.

## Metastable Products Will Not Appear

Equilibrium is the state reached once every reaction has run to completion, so anything that survives in practice only because it decomposes slowly is absent from the answer — correctly, and unhelpfully if it is the thing being designed for.

Sodium hypochlorite is the clearest case. A chlorine scrubber is built to make it, but OCl⁻ → Cl⁻ + ½O₂ releases about 94 kJ/mol, so at equilibrium bleach has all decomposed: feed Cl₂ and NaOH here and the answer is NaCl and oxygen. The chlorine removal it reports is real — the chlorine is indeed gone — but it says nothing about the hypochlorite yield, which is the number a scrubber is rated on. Peroxides and most partial-oxidation intermediates behave the same way.

For those, use the [Reaction](Reaction) mode instead: it takes the stoichiometry and the conversion from you rather than deriving them, which is exactly what a kinetically controlled product needs.

## Dissolved Species Are Modelled As Pure Phases

Every condensed species is treated as a pure phase at unit activity. In a solution it is not: caustic soda in water is dissolved ions, and its activity is far from one — a 17 % NaOH solution is about 5 molal. Results for aqueous systems are therefore qualitative. They will get the direction and the stoichiometry right and the amounts only approximately.

## Other Limitations

Ionic species are excluded: the solver balances elements but not charge, so admitting an ion would let it create charge from nothing. There are no solution phases — no molten slag, no solid solutions — so a system that really forms a melt is modelled only approximately; this handles calcination well and clinkering roughly. There is no kinetics. And heat capacity correlations extrapolate silently, so compositions much above 1700 °C should be treated as indicative.
