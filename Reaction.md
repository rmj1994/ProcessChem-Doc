---
title: Reaction
summary: >
  Enter the reactants and products of a reaction you already know; balances
  it, applies your excess and conversion, and reports the outlet amounts
  with the heat of reaction and the equilibrium constant.
---

## What This Models

A reaction you specify. You name the reactants and the products, and the coefficients follow from conserving every element — you never type them. You then anchor the calculation on one reference compound's amount, say how much excess the others carry, and the result is the full material balance together with the heat and the equilibrium constant.

This is the opposite of the [Chemical Equilibrium](Chemical-Equilibrium) mode. There you give a feed and the thermodynamics decides what forms. Here you have already decided what forms, and supply the conversion yourself. If you want to know whether your conversion is attainable rather than assume it, use Chemical Equilibrium.

## The Two Modes

'I have this feed' takes the amounts you enter and works out what comes out. 'I need this much product' works backwards: you name the production you want and it sizes the feed to deliver it at your conversion.

## Stoichiometric Or Not

The checkbox at the top decides how much the form asks of you. Left unticked — the usual case — the reaction is taken as exactly stoichiometric: every reactant is present in precisely the ratio the balanced equation calls for, nothing is in excess, and no inert is carried. The excess and amount fields have nothing to say under that assumption, so they are hidden rather than left to be filled in.

Tick it to describe a real feed instead: an excess of one reactant, a product already present, a compound in short supply, or a diluent passing through. The per-compound fields appear, and the two sections below describe them. Anything typed there applies only while the box is ticked — unticking it returns the calculation to pure stoichiometry rather than quietly keeping the last numbers entered.

## Excess And Actual Amounts

These apply when the box above is ticked. Every compound except the reference can be given either way. Excess is a percentage over what the stoichiometry requires, so 20 % excess air means 1.2 times the oxygen the reaction needs, and 0 % means exactly enough. The excess is not consumed, so it appears in the outlet — that is what makes it visible in the masses.

An actual amount is taken as entered instead. That means a compound can be put in short supply, in which case it becomes the limiting reactant and the reference is no longer fully converted. The result says which compound limited it and gives the conversion of each reactant separately, because with anything in excess they do not all convert to the same degree.

## Inerts

Also only when the box above is ticked, an inert being by definition material beyond the stoichiometry. Anything that is present but does not react — the nitrogen in combustion air, a steam diluent — belongs in the inerts list, not among the reactants. It passes through untouched and takes no part in the balance, but it still counts toward the totals and the gas volume, which is what it is there for.

## Phase Matters

Each compound carries the phase you choose, and it changes the answer. Burning methane to liquid water releases about 88 kJ per mole more than burning it to steam: that is the difference between a fuel's higher and lower heating value, and it is entirely down to which phase you pick.

## Method

Each compound's enthalpy and entropy at temperature come from its standard enthalpy of formation, its absolute entropy and its heat capacity, exactly as in the Chemical Equilibrium mode. The reaction's own properties are the sums of those, weighted by the balanced coefficients νᵢ.

## Key Relations

```
ΔH_rxn = Σ νᵢ·hᵢ            heat of reaction, products minus feed
ΔG°_rxn = Σ νᵢ·gᵢ           at standard-state activities
ln K = −ΔG°_rxn / (RT)      equilibrium constant
```

νᵢ is positive for a product, negative for a reactant, and the reported heat duty is this same sum applied to the whole outlet and feed: enthalpy of the outlet less enthalpy of the feed. With no initial temperature given the feed is taken to be already at the reaction temperature, so the duty is the heat of reaction alone; give one and it includes the sensible heat as well.

## About The Equilibrium Constant

K depends on temperature alone. Pressure shifts where a real equilibrium settles, but it does not change K, and the value shown will not move when you change the pressure. Pressure does set the gas volumes.

## What It Refuses

A set of compounds that cannot be balanced, or that can be balanced in more than one way — carbon and oxygen giving both CO and CO2 is the everyday case, and there is no single right answer to report. Ions are refused too: the balance conserves elements but not charge.

## Limitations

One reaction at a time, with no kinetics and no reactor sizing. Gas volumes use the ideal molar volume RT/P, which is consistent with how the activities are modelled but approximate above about 10 bar. Heat capacity correlations extrapolate silently, so a compound entered in a phase it does not hold at your temperature is flagged rather than corrected.
