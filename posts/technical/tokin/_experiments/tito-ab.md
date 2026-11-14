# TITO against re-rendering, policy frozen

Paired A/B at evaluation: one arm through tokin, the other through the same gateway re-rendering every turn from text. Shared: model, harness, Harbor 0.24.0, sglang 0.5.21, temperature 1.0, top_p 1.0, `max_tokens` 65,536. Terminal-Bench 2.1 is 89 × 4, SWE-bench Verified 500 × 1. Differences are tokin minus re-render, 95% CI from a bootstrap over tasks. Only setup failures are rerun; every other failure scores 0. Scored 2026-10-29.

| pair (Qwen3.6-35B-A3B) | n | re-render | tokin | tokin − re-render |
|---|---|---|---|---|
| TB2.1, mini-swe-agent | 356 | 0.480 | 0.435 | −0.045 [−0.090, −0.003] |
| TB2.1, opencode | 356 | 0.430 | 0.447 | +0.017 [−0.034, +0.067] |
| TB2.1, pi | 356 | 0.458 | 0.421 | −0.037 [−0.084, +0.011] |
| SWE-bench Verified, mini-swe-agent | 500 | 0.682 | 0.688 | +0.006 [−0.026, +0.038] |
| SWE-bench Verified, opencode | 500 | 0.666 | 0.660 | −0.006 [−0.042, +0.030] |
| SWE-bench Verified, pi | 500 | 0.640 | 0.690 | +0.050 [+0.014, +0.086] |
| **pooled, 6 pairs** (blog Appendix B) | 2,568 | 0.577 | 0.577 | **+0.001 [−0.015, +0.017]** |

The same 6 pairs on a non-public MoE checkpoint pool to −0.013 [−0.028, +0.003].
