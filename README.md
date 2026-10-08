# Celica Baseline

Execution plan for getting the current **2000 Toyota Celica GT-S** into a mechanically sorted, dependable **get in and drive** condition before the major Street Build.

Baseline is intentionally narrow. It is complete when the current car has:

- maintenance caught up;
- functional A/C;
- functional hydraulic power steering;
- the seat upgrade installed;
- no known issue preventing normal street use.

The objective is not to redesign the car during Baseline. Opportunities for measurement, CAD, or future refinement may be captured, but they do not get to hold the car apart.

## Current State

The major A/C / hydraulic-PS reassembly is complete and the project is in **validation / closeout**.

Completed in the current service cycle:

- rare A/C high-pressure line installed, P-clipped, and protected with 5/8-in heater hose around the vulnerable section;
- hydraulic power steering restored;
- standard accessory-drive configuration restored;
- steering wheel mechanically recentered;
- A/C / PS / charge-pipe corridor 3D scan captured;
- existing intercooler piping reinstalled;
- turbo coolant lines rebuilt;
- turbo oil drain rebuilt;
- engine oil changed;
- PowerFC A/C idle-hunt diagnosis and localized base-map correction completed.

The scan review suggests there is limited useful space to recover in the current service corridor without a larger redesign, so further charge-pipe optimization is intentionally deprioritized in favor of advancing the Street Build.

The PowerFC idle correction and supporting logs are documented in [`diagnostics/2026-09-11-powerfc-baseline.md`](diagnostics/2026-09-11-powerfc-baseline.md).

## Current Critical Path

1. Confirm registration/tag renewal status; the recorded 2026-09-30 deadline has passed and completion is not recorded.
2. Schedule the state safety inspection, then complete it at the booked appointment.
3. Road-verify A/C cooling/leak-free operation, hydraulic steering assist, belt tracking, leaks, and steering-wheel position.
4. Capture a PowerFC driving log of the reported shift/rev-hang behavior before changing decel or idle-control settings.
5. Recheck manual-transmission fluid level/condition.
6. Measure key-off parasitic draw with an ammeter and isolate the responsible circuit by pulling fuses methodically.
7. Replace brake fluid when a second set of hands is available.
8. Finish the evidence-driven mechanical roadworthiness audit.

No state-inspection expiration date is currently recorded in the repository; the recorded 2026-09-30 deadline applies to the registration/tags.

## Parallel Seat Path

- Recaro SR2 seats and Recaro rails are **in hand**, user-confirmed 2026-10-08.
- Receipt/sourcing tasks are complete; the earlier SR3 search is superseded.
- Installation and driving-position/restraint verification are ready to proceed; no installed-fit claim is made.

## Follow-on Refinement

The A/C / power-steering / charge-pipe region has now been scanned. Review of the corridor indicates that the current architecture offers limited practical recoverable space, and the rare A/C line is already physically supported and protected. Improved charge-pipe CAD/fabrication remains a low-priority future refinement rather than active Baseline work.

## Source of Truth

- [`PROJECT.md`](PROJECT.md) — durable current vehicle state, hardware, constraints, and execution logic.
- [`tasks.csv`](tasks.csv) — canonical executable work queue and task status.
- [`project.yaml`](project.yaml) — machine-readable project state for the dashboard.
- [`AGENTS.md`](AGENTS.md) — collaboration and repository-maintenance rules.

Related repositories:

- [`celica-street-build`](https://github.com/wildc4t-workshop/celica-street-build) — final major drivetrain/controls build.
- [`Celica-engineering-knowledge`](https://github.com/wildc4t-workshop/Celica-engineering-knowledge) — research/reference archive.
- [`celica-project-dashboard`](https://github.com/wildc4t-workshop/celica-project-dashboard) — public task dashboard.

