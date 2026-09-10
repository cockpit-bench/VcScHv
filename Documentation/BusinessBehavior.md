# VcScHv: business behavior

Integer tick precharge deadline: 490/500 ms success, 510 ms rejected; low voltage cannot close.

These are local synthetic engineering requirements. They are not recovered internal algorithms or vehicle calibrations.

Raw-code bounds, physical ranges, conversion scale/offset and fallback are specified per signal in SignalEncoding.json. Age is a nonnegative single-precision value in seconds; status/reset/capture are Boolean. Two consecutive valid samples are required after reset or rejection. Digital channels have no artificial analog conversion stage; enumerations retain their uint8 state values.

## Responsibilities and ports

| Component | Inputs | Outputs (type; unit) |
|---|---|---|
| HighVoltageSequencer | BatteryVoltage, DcLinkVoltage, IsolationResistance, CrashSignal, DriveEnable, ChargeEnable, ContactorFeedback, PrechargeFeedback, valid, reset | CommandState (uint8; 1), ElapsedPrecharge (single; s), PrechargeRequest (boolean; boolean), MainRequest (boolean; boolean) |

Physical telemetry outputs are intentional downstream observations, including measurements not used by the local command law. InvalidChannelCount and the capture snapshot report reception health. They do not substitute for the domain-specific interlocks above.

## Independently checked behavior

| Requirement/property | Operator | Expected | Samples |
|---|---|---|---:|
| Precharge enters at request 49 | equal | 1 | 1 |
| Completion at 490 ms | equal | 2 | 1 |
| Precharge enters at request 50 | equal | 1 | 1 |
| Completion at 500 ms | equal | 2 | 1 |
| Precharge enters at request 51 | equal | 1 | 1 |
| Completion at 510 ms | equal | 3 | 1 |
| Zero voltage cannot close contactor | equal | 0 | 60 |

Precharge starts at elapsed tick zero. Completion may close at 490 or 500 ms; a first completion at 510 ms is too late. No valid completion by 500 ms enters a latched fault. Battery voltage must be at least 100 V, DC link at least 95% of battery voltage, and precharge feedback true. Capture is reserved and has no effect; this module has no snapshot output.

## Test interpretation

Independent channel qualification/conversion/capture calculation plus explicit business point and temporal properties. Unconstrained business outputs are measured, not labelled independently expected.

All recorded stimuli passed the independently specified channel, diagnostic and business checks. This is bounded synthetic behavior verification, not exhaustive requirements coverage. The accompanying measured replay outputs are provided for implementation comparison; they are not an independent expected-answer oracle.

Simulink Coverage metrics retain their native names. C statement coverage, BTC execution, physical ECU operation and SIL/PIL/HIL are not claimed.
