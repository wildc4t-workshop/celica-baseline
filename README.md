# Celica Baseline

Execution plan for getting the current **2000 Toyota Celica GT-S** into a mechanically sorted, dependable **get in and drive** condition before the major Street Build.

Baseline is intentionally narrow. It is complete when the current car has:

- maintenance caught up;
- functional A/C;
- functional hydraulic power steering;
- the seat upgrade installed.

The objective is not to redesign the car during Baseline. Opportunities for measurement, CAD, or future refinement may be captured, but they do not get to hold the car apart.

## Current State

The major A/C / hydraulic-PS reassembly is complete enough that the project has moved from **build** into **validation**.

Completed in the current service cycle:

- rare A/C high-pressure line installed and protected;
- hydraulic power steering restored;
- standard accessory-drive configuration restored;
- steering wheel mechanically recentered;
- existing intercooler piping reinstalled;
- turbo coolant lines rebuilt;
- turbo oil drain rebuilt;
- engine oil changed;
- PowerFC A/C idle-hunt diagnosis and localized base-map correction completed.

The A/C idle correction and supporting logs are documented in [`diagnostics/2026-09-11-powerfc-baseline.md`](diagnostics/2026-09-11-powerfc-baseline.md).

## Current Critical Path

1. Road-verify A/C cooling/leak-free operation, hydraulic steering assist, belt tracking, leaks, and steering-wheel position.
2. Capture a PowerFC driving log of the reported shift/rev-hang behavior before changing decel or idle-control settings.
3. Recheck manual-transmission fluid level/condition.
4. Measure key-off parasitic draw with an ammeter and isolate the responsible circuit by pulling fuses methodically.
5. Replace brake fluid when a second set of hands is available.
6. Finish the evidence-driven mechanical roadworthiness audit.

## Parallel Seat Path

- Recaro-compatible seat rails have been ordered from Japan and are in transit.
- Suitable Recaro SR3 seats are being sourced.
- Final installation waits on both rails and seats.

## Follow-on Refinement

The current charge piping can be redesigned after Baseline. A 3D scan of the A/C / power-steering / charge-pipe region is now opportunistic rather than a blocker. Future work may investigate ovalized sections, additive-manufactured transitions, or composite approaches, but the permanent solution should favor serviceability and avoid unnecessary fabrication complexity.

## Source of Truth

- [`PROJECT.md`](PROJECT.md) — durable current vehicle state, hardware, constraints, and execution logic.
- [`tasks.csv`](tasks.csv) — canonical executable work queue and task status.
- [`project.yaml`](project.yaml) — machine-readable project state for the dashboard.
- [`AGENTS.md`](AGENTS.md) — collaboration and repository-maintenance rules.

Related repositories:

- [`celica-street-build`](https://github.com/wildc4t-workshop/celica-street-build) — final major drivetrain/controls build.
- [`Celica-engineering-knowledge`](https://github.com/wildc4t-workshop/Celica-engineering-knowledge) — research/reference archive.
- [`celica-project-dashboard`](https://github.com/wildc4t-workshop/celica-project-dashboard) — public task dashboard.
