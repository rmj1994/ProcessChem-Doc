---
title: Fluidized Bed
summary: >
  Sizes a fluidized bed: the velocity at which it lifts, the velocity at
  which it blows out, where the gas you have sits between them, and the
  pressure drop that follows.
---

## What This Models

A gas passed upward through a bed of particles. Below a certain velocity the bed sits on the distributor and the gas merely percolates through it. At that velocity the drag on the particles equals their weight, the bed lifts, and it begins to behave like a liquid — this is the minimum fluidization velocity. Well above it, individual particles are carried out of the vessel altogether. Those two velocities bound every fluidized bed, and this case computes both and says where your gas rate falls.

## Inputs

The solid — one species or several, each with its own particle size, sphericity, density and voidage, and its own share of the bed or its own feed rate. A blend of different particles genuinely segregates: each keeps its own fluidization velocity rather than sharing one, and the bed can be fluidized in one species while another still sits on the distributor. True density is looked up for each; the shape and porosity given turn that into the one the gas actually has to lift — a particle with 40 % internal porosity fluidizes as though it were 40 % lighter.

The fluidizing gas at the bed's own temperature and pressure — one species or several, each fed its own flow on its own basis (volumetric, mass, molar or normal volumetric), the way a real feed is actually specified: so many Nm³/h of air, so many kg/h of steam, rather than a composition entered as percentages plus one shared total that could disagree with each other. Then the vessel cross-section, cylindrical or rectangular, the bed height, and either the bed voidage or the bulk density.

## The Gas State Is Where Beds Go Wrong

Both velocities depend on the gas density and viscosity, and both change sharply with temperature. Air at 850 °C is about a quarter the density and two and a half times the viscosity of air at ambient. A calciner therefore fluidizes at a lower superficial velocity than the same solid in cold air — so properties taken at ambient by mistake move the answer in the wrong direction, not merely by a little. The temperature and pressure entered here are the ones used.

The same applies to the flow. A normal cubic metre at 850 °C occupies nearly four times its volume, so a normal flow read as an actual one understates the velocity fourfold and can make an entraining bed look barely fluidized. Choosing the right basis is what prevents that, and 'normal' means whatever reference you set on the [Units](Units-Tab) tab.

## Two Answers For The Minimum Fluidization Velocity

Both routes turn on the same dimensionless group, the Archimedes number — the ratio of gravity's pull on the particle (net of buoyancy) to viscous drag:

```
Ar = g·ρ_g·(ρ_p − ρ_g)·d_p³ / μ_g²

Ergun (Kunii & Levenspiel):
    Re_mf = (−b + √(b² + 4a·Ar)) / (2a)
    a = 1.75 / (φ·ε_mf³),   b = 150(1 − ε_mf) / (ε_mf³·φ²)
Wen & Yu:
    Re_mf = √(33.7² + 0.0408·Ar) − 33.7
both give   u_mf = Re_mf·μ_g / (ρ_g·d_p)
```

ρ_p and ρ_g are the particle and gas densities, d_p the particle size, μ_g the gas viscosity, φ the sphericity, ε_mf the voidage at minimum fluidization. The Ergun form is exact given φ and ε_mf — but those are rarely measured, and guessing them is worse than a correlation fitted without them. Wen & Yu folds both into its two fitted constants (33.7 and 0.0408) instead. For 200 µm sand in ambient air the two give 0.046 and 0.035 m/s, a 35 % spread. Both are shown rather than averaged, because that spread is a real statement about how well the velocity is known for your powder. Where φ and ε_mf are estimates, Wen & Yu is the safer of the two.

## The Terminal Velocity

Where a lifted particle stops accelerating and is simply carried along — Haider & Levenspiel (1989), through the same Ar-like grouping in a dimensionless size d*:

```
d* = d_p·[ρ_g·g·(ρ_p − ρ_g) / μ_g²]^(1/3)
u_t* = [18/d*² + (2.335 − 1.744φ)/√d*]⁻¹
u_t = u_t*·[μ_g·g·(ρ_p − ρ_g) / ρ_g²]^(1/3)
```

Fitted for sphericity between 0.5 and 1 — flagged when a particle's φ falls outside it, per species.

## Pressure Drop, And Why It Stops Changing

Below minimum fluidization the bed rests on the distributor and the drop is Ergun's own packed-bed form, rising with the gas rate:

```
ΔP/H = 150·μ_g·u·(1 − ε)² / (φ²·d_p²·ε³)     viscous term
     + 1.75·ρ_g·u²·(1 − ε) / (φ·d_p·ε³)       inertial term
```

At and above u_mf the gas carries the bed, and the drop is simply its weight per unit area:

```
ΔP = (ρ_p − ρ_g)·(1 − ε)·g·H          fluidized, independent of u
```

H is the bed height, ε its voidage, u the superficial velocity — the two forms meet exactly at u_mf, which is what defines u_mf in the first place. Above it, ΔP does not rise any further however fast the gas goes: expanding the bed raises its height exactly as much as it raises its voidage, so the solids inventory (1 − ε)·H is unchanged and so is the drop. This is why a measured pressure drop is such a useful diagnostic: one that falls as the gas rate rises means the bed is channelling or has lost inventory.

## Each Species Gets Its Own Velocity

With more than one solid, every one of the figures above — u_mf, both routes, u_t, regime, Geldart group, minimum bubbling velocity, elutriation, and the effect of a reaction — is reported once per species, in its own card, rather than averaged into one number. A settled-looking blend can still be a fine species already entraining over a coarse one that has not even lifted yet, and a single shared velocity would hide exactly that. When the species disagree on regime at the same gas rate, the result says so by name — that is the bed segregating, not a rounding difference. The terminal velocity is for each species' own mean particle size, so it bounds when that species is carried out, not when its dust is: elutriation is governed by the small end of its size distribution, and the fines-size figure reported alongside the mean-size one is the one that governs.

## What Stays One Number For The Whole Bed

Pressure drop, the solids inventory, bulk density and the distributor are properties of the one physical vessel, not of any single species, so they stay aggregate: a mass-weighted blend of each species' own envelope density (volume is additive, not mass, so this is a harmonic mean, not a simple average) and a similarly blended particle size stand in for 'the bed' in these calculations, the same way a Sauter mean diameter would. The Bed card reports this blended density; the Result card, the one pressure drop that follows from it. The Operating window is the range that fluidizes every species without entraining any of them — the highest u_mf and the lowest u_t across the blend, not a weighted average of either — and is flagged empty when no single gas rate can do that at once.

Minimum bubbling velocity is Abrahamsen & Geldart's ratio to u_mf, and is the Geldart A/B classification — a ratio above 1 expands before it bubbles (Group A), at or below 1 it bubbles as soon as it fluidizes (Group B):

```
u_mb / u_mf = 2300·ρ_g^0.126·μ_g^0.523·exp(0.716F)
              / (d_p^0.8·g^0.934·(ρ_p − ρ_g)^0.934)
```

F is the mass fraction of fines below 45 µm. Above u_mb, Darton's correlation gives the bubble diameter at height h above the distributor, and it grows again in a crowd:

```
d_b = 0.54·(u₀ − u_mf)^0.4·(h + 4√A₀)^0.8 / g^0.2
u_br = (u₀ − u_mf) + 0.711·√(g·d_b)
```

A₀ is the distributor area per orifice — a coarser plate makes bigger bubbles everywhere above it, which is why the Bubbling and Distributor cards cannot be sized apart from each other. The Bubbling card reports d_b at the bed surface, u_br, and how far the bed expands — flagging it when d_b grows enough to span the vessel and the bed slugs instead — using that same blended particle population, since a bubble rising through a mixed bed is a bed-scale phenomenon, not a per-species one. The Distributor card takes the orifice diameter and count you specify — what a real plate is actually made from — and reports the velocity and pressure drop that follow, alongside the drop a plate should take to distribute gas evenly (a fraction of the bed's own drop). When the plate you specified falls short of that, it's flagged: the gas will find the easiest path through the bed rather than spread across it.

## Reaction, The Freeboard And What Leaves

A calciner is the case this exists for, and it is the shipped default: CaCO₃ → CaO + CO₂ at 90 % conversion, fluidized by CO₂ itself rather than an inert diluent — the recycled product gas a real electrified calciner runs on. Turning the reaction on opens an editor where you name any number of reactant, product and inert species across any phase, seeded from every solid and gas row already entered. One reactant is picked as the reference; when the balanced equation is ambiguous, a split ratio resolves it, the same way the [Reaction](Reaction) mode does.

Works in either mode, against a different anchor each way. A continuous flow reacts against its actual fed rate, and CaCO₃ → CaO + CO₂ puts a mole of gas into the freeboard for every mole converted, so the gas leaving is more than the gas that came in — a bed that fluidizes properly at the distributor can be entraining at the top. Each species' own card shows its u_mf and u_t recomputed on that outlet gas, flagged whenever the regime changes. A batch reacts against the solid amount currently charged into the bed, at the conversion given — its Reaction card reports totals (kg, not kg/h): the bed as charged, the bed after reaction (product formed plus whatever reactant did not convert), and the gas produced, assumed to have left via the fluidizing stream by the end of the batch. The fluidizing gas's own u_mf/u_t/elutriation figures stay at their pre-reaction values in batch mode, since there is no feed rate for the reaction's gas to blend into. In both modes, any fed species left out of the reaction's own rows — a carrier gas, an inert solid — passes straight through unreacted; a species that is both fed and one of the reaction's own rows (the default's own recycled CO₂, for instance) has its fed amount folded into the reaction's own balance rather than counted twice.

The freeboard's cross-section is the bed's own unless an expanded top is given, in which case the extra area drops the velocity so entrained solids can disengage and fall back rather than leaving. This module does not compute a specific transport disengaging height, since that is read off a chart rather than a closed form; every elutriation rate given is the floor of what leaves, and the true rate is higher below it.

Bed height is entered directly in both modes. In flow mode, the residence time it implies shows up in the results rather than being entered. The Solids balance card shows the feed, the total solid leaving the bed (accounting for anything converted to gas), and gas lost to reaction. Estimated elutriation appears separately in the Result section, as guidance on how much of that total is likely carried out overhead versus drawn from the bottom — flagged if the estimate would exceed the total that actually leaves.

## Limits

One mean particle size per species — a wide size distribution within one species still fluidizes progressively rather than at a single velocity, and no single diameter can express that. The terminal-velocity correlation's own sphericity range is checked per species, per [The Terminal Velocity](#the-terminal-velocity) above.

The reaction editor resolves one balanced equation (with a split ratio when it is ambiguous), not independent reactions running side by side. A batch reaction's reference must be a solid — the fluidizing gas has no batch total, only a flow — and a batch does not recompute a post-reaction bed height even though the reaction changes the solid's mass; before/after composition is reported, not a new geometry. Air and other pseudo-pure blends (refrigerants) can't be fed as the fluidizing gas at all, even alone — enter their real constituents instead (nitrogen and oxygen for air), since they have no CAS of their own and so can never be one component of the mixture a reaction's outlet gas may need to become. No heat transfer and no attrition — this case sizes the bed, bounds its operating window, and says what leaves it.
