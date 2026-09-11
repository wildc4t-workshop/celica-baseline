# AGENTS.md — Celica Baseline

## Mission

This repository is the engineering system of record for getting the current 2000 US-spec Toyota Celica GT-S into a mechanically sorted **get in and drive** condition before the major Street Build.

Baseline is intentionally narrow. Do not let interesting upgrades expand its completion criteria.

## Core operating rule

**Markdown is durable engineering memory. `tasks.csv` is engineering attention. `project.yaml` is machine-readable state. The dashboard is derived only.**

The repository should remain sufficient to understand what is being fixed, why, what hardware is already in hand, and what is actually blocking normal street use.

## Read before changing state

Read at minimum:

- `PROJECT.md`
- `tasks.csv`
- `project.yaml`
- relevant vehicle-wide reference material in `Celica-engineering-knowledge` when factory/year-specific information matters

Treat current repository state as authoritative unless the user explicitly corrects it.

## Collaboration rule

The user may report real-world updates in natural language from any chat, for example:

- `Baseline: the A/C line is installed.`
- `The Recaro rails showed up.`
- `I found a leak during the inspection.`

Do not require task IDs or filenames. Resolve the affected project state, update durable documentation/tasks when appropriate, and report what changed.

If the user says not to update GitHub yet, discuss only.

## Task and decision IDs

Use:

`BASE-###`

Decision IDs:

`DEC-BASE-###`

Canonical task schema:

```text
id,title,status,action,time_min,context,cost,priority,blocked_by,decision_needed,doc_link,requires_car_down,requires_parts,notes
```

Dashboard-supported statuses:

`backlog`, `ready`, `doing`, `blocked`, `verify`, `done`

Dashboard-supported actions:

`research`, `measure`, `buy`, `cad`, `mockup`, `bench-test`, `vehicle-test`, `code`, `fabricate`, `install`, `document`, `verify`

Dashboard-supported contexts:

`desk`, `phone`, `garage`, `car`, `bench`, `cad`, `computer`

Keep tasks limited to work that actually advances the current car toward normal use. Do not create generic maintenance replacement tasks without evidence.

## Baseline completion criteria

Baseline is complete when the current car has:

- maintenance caught up;
- functional A/C;
- functional hydraulic power steering;
- the seat upgrade installed;
- no known issue preventing normal get-in-and-drive street use.

Tires remain part of Street Build / upgrade progression, not a Baseline completion gate.

## Current critical-path discipline

The major A/C / hydraulic-PS reassembly is complete. Current work is validation / closeout.

Current execution logic is:

1. renew registration/tags before 2026-09-30;
2. schedule the state safety inspection and then complete it at the booked appointment;
3. road-verify A/C and hydraulic power-steering operation, belt tracking, leaks, and steering-wheel position;
4. capture the PowerFC shift/rev-hang log before changing decel/idle-control settings;
5. recheck manual-transmission fluid;
6. diagnose the known key-off parasitic draw with an ammeter/fuse-pull test;
7. replace brake fluid when helper availability allows;
8. finish the evidence-driven roadworthiness audit;
9. complete the Recaro seat path when hardware is available.

Do not invent an inspection deadline that is not recorded by the user. The currently documented end-of-month deadline applies to registration/tags.

Do **not** reopen the service corridor or hold Baseline open for a speculative charge-pipe redesign.

## A/C discipline

Known state includes a new OEM compressor, aftermarket condenser, refreshed/new lines where available, and one rare high-pressure line that must be protected carefully.

The rare line is installed, P-clipped for support, and protected with 5/8-in heater hose around the vulnerable section.

Treat the rare line as a packaging/serviceability constraint. When documenting work preserve routing, supports, abrasion/heat risks, clearances, and any changes that materially affect future service.

Do not assume a fabricated replacement is readily available merely because the rest of the system can be replaced.

## Hydraulic power-steering discipline

Baseline owns restoration and validation of the conventional hydraulic system.

The hydraulic system is installed. Remaining work is road validation of assist, leaks, belt tracking, pump behavior, and steering-wheel position.

The rack is the known-good architecture for Baseline; EPS belongs to Side Projects and must earn its way onto the car later.

Restoring hydraulic PS now does not conflict with future EPS R&D.

## Charge-pipe / packaging discipline

The A/C / PS / charge-pipe corridor has been 3D-scanned and the current piping is reinstalled.

The scan indicates limited practical recoverable space in the current architecture. Because the rare A/C line is now supported/protected and the car is back together, further charge-pipe optimization is low-priority refinement rather than Baseline work.

Preserve the scan as useful packaging evidence, but do not treat low-cost scan geometry as metrology truth for critical hardpoints without confirmation.

## PowerFC / diagnostic discipline

The current PowerFC is a known-running reference and should be preserved as evidence before EMU removal.

The 2026-09-11 A/C idle-hunt diagnosis and localized base-map correction are documented in `diagnostics/2026-09-11-powerfc-baseline.md`.

Do not change decel, fuel-cut, or idle-control behavior for the reported shift/rev-hang symptom until a road log captures VTA/TPS, RPM, ISC command, injector pulse/fuel-cut behavior, AFR, and vehicle speed where available.

Baseline owns the current drivability symptom diagnosis. Street Build owns the broader pre-EMU calibration/body-function archive.

## Seating discipline

Recaro-compatible infrastructure is selected. Rails/brackets have been ordered from Japan and suitable SR3 seats are being sourced.

Preserve exact rail/base-frame part numbers, side applicability, mounting hardware, seating height/position, slider/recline behavior, seatbelt-buckle/anchor integration, and actual installed clearance.

Prefer proven chassis-specific rails and manufacturer-supported hardware. Do not solve fitment with undocumented spacer stacks, improvised drilling, or altered restraint geometry.

A seat purchase is not completed fitment; installation and ergonomic/restraint verification remain separate.

Future upholstery, reskin, alternate Recaro choice, or migration of seats to another vehicle does not need to be resolved for Baseline.

## Maintenance discipline

Use one evidence-driven mechanical audit rather than inventing a long generic replacement list.

Typical audit domains include:

- fluids and intervals;
- leaks;
- belts/hoses;
- brakes;
- charging/battery;
- suspension/steering wear;
- lights/wipers/basic roadworthiness.

Only create new dashboard tasks for actual findings that require action.

## Evidence discipline

Distinguish measured/observed state from assumption. Useful labels include `MEASURED-CAR`, `INSTALLED`, `BENCH-TESTED`, `FACTORY-DOC`, `MANUFACTURER`, `CAD-DERIVED`, `INFERRED`, and `TENTATIVE`.

Ownership/purchase does not equal successful installation.

## Cross-project boundaries

- **Street Build** owns EMU, fuel-system validation, final drivetrain, turbo/intake/charge architecture, custom harness, DBW/flex, tires, final instrumentation, and the broader pre-EMU archive.
- **Side Projects** owns BBK and EPS.
- **CeliKey** owns passive entry/body-control/keyless-start R&D.

Do not duplicate those tasks in Baseline merely because work occurs on the same physical car.

## Definition of done

Before setting a task to `done`:

1. record the useful installation/measurement/test result;
2. update affected project state;
3. record any newly discovered issue as a task only if it is actionable;
4. reconcile dependent tasks;
5. preserve photos/scans/CAD/part information where it will matter later.

## End-of-session reconciliation

After meaningful garage work, update what was installed, what actually worked, what was discovered, what remains blocked, and what became ready. Keep the record concise enough that the next session starts with the car rather than reconstructing history.
