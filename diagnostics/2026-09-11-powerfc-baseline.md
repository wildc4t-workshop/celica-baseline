# PowerFC Baseline Diagnostics — 2026-09-11

## Purpose

Capture the current APEXi Power FC / FC-Datalogit baseline before further street driving so future behavior can be compared against measured data rather than memory.

Current vehicle: 2000 Toyota Celica GT-S, 2ZZ-GE, manual, turbocharged.

## Source-of-truth rule

The values below come from a fresh ECU `Read All` / controlled 2026-09-11 testing. Older saved `.dat` files are historical references only and must not be treated as current ECU truth without readback verification.

Known current/fresh-read settings established during this session include:

- Rev Limit: 8300 rpm
- VTLI High: 8900 rpm
- VTLI Low: 5650 rpm
- F/C A/E: 1100 rpm
- F/C A/C: 1200 rpm
- Idle A/E: 800 rpm after the diagnostic change
- Idle A/C: 900 rpm after the diagnostic change
- O2 F/B Control: returned to normal operation after open-loop diagnosis
- Idle-IG Control: ON
- O2 Feedback Setting: 1.047
- Injector correction/scaling: 55.0% on all four injectors

Do not silently substitute the older saved-file values for any of these. The unusual VTLI High/Low relationship is preserved as observed configuration and should be verified against actual lift behavior before using it as a test threshold.

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
- Sensor-zone `O2S` — conventional narrowband-like oxygen-sensor signal used for rich/lean corroboration

Do not substitute the later Advanced-zone `O2S1` field for the conventional Sensor-zone `O2S` signal when interpreting narrowband switching.

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
- Sensor `O2S`: rich-side voltage, consistent with the wideband
- ISC command: very low
- PIM: ~1900
- AFL V: ~1.17
- Inj ms: ~1.78

A/C ON hot idle was approximately:

- RPM: ~900
- AFR: ~17.8
- Sensor `O2S`: effectively pinned lean
- ISC command: ~390-400
- PIM: ~3000-3300
- AFL V: ~1.5
- Inj ms: ~2.1

Both the AEM wideband and OEM O2 sensor independently indicated the lean condition. O2 feedback therefore was not the root cause; when enabled it was correcting a large base-fueling error.

Relevant diagnostic log files from this session:

- `Log_20260911_1150.txt` — original A/C idle hunt
- `Log_20260911_1234 (throttle).txt` — throttle-guided stabilization and A/C transition behavior
- `Log_20260911_1301.txt` — O2 feedback OFF, stable 800/900-rpm comparison demonstrating A/C-specific lean condition
- `Log_20260911_1305.txt` — O2 feedback ON, demonstrating closed-loop correction of the same A/C-idle region

## O2-feedback comparison

At comparable stable A/C-on conditions with the same 800/900-rpm idle targets:

O2 feedback OFF:

- RPM: ~908 rpm
- AFR: ~17.77
- Sensor `O2S`: pinned lean
- Inj ms: ~2.12
- AFL V: ~1.51
- PIM: ~3296
- ISC command: ~396

O2 feedback ON:

- RPM: ~901 rpm
- AFR: ~15.22 average during the representative stable window
- Sensor `O2S`: switching lean/rich rather than pinned lean
- Inj ms: ~2.10
- AFL V: ~1.42
- PIM: ~3012
- ISC command: ~281

This confirms that O2 feedback materially corrected the A/C-idle mixture but did not create the original lean condition. Feedback also showed slow carryover across A/C load transitions, including temporary rich excursions after A/C was switched off, so base-map work was performed with feedback OFF.

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

Final current local correction:

- Idle A/E: 800 rpm
- Idle A/C: 900 rpm
- Base Map 3000 / 800 rpm: 2.550
- Base Map 3000 / 1200 rpm: 2.550
- injector correction/scaling: unchanged at 55.0%
- injector lag/deadtime table: unchanged

The idle hunt effectively disappeared after correcting the lean A/C-idle region. O2 feedback was returned to normal operation after the open-loop verification.

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

## Street Build handoff

This file owns the current Baseline drivability diagnosis. The broader pre-EMU archive remains owned by `celica-street-build/PRE_EMU_BASELINE.md` and should carry forward this corrected known-running PowerFC state rather than an older saved calibration.
