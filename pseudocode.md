# Conceptual multi-agent refinement workflow

Retrieved reference cases are illustrative context. Retrieval is a conceptual input in this schematic, rather than an implemented or evaluated module. Agent names denote functional roles.

```text
Input: PET–CT visual features and retrieved reference cases

report ← ReportAgent.generate(visual features, reference cases)

For each round up to the maximum number of rounds:
    score, feedback ← QualityControlAgent.assess(visual features, report)
    If the consistency threshold is reached or this is the last round:
        Stop
    report ← RevisionAgent.revise(report, feedback, visual features)

Output: final report
```
