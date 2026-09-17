---
title: Electrochemical Reaction
summary: >
  A reaction driven by electricity, or driving it. Balances the equation as
  the Reaction mode does, then reports the cell voltage, the electrical
  energy, the heat, and the current for a monopolar or bipolar stack.
---

## What This Models

The thermodynamics of an electrochemical cell: what voltage a reaction needs to be driven at, or produces when it drives, and what heat goes with it. Enter the reaction exactly as in the [Reaction](Reaction) mode, add how many electrons it transfers and how the cells are wired.

It works in both directions and tells them apart itself. A reaction with a positive Gibbs energy has to be driven — an electrolyser. One with a negative Gibbs energy drives — a battery or fuel cell. The equations are the same; only the wording changes.

## The Electrons Are Counted For You

Leave the electrons field blank and they are worked out from the oxidation states of the balanced equation, then reported as a result. Water balances as 2H₂O → 2H₂ + O₂: four hydrogens go from +1 to 0, gaining one electron each, while two oxygens go from −2 to 0, losing two each — four gained, four lost, so four transferred.

This matters because the number belongs to the equation as balanced, not to the half-reaction you remember. 2H⁺ + 2e⁻ → H₂ is two electrons per molecule of hydrogen, and this equation makes two of them. Entering two would give 2.46 V instead of 1.23 V — and 2.46 V looks perfectly ordinary, between chlor-alkali's 2.19 and magnesium's 2.48, so nothing downstream could have caught it.

Fill the field in only to override the count. It is then labelled as yours on the result, so a derived figure and an asserted one never look alike.

It declines rather than guessing in two cases. A reaction that moves no electrons at all — calcination, say — has none to count. And where the rules contradict themselves, as in a peroxide, where hydrogen at +1 and oxygen at −2 leave a molecule that does not add up to zero, it says so instead of returning a confident wrong number.

## Method

Two relations carry everything, plus Faraday's law for the current.

## Key Relations

```
E_rev = −ΔG/(zF)     reversible voltage — what thermodynamics demands
E_tn = −ΔH/(zF)      thermoneutral — cell neither heats nor cools
z·F·(E_tn − E_rev) = TΔS   heat exchanged, per mole reacted
I = ṅ_rxn·z·F         Faraday's law — a rate of reaction is a current
```

z is the electron count, F Faraday's constant, ṅ_rxn the molar rate of reaction. The heat TΔS is absorbed by an electrolyser, released by a fuel cell. Give the amount as a flow to get ṅ_rxn and so a current; a batch has no rate in it and so has no current.

## Monopolar And Bipolar

The wiring decides how one duty is split between current and voltage, and it is the part most often got wrong.

```
bipolar (series):     V_stack = N·E,   I_stack = I        high V, low I
monopolar (parallel): V_stack = E,     I_stack = N·I       low V, high I
P = V_stack·I_stack    identical either way
```

N is the number of cells, E and I one cell's own voltage and current. Bipolar cells sit in series: one current threads all of them and the voltages add, giving a high-voltage, low-current stack. Monopolar cells sit in parallel: each sees the same voltage and the currents add, giving the opposite. The power is identical either way — the choice is about busbars, rectifiers and sealing, not about energy.

## A Worked Comparison

Aluminium smelting is the clearest example of what this mode is for. With a consumable carbon anode the reversible voltage at 960 °C is about 1.18 V; with an inert anode releasing oxygen instead it is about 2.20 V. The carbon is oxidised and contributes chemical energy, which is real and worth about a volt.

That is not the whole picture, and the mode deliberately does not pretend it is: an inert anode produces no process CO₂ and needs no replacing, which is why it is pursued despite the extra volt. What holds it back is materials that survive molten cryolite, not this number. Use the comparison to size the energy penalty, not to settle the question.

## What This Does Not Do

No kinetics. There is no overpotential model, no exchange current density, no Tafel slope — those depend on electrode material, surface and age, and are in no database anywhere. The voltages here are reversible ones, and a real cell always needs more. Everything between the two is yours to supply.

It also assumes unit activity throughout: pure phases and ideal gases at the stated pressure, with no correction for concentration. For a concentrated brine or a molten-salt bath the real voltage differs by tens of millivolts, which matters for a precise energy balance and not for sizing a rectifier.
