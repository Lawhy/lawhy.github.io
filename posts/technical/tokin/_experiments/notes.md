# Pitfalls

Things that cost time or silently changed results, one line each.

## Serving and sampling
- sglang 0.5.21 defaults to `--sampling-defaults model`: an unset `top_k` becomes the model's (20 for Qwen3.6). Comparable runs need `openai` or an explicit `top_k`.
- sglang re-tokenizes multimodal prompts silently (12–13% of later turns on Qwen3.5) unless run with `--mm-preprocess-cache-size-mb`; check the returned prompt ids.
- sglang's fast (GPU) image processor OOMed an engine during weight sync; use `--sglang-image-processor-backend pil` and the PIL processor in the trainer too.
- EAGLE speculative decoding breaks R3: only 72.8% of expert sets match a plain prefill (98.1% without). Turn EAGLE off with routing replay.
- slime `--save-hf` on Qwen3.5 drops the `mtp.*` and `model.visual.*` tensors; sglang loads the save without error and then emits padded-vocab ids. Copy those tensors from the base.

## Harnesses
- An 8k per-turn cap at eval ends pi's session when the first turn thinks past it: the 27B looked worse at 8k (−0.065) and better at 32k (+0.051).
- A length cut ends Codex's whole run; Claude Code survives one or two in a row and exits on the third.
- Harnesses see their base URL in the shell env; the model can call tokin itself. Exclude `OPENAI_*` / `ANTHROPIC_*` from tool environments.
- Claude Code: tool search grows the tool list mid-session (set `ENABLE_TOOL_SEARCH=false`); WebFetch and WebSearch add stray roots; the fork subagent resends the parent without its reasoning, so `attach` branches one turn early.
- Codex refuses `rm -rf`-style commands even in bypass mode.

## Infra
- A save in slime's fully async mode waits for every in-flight group: 30–53 min drains.
- Many trials importing Python deps from Lustre at once deadlock on lock waits; install deps on local disk and set `PYTHONPYCACHEPREFIX=/tmp`.
- A single ~57k-token leaf alone in a micro-batch needs ~28 GiB of logits; long agent leaves need TP2+.
- Syncing a new file to the shared filesystem can take 12–45 min; ship one tarball.
- uvicorn's default 5 s keep-alive races httpx connection reuse; set `timeout_keep_alive=75`.
- An outage of an external host (GitHub) during a sweep fails verifiers en masse; that TB2.1 sweep of the 35B `iter_79` is not a measurement.
