# Automatic Supply Changeover (NEPA / Inverter)

A relay-based automatic changeover that powers a house load from the grid (NEPA) when it is available and switches to an inverter when the grid fails.

**Tool:** CADe_SIMU | **Status:** Simulated | **Supply:** single-phase (live and neutral switched)

## Overview

In many homes the grid supply is unreliable and a backup inverter is common. This circuit makes the switch automatic. One relay, whose coil is connected to the grid supply, decides which source feeds the house. When the grid is present the relay is energised. When it fails, the relay drops out and the load moves to the inverter. Both **phase and neutral** are switched, and the two sources are never connected to each other.

## Circuit diagram

![Automatic supply changeover circuit diagram](images/circuit-diagram.png)

## Components

| Label | Component | Function |
|---|---|---|
| NEPA (A) | Grid supply, live (L) and neutral (N) | Main source |
| CBN | 2-pole circuit breaker | Protects and isolates the NEPA input |
| INVERTER (B) | Inverter supply, live (L) and neutral (N) | Backup source |
| CBQ | 2-pole circuit breaker | Protects and isolates the inverter input |
| K (coil A1-A2) | Relay coil connected across the NEPA live and neutral | Senses whether the grid is present |
| Relay for phase | Changeover contact of K | Switches the house live between NEPA and the inverter |
| Relay for neutral | Changeover contact of K | Switches the house neutral between NEPA and the inverter |
| HOUSE | Lamp (X1-X2) | Represents the household load |

## How it works

Each changeover contact has a common terminal (to the house), a normally closed (NC) terminal wired to the **inverter** and a normally open (NO) terminal wired to **NEPA**.

| Condition | Relay K | Phase and neutral contacts | House powered by |
|---|---|---|---|
| NEPA present | Energised | Moved to the NO side | NEPA |
| NEPA fails | De-energised | Return to the NC side | Inverter |
| NEPA restored | Energised again | Move to the NO side | NEPA |

1. The coil K is wired directly across the NEPA supply, so it is energised whenever the grid is on.
2. When it energises, both contacts move to the NEPA side and the house lamp is lit from the grid.
3. If NEPA drops, the coil loses power. The spring returns both contacts to the NC side, and the load is fed by the inverter.
4. When NEPA returns, the coil energises and the load moves back to the grid.

## Safety notes

- A changeover contact connects to **one source at a time**, so the grid and inverter cannot be paralleled through the contacts. This prevents the inverter from feeding back into the grid.
- Switching both live and neutral keeps the two sources isolated from each other.
- The contact and breaker ratings must be higher than the load current in a real installation.

## Running the simulation

1. Open the project file in [CADe_SIMU](https://www.cadesimu.net/).
2. Click **Run**.
3. Switch the CBN breaker off to simulate a grid failure and watch the HOUSE lamp stay on from the inverter. Switch it on again to see the transfer back.

## Possible improvements

- Add an on-delay so the load only returns to the grid after the supply has been stable for a few seconds.
- Use a voltage monitoring relay instead of only detecting present or absent.
- Use a contactor rated for the full load, with a mechanical interlock.
- Add surge protection on both inputs.

## Skills demonstrated

Relay changeover logic, switching live and neutral, source isolation, fail-safe design (inverter takes over when the relay de-energises).

## Files

```
02-automatic-supply-changeover/
├── README.md
├── automatic-supply-switch.cad   (add your CADe_SIMU project file here)
└── images/circuit-diagram.png
```

## Author

Nifemi Akintoye ([GitHub](https://github.com/attommm))

> This is a learning simulation. Real mains and inverter wiring must be done by a qualified electrician in line with local wiring regulations.
