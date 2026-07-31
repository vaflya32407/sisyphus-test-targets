# sisyphus-test-targets

Public, immutable test matter for operational calibration of the Sysiphus OS,
PSN, Workbench, and selected virtual repositories (VRs).

This repository owns test objects only. It does not own VR processes, PSN
routing, Sysiphus execution, Workbench authority, admission, or operational
qualification.

## Layout

Each VR has an independent namespace:

```text
vr/<vr-id>/
  targets/       Remotely recovered source matter
  schemas/       Structural validation contracts
  expectations/  Deterministic processing and QC expectations
```

Current exemplar:

```text
vr/testvr/targets/web_recovery_array_v1.json
vr/testvr/schemas/web_recovery_array_v1.schema.json
vr/testvr/expectations/web_recovery_array_v1.expected.json
```

Future exemplars, including IG5, should use their own namespace, for example
`vr/ig5/`, and must not reuse TestVR truth or expectations.

## Operational use

An operational package must pin an exact repository commit and independently
record the recovered target's SHA-256. Branch URLs such as `main` are not
immutable operational inputs. The VR must recover and process the target;
expectation files are QC references and are not substitutes for execution.
