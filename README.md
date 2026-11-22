# BRACKEN DDoS Defense

**Detection and controlled mitigation of disruptive network traffic.**

BRACKEN DDoS is intended to analyze traffic signals and help detect denial-of-service activity, then coordinate bounded mitigation actions through BRACKEN network components. It should make detection explainable and mitigation auditable, with safe defaults that avoid turning uncertain classifications into disruptive actions.

> **Project status:** Early-stage project. Detection coverage, thresholds, automated actions, and effectiveness have not been validated.

## Responsibilities

- Define signal inputs and traffic baselines for detection.
- Detect and classify patterns such as SYN, UDP, ICMP, HTTP, and DNS floods as capabilities are implemented.
- Correlate activity across flows and destination ranges, including distributed patterns that may evade per-address thresholds.
- Recommend or apply configured rate limits and filters through the [data plane](https://github.com/vayun-networks/bracken-data-plane) and [network engine](https://github.com/vayun-networks/bracken-network-engine).
- Record evidence, action, duration, and operator override for each mitigation.
- Provide metrics and event data to [analytics](https://github.com/vayun-networks/bracken-analytics) and [observability](https://github.com/vayun-networks/bracken-observability).

## Safety model

Detection, recommendation, and enforcement should be separate states. Mitigation should have explicit scope, limits, expiry, and rollback behavior. False positives can interrupt legitimate traffic, so thresholds and automated response policies must be explainable, tested, and operator-configurable. Begin in an observe-only mode before considering automated enforcement.

## Planned milestones

1. Define traffic signals and a replayable synthetic test corpus.
2. Implement baseline and rule-based detectors with measured false-positive behavior.
3. Add distributed destination-range correlation and reporting.
4. Integrate a bounded mitigation API with dry-run and expiry controls.
5. Evaluate effectiveness in an isolated lab using authorized traffic only.

Machine-learning-assisted classification may be explored after reliable telemetry and a representative evaluation set exist; it should not replace explainable baseline detection.

## Development

No live attack simulation or third-party traffic generation is appropriate. Use isolated labs, synthetic traces, and infrastructure you own or are authorized to test. Performance and effectiveness claims must state traffic mix, scale, hardware, detection delay, and false-positive methodology.

## Related components

- [bracken-data-plane](https://github.com/vayun-networks/bracken-data-plane)
- [bracken-network-engine](https://github.com/vayun-networks/bracken-network-engine)
- [bracken-control-plane](https://github.com/vayun-networks/bracken-control-plane)
- [bracken-analytics](https://github.com/vayun-networks/bracken-analytics)