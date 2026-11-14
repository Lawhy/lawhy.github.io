# MiMo-RL with pi: Qwen3.8-27B and Qwen3.5-35B-A3B

pi trained through tokin with slime (fully async) on the code tasks of MiMo-V2.6-RL-oss, 256 held out (`examples/pi_mimo_rl/heldout.txt`), 2,442 for training. REINFORCE with truncated importance sampling, score centering and dynamic sampling; the 35B also replays expert routing (R3). Recipes are in `examples/pi_mimo_rl`.

Evaluation: pi on held-out MiMo (256 × 4) and Terminal-Bench 2.1 (89 × 4), 32,768 tokens per turn. Differences are checkpoint minus base, 95% CI from a paired bootstrap over tasks.

| setting | Qwen3.8-27B | Qwen3.5-35B-A3B |
|---|---|---|
| batch per step | 8 tasks × 8 trials | 64 tasks × 16 trials |
| tokens per turn, training | 8,192 | 8,192 |
| steps | 300 (~1.0 epoch) | 200 (~5.2 epochs) |
| nodes, 8× H200 | 3 training + 3 rollout | 3 training + 3 rollout |
| time per step (median) | ~7 min | ~44 min |

## Qwen3.8-27B

Base: MiMo 0.499 [0.453, 0.547], TB2.1 0.593 [0.508, 0.677]. The checkpoint is picked on held-out MiMo (`iter_299`), and TB2.1 is tested on that pick only.

| checkpoint | MiMo pass@1 | MiMo − base | TB2.1 − base |
|---|---|---|---|
| `iter_159` | 0.671 | +0.172 [+0.133, +0.212] | +0.051 [+0.000, +0.101] |
| `iter_269` | 0.790 | +0.291 [+0.241, +0.340] | +0.076 [+0.028, +0.126] |
| **`iter_299`** (blog) | **0.797** | **+0.298 [+0.246, +0.351]** | **+0.070 [+0.017, +0.124]** (sweep 2; sweep 1 +0.031, both +0.051) |

## Qwen3.5-35B-A3B

Base: MiMo 0.238 [0.203, 0.274], TB2.1 0.368 [0.281, 0.455].

| checkpoint | MiMo pass@1 | MiMo − base | TB2.1 pass@1 | TB2.1 − base |
|---|---|---|---|---|
| `iter_79` | 0.336 | +0.098 [+0.064, +0.131] | | |
| `iter_139` (first blog version) | 0.373 | +0.135 | 0.419 | +0.051 |
| `iter_149` | | | 0.452 | +0.084 [+0.045, +0.126] |
| `iter_159` | | | 0.407 | +0.039 [−0.006, +0.084] |
| `iter_169` | 0.363 | +0.125 [+0.090, +0.161] | 0.419 | +0.051 [+0.006, +0.098] |
| `iter_179` | 0.389 | +0.150 [+0.113, +0.188] | 0.424 | +0.056 [+0.008, +0.104] |
| `iter_189` | 0.368 | +0.130 [+0.093, +0.167] | 0.430 | +0.062 [+0.014, +0.110] |
| **`iter_199`** (blog, last) | **0.382** | **+0.144 [+0.106, +0.182]** | **0.480** | **+0.112 [+0.067, +0.163]** |
