# `examples/harbor_eval`: Qwen3.6-35B-A3B across harnesses

Each sample runs the harness on its own tokin session in an E2B sandbox, served by sglang. temperature 1.0, top_p 1.0, `max_tokens` 65,536, memory ×2, agent timeout 86,400 s, `top_k` unset (the Codex and Claude Code runs set −1 explicitly: their server filled an unset `top_k` with 20). Terminal-Bench 2.1 is 89 × 4, SWE-bench Verified 500 × 1. Infra failures get 3 attempts.

| | mini-swe-agent | opencode | pi | Codex | Claude Code |
|---|:---:|:---:|:---:|:---:|:---:|
| Terminal-Bench 2.1, pass@1 | 0.451 | 0.454 | 0.438 | 0.441 | pending |
| Terminal-Bench 2.1, pass@4 | 0.616 | 0.655 | 0.625 | 0.663 | pending |
| SWE-bench Verified, pass@1 | 0.689 | 0.666 | 0.690 | 0.658 | 0.686 |
| recorded | 2026-11-05 | 2026-11-05 | 2026-11-05 | 2026-11-13 | 2026-11-13 |

- Codex 0.167.1 via the Responses API; Claude Code 2.1.325 via a prototype Messages API adapter (not on `main`).
- Codex TB2.1: 17 runs ended by a length cut (Codex stops the run), 1 by a full disk; 0 tokin refusals.
- Claude Code TB2.1: image tasks fail, since tokin refuses images in tool results.
