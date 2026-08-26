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

Current execution logic is:

1. finish A/C restoration using the rare reusable high-pressure line;
2. restore hydraulic power steering while charge piping is out of the way;
3. correct rack/column indexing;
4. capture a 3D scan of the A/C / PS / charge-pipe packaging region while access is good;
5. add practical protection/support for the rare A/C line;
6. reinstall the existing intercooler piping and return the car to running configuration;
7. verify A/C and hydraulic steering operation;
8. perform a mechanical roadworthiness audit and create follow-up tasks only from actual findings.

Do **not** keep the car apart waiting for a perfect charge-pipe redesign.

## A/C discipline

Known state includes a new OEM compressor, aftermarket condenser, refreshed/new lines where available, and one rare high-pressure line that must be reused and protected.

Treat the rare line as a packaging/serviceability constraint. When documenting work preserve routing, supports, abrasion/heat risks, clearances, and any changes that materially affect future service.

Do not assume a fabricated replacement is readily available merely because the rest of the system can be replaced.

## Hydraulic power-steering discipline

Baseline owns restoration of the conventional hydraulic system.

The rack is currently the known-good architecture for Baseline; EPS belongs to Side Projects and must earn its way onto the car later.

When restoring PS, document line routing, leaks, belt tracking, pump behavior, steering-wheel indexing, and any remaining mechanical issue.

Restoring hydraulic PS now does not conflict with future EPS R&D.

## Charge-pipe / packaging discipline

The current charge piping conflicts with access and creates concern around the rare A/C line.

For Baseline:

- remove/move piping as required to complete A/C and PS work;
- scan and document the area while open;
- protect the rare A/C line;
- reinstall the existing piping and return the car to service.

Follow-on improved piping may use ovalized geometry, AM transitions, composites, or other fabrication methods, but the design should favor simple manufacture, serviceability, line protection, and minimal unnecessary welding.

Preserve scan/CAD source, keep-out zones, engine movement allowance, line/hose clearance, supports, fastener/tool access, and assembly/removal path.

A low-cost 3D scan is useful packaging input, not metrology truth for critical hardpoints without confirmation.

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

- **Street Build** owns EMU, fuel-system validation, final drivetrain, turbo/intake/charge architecture, custom harness, DBW/flex, tires, and final instrumentation.
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
