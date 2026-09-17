---
title: Heat Exchanger
summary: >
  Two streams exchange heat: one cools, the other warms by the same amount.
  Give the duty, or one outlet temperature, and it finds the rest — and
  refuses a pairing that would need heat to flow backwards.
---

## What This Models

A hot stream and a cold stream flowing past each other and exchanging heat — a shell-and-tube unit, a plate exchanger, any device where the two never mix. Whatever heat the hot stream gives up, the cold stream takes on: no loss to the surroundings is modelled, so the duty on one side always equals the duty on the other.

## Key Relations

```
Q = ṅ_hot·(h_hot,in − h_hot,out)     heat the hot stream gives up
Q = ṅ_cold·(h_cold,out − h_cold,in)  heat the cold stream picks up
```

The same Q both ways, by construction — no separate closure to check. Each Δh comes from the same relation the [Heater](Heater) case uses on its one stream, Δh = ∫Cp dT + Σ L_tr (sensible heat plus any latent heat crossed), run once per stream. Whichever you give — the duty, or one stream's own outlet — the other three unknowns follow from these two equations together.

## Counter-Current

The two streams are assumed to flow in opposite directions through the unit, the usual arrangement and the more efficient one. That choice only matters for the feasibility check below — the energy balance itself is the same either way.

## Inputs

Each stream: a substance, a flow rate, an inlet temperature and a pressure — the same choices the Heater case offers for a single stream, given here twice. Then either a duty (both outlet temperatures are found), or one stream's own outlet temperature (the duty and the other stream's outlet are found from it).

## When It Refuses

Heat only flows from hot to cold.

```
T_hot,out ≥ T_cold,in
T_cold,out ≤ T_hot,in
```

In a counter-current unit those are the two ends where the streams pair up — asking for a pairing that breaks either one is refused rather than answered with a duty that would require heat to run backwards.

That check only looks at the four inlet/outlet temperatures, not the shape of the temperature profile in between. If a stream changes phase partway through, the closest approach between the two streams can actually occur at that phase change rather than at either end — sizing an exchanger for that case needs the fuller method below, not this check alone.

## What This Does Not Do Yet

This is the energy balance only: how much heat moves, and what temperature each stream leaves at. It does not size the exchanger — no heat-transfer area, no tube count, no pressure drop, no fan or pump power, and no cost. Sizing needs the temperature profile along the unit and a heat-transfer coefficient, both a separate calculation from the one here.
