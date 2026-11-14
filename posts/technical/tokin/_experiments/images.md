# GRPO with images: Qwen3.5-4B on geo3k (2026-11-12)

slime GRPO through an image-capable tokin, sglang 0.5.21. Thinking off, 3,072-token cap, 32 prompts × 8 samples a step, lr 2e-6, temperature 1, 2 turns (figure and question, then the same figure with a fixed recheck text), reward on the last answer. 183 steps; last save `iter_174`.

Eval: geo3k test, 601 problems × 4, temperature 0.6, top_p 0.95, same 2 turns through tokin. pass@1 scores turn 1. Differences are checkpoint minus base, paired bootstrap over problems.

| checkpoint | pass@1 | − base | cut at length |
|---|---|---|---|
| base | 0.692 | | 0.205 |
| `iter_49` | 0.801 | +0.109 [+0.085, +0.134] | 0.055 |
| `iter_99` | 0.802 | +0.110 [+0.084, +0.136] | 0.041 |
| **`iter_124`** | **0.825** | **+0.133 [+0.107, +0.159]** | 0.099 |
| `iter_174` | 0.808 | +0.116 [+0.089, +0.145] | 0.009 |

Part of the gain is fewer length cuts; this eval does not separate the two. tokin refused nothing over 47,616 training sessions.
