# Celica Baseline — Project State

## Objective

Make the current 2000 Celica GT-S a sorted street car that can be driven and enjoyed without waiting for the future drivetrain build.

Baseline completion means:

- maintenance caught up;
- A/C functional;
- hydraulic power steering functional;
- seat upgrade installed.

Modernization work outside those requirements may happen opportunistically, but it is not allowed to redefine Baseline completion.

## Current Vehicle State

### A/C

The A/C system has been substantially refreshed and the engine is back in running configuration.

Known current hardware/state:

- Brand-new OEM compressor is installed.
- Aftermarket condenser is part of the refresh.
- New/refreshed A/C lines are installed where available.
- The rare high-pressure line has been installed and protected with a P-clip plus 5/8-in heater hose around the vulnerable section.
- A/C request/compressor loading has been observed during PowerFC idle diagnostics.
- Final Baseline closeout is a normal-use verification of cabin cooling and leak-free operation rather than more disassembly.

### Hydraulic power steering

The conventional hydraulic power-steering system has been restored after previously being deleted/bypassed at the rack.

Current state:

- Power-steering hardware/plumbing is installed.
- The accessory drive is back in the standard-length-belt hydraulic-PS configuration.
- Steering-wheel indexing has been corrected/recentered mechanically.
- Remaining closeout is a road verification of assist, leaks, belt tracking, pump behavior, and steering-wheel position.

Service lesson preserved for future work: the 2ZZ power-steering pump sliding/captive sleeves can be reset without hammer access using a bearing cup, the long PS-delete-pulley bolt, and two nuts as a compact press.

### Turbo service work completed during reassembly

The following current-turbo-system maintenance was completed while the front/passenger-side service area was open:

- Turbo coolant lines rebuilt.
- Turbo oil drain rebuilt.
- Engine oil changed.

These are Baseline maintenance actions on the current running configuration; they do not redefine the future Street Build turbo architecture.

### Intercooler piping / packaging

The existing intercooler piping has been reinstalled and the car returned to running configuration.

The A/C / PS / charge-pipe corridor was 3D-scanned before closeout. Review of the exposed corridor suggests that the current architecture does not offer much practical recoverable space without a larger redesign. Because the rare A/C line is now physically supported and protected, further Baseline effort on charge-pipe packaging is low-value relative to advancing the Street Build.

Follow-on CAD/fabrication of improved charge piping remains optional future refinement rather than a Baseline priority.

### Engine management / diagnostics

The current ECU is an APEXi Power FC using FC-Datalogit / FC-Edit.

A repeatable A/C-on idle hunt was diagnosed with logging rather than parts substitution. The key observed behavior was excessive idle-control authority plus a lean A/C-idle operating region. With O2 feedback disabled for diagnosis, hot A/C-off idle was reasonable while A/C-on idle at approximately 900 rpm went roughly 17.8:1 AFR.

The corrective change was intentionally local:

- Idle A/E target: 800 rpm.
- Idle A/C target: 900 rpm.
- Base Map row 3000 / 800 rpm: 2.152 -> 2.550.
- Base Map row 3000 / 1200 rpm: 2.152 -> 2.550.
- Injector scaling and injector-lag settings were left untouched.

With O2 feedback still off for the controlled test, the A/C-on AFR moved to approximately 14.8-15.0:1 and the idle hunt effectively disappeared. O2 feedback can therefore be used normally without having to rescue a large base-map error.

Preserve the diagnostic evidence and capture one additional driving log for the separate shift/rev-hang complaint. The useful channels are VTA/TPS, RPM, ISC command (`???(2)`), injector pulse width, AFR, and relevant A/C states. The purpose is to determine whether the engine is experiencing ECU/IAC dashpot behavior, delayed mechanical throttle closure, or another decel transition issue.

### Seats

The user has effectively committed to Recaro-compatible seat infrastructure.

Current state:

- Left/right Recaro-compatible Celica seat rails/brackets have been ordered from Japan.
- Delivery timing is uncertain.
- Suitable Recaro SR3 seats are being actively watched for.
- Seat installation is blocked until both rails and suitable seats are available.

Future upholstery or alternate Recaro choices do not need to be resolved for Baseline.

## Maintenance / catch-up

The car is now far enough along that Baseline is in closeout/validation rather than major reassembly.

Known remaining maintenance/diagnostic actions:

- Recheck manual-transmission fluid level/condition.
- Measure key-off parasitic draw with an ammeter and isolate the affected circuit by pulling fuses methodically.
- Replace brake fluid when a second set of hands is available for bleeding.
- Complete the remaining vehicle-level mechanical/roadworthiness audit from actual findings rather than a generic replacement list.

The audit should continue to cover, as applicable:

- fluid condition / known service intervals;
- visible leaks;
- belts and hoses;
- brakes;
- charging/battery behavior;
- obvious suspension/steering wear;
- lights, wipers, and basic roadworthiness.

## Administrative / road-legal

- State safety inspection must be scheduled and completed before the end of September 2026.
- Vehicle registration/tags also expire at the end of September 2026 and should be renewed before 2026-09-30.

## Execution logic

### Required now

1. Road-verify hydraulic power steering, steering-wheel position, and A/C operation after reassembly.
2. Capture a PowerFC diagnostic baseline including normal hot idle behavior and the shift/rev-hang event.
3. Schedule/complete the state safety inspection and renew registration/tags before month-end.
4. Recheck manual-transmission fluid.
5. Measure parasitic current draw and isolate the responsible fused circuit.
6. Replace brake fluid when helper availability allows.
7. Finish the baseline mechanical roadworthiness audit and create additional tasks only from real findings.

### Parallel / waiting

- Receive seat rails from Japan.
- Source suitable Recaro SR3 seats.
- Install seats when both prerequisites exist.

### Deferred refinement / Street Build priority

- The packaging scan is complete and suggests limited practical space can be recovered in the current corridor.
- Keep improved charge-pipe CAD/fabrication low priority unless a future service event creates a clear reason to revisit it.
- Direct near-term project energy toward the Street Build rather than further optimizing the current service corridor.

## Boundary with Street Build

Tires and major drivetrain/control modernization belong in the Street Build execution path, not Baseline.

The Baseline repo should remain focused on the current car and current powertrain becoming dependable and enjoyable before the replacement drivetrain module is ready.
