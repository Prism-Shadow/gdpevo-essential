# GDPevo Harbor tasks

Task data, environments and verifiers for the following PenguinHarness packages.

- [gdpevo-essential-court-clerk-operations-test](penguinharness-benchmark-gdpevo-essential-court-clerk-operations-test/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-court-clerk-operations-test)
- [gdpevo-essential-court-clerk-operations-train](penguinharness-benchmark-gdpevo-essential-court-clerk-operations-train/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-court-clerk-operations-train)
- [gdpevo-essential-coverage-review-test](penguinharness-benchmark-gdpevo-essential-coverage-review-test/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-coverage-review-test)
- [gdpevo-essential-coverage-review-train](penguinharness-benchmark-gdpevo-essential-coverage-review-train/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-coverage-review-train)
- [gdpevo-essential-engineering-portfolio-analytics-test](penguinharness-benchmark-gdpevo-essential-engineering-portfolio-analytics-test/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-engineering-portfolio-analytics-test)
- [gdpevo-essential-engineering-portfolio-analytics-train](penguinharness-benchmark-gdpevo-essential-engineering-portfolio-analytics-train/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-engineering-portfolio-analytics-train)
- [gdpevo-essential-financial-control-test](penguinharness-benchmark-gdpevo-essential-financial-control-test/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-financial-control-test)
- [gdpevo-essential-financial-control-train](penguinharness-benchmark-gdpevo-essential-financial-control-train/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-financial-control-train)
- [gdpevo-essential-portfolio-management-test](penguinharness-benchmark-gdpevo-essential-portfolio-management-test/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-portfolio-management-test)
- [gdpevo-essential-portfolio-management-train](penguinharness-benchmark-gdpevo-essential-portfolio-management-train/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-portfolio-management-train)
- [gdpevo-essential-service-ticket-resolution-test](penguinharness-benchmark-gdpevo-essential-service-ticket-resolution-test/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-service-ticket-resolution-test)
- [gdpevo-essential-service-ticket-resolution-train](penguinharness-benchmark-gdpevo-essential-service-ticket-resolution-train/README.md) · [package](https://github.com/Prism-Shadow/penguin-harness-benchmark/tree/main/packages/penguinharness-benchmark-gdpevo-essential-service-ticket-resolution-train)

## Running a task (for agents)

Run the Case's Harbor command from the root of the data checkout specified in
its statement. The examples use `ADAPTER_DIR` for the adapter directory
provided by the evaluator.

```bash
export PYTHONPATH="$ADAPTER_DIR"
```

For a Test batch, set `STATE_TAR` to the absolute path of the
Agent State frozen after training the same scenario. For example, from the
data repository root, run all five Service Ticket Resolution test questions as follows.

```bash
uvx --from harbor==0.23.0 harbor run \
  -c penguinharness-benchmark-gdpevo-essential-service-ticket-resolution-test/job.yaml \
  --ak "agent_state_tar=${STATE_TAR:?set STATE_TAR to the frozen Agent State archive}" -y
```

Use the model, time limits and network settings in the Case. The default host
limit is four concurrent trials. Apply the shared Docker network only when the
Case asks for it. For a network-restricted agent, `"$ADAPTER_DIR/agent_host.py"`
resolves the model's host from the configured Project.

Harbor writes the trial's `result.json` under the job output directory. Score
the verifier's reward as the Case rubric specifies. If the verifier produced no
reward or the model never ran, record an evaluation failure. Retry startup
failures after fixing their cause, under a new job name.
