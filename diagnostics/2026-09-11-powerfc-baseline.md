# PowerFC Baseline Diagnostics — 2026-09-11

## Purpose

Capture the current APEXi Power FC / FC-Datalogit baseline before further street driving so future behavior can be compared against measured data rather than memory.

Current vehicle: 2000 Toyota Celica GT-S, 2ZZ-GE, manual, turbocharged.

## Logging configuration

Useful FC-Datalogit logging zones for the current work:

- Advanced
- Sensor
- Aux a/d

Important channels:

- RPM
- PIM/load
- AFL V / MAF signal
- VTA / throttle position
- Inj ms
- IGN
- battery voltage
- coolant temperature
- A/C request and compressor-relay state
- AN1 Wide Band
- `???(2)` — identified in current diagnosis as ISC/IAC actuator command, 0-1000 scaling
- OEM O2 sensor voltage

## A/C idle-hunt diagnosis

### Initial symptom

With the former high idle targets, enabling A/C produced a repeatable oscillation approximately in the 700-1300 rpm range.

Observed behavior showed:

- throttle physically closed;
- A/C request remaining continuously active;
- injectors not entering repeated fuel cut during the hunt;
- ISC command moving strongly opposite RPM;
- RPM falling, ISC opening aggressively, delayed airflow response, RPM overshooting, then ISC closing and repeating.

This identified the primary oscillation as a closed-loop idle-air-control hunt rather than decel fuel-cut cycling.

### Controlled A/C-on lean condition

With O2 feedback disabled for diagnosis and idle targets reduced to 800 rpm normal / 900 rpm A/C:

A/C OFF hot idle was approximately:

- RPM: ~800
- AFR: ~14.0
- ISC command: very low
- PIM: ~1900
- AFL V: ~1.17
- Inj ms: ~1.78

A/C ON hot idle was approximately:

- RPM: ~900
- AFR: ~17.8
- ISC command: ~390-400
- PIM: ~3000-3300
- AFL V: ~1.5
- Inj ms: ~2.1

Both the AEM wideband and OEM O2 sensor indicated the lean condition. O2 feedback therefore was not the root cause; when enabled it was correcting a large base-fueling error.

Relevant diagnostic log files from this session:

- `Log_20260911_1150.txt` — original A/C idle hunt
- `Log_20260911_1234 (throttle).txt` — throttle-guided stabilization and A/C transition behavior
- `Log_20260911_1301.txt` — O2 feedback OFF, stable 800/900-rpm comparison demonstrating A/C-specific lean condition
- `Log_20260911_1305.txt` — O2 feedback ON, demonstrating closed-loop correction of the same A/C-idle region

## Base-map correction

Map Trace showed the A/C-on idle operating in the PowerFC Base Map around the 3000-load row between the 800- and 1200-rpm columns.

Original cells:

- 3000 load / 800 rpm: 2.152
- 3000 load / 1200 rpm: 2.152

First controlled change:

- both cells -> 2.350
- observed A/C-on AFR improved to approximately 16.2

Second controlled change:

- both cells -> 2.550
- observed A/C-on AFR improved to approximately 14.8-15.0, including with the cooling fan running

Final current settings for this local correction:

- Idle A/E: 800 rpm
- Idle A/C: 900 rpm
- Base Map 3000 / 800 rpm: 2.550
- Base Map 3000 / 1200 rpm: 2.550
- injector correction/scaling: unchanged
- injector lag/deadtime table: unchanged

The idle hunt effectively disappeared after correcting the lean A/C-idle region. O2 feedback may be returned to normal operation now that the base calibration is close enough that closed-loop control is making modest rather than rescue-level corrections.

## Rev-hang / shift-transition complaint

### Driver observation

During normal manual shifts, throttle/revs do not appear to respond immediately when the accelerator is released and the clutch is depressed at nearly the same time. Shifts feel cleaner if the accelerator is released slightly before clutch-in.

Because the car uses a cable throttle, the PowerFC cannot electronically hold the throttle blade open. A likely ECU-side mechanism is ISC/IAC dashpot airflow during deceleration, but this remains to be measured rather than assumed.

### Required road log

Capture several normal 2-3 and/or 3-4 shifts with the same logging configuration.

Evaluate at minimum:

- VTA/TPS return rate
- RPM decay
- `???(2)` ISC command during and immediately after lift
- Inj ms / fuel-cut behavior
- AFR
- vehicle speed if available

Interpretation target:

- VTA closes immediately while ISC remains elevated and RPM hangs -> likely ISC/dashpot behavior.
- VTA itself closes slowly -> mechanical throttle/cable/TPS issue.
- VTA and ISC both close but fuel remains unexpectedly active -> investigate decel/fuel-cut logic.
- VTA and ISC both close normally and RPM still hangs -> investigate non-ECU mechanical/inertial causes.

Do not change fuel-cut or idle-control settings until the driving log identifies which mechanism is actually responsible.
