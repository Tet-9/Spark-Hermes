**This round:** rank 3 · Δ vs baseline +0.125 on 6 paired instances · 2 verified.

## Round `r0014` — `5C5JKnm8M8pyn6neLqwmAKZ7DoyzJf7ZB1Mabv62LwfSEsHh`

**weight 0.1137** · score 0.0537

| | |
|---|---|
| episodes | 48 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.0537 |
| standard error (incl. reference term) | 0.049143 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0000 |
| score (mean d after the overfit and copy penalties) | +0.0537 |
| correctness gate | passed |
| Δe | api_calls -0.38 · tool_calls -0.24 |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.22 | 0.26 | 0.0415 | frontier |

### Check the grading yourself

6 of 6 withheld commitments re-verified at close: **all match**.

Each instance's withheld half was committed to *before* submissions opened, as `hmac-sha256(salt, canonical_json(withheld))`. The commitment is in the task record — under `rounds/<id>/tasks/` when you were shown the scored tasks, under `rounds/<id>/evaluated/` when you were shown previews — and `rounds/queue.json` carried the digest of those records before the round opened. The salt and the half itself are published now, in `reveal.json`. Recompute it and confirm the criteria you were graded against are the ones that were fixed in advance:

```python
import hashlib, hmac, json
salt, withheld = reveal[task_id]["salt"], reveal[task_id]["withheld"]
body = json.dumps(withheld, sort_keys=True, separators=(",", ":"), ensure_ascii=False).encode()
"hmac-sha256:" + hmac.new(bytes.fromhex(salt), body, hashlib.sha256).hexdigest()
```

<details><summary>Revealed withheld halves (6) — full record in `reveal.json`</summary>

| task | withheld checks | salt | source |
|---|---|---|---|
| `swe-fix-r0014-00` | 5 | `09a19e021bcc1a1c…` | tobymao__sqlglot.036601ba.lm_rewrite__0omp5x37 |
| `swe-fix-r0014-01` | 8 | `18b12c1b90969baf…` | tobymao__sqlglot.036601ba.combine_module__f299g1y5 |
| `swe-fix-r0014-07` | 4 | `94fef8057637dda3…` | tobymao__sqlglot.036601ba.func_pm_ctrl_shuffle__kkljj8jz |
| `swe-fix-r0014-08` | 3 | `1004520f773e83be…` | cantools__cantools.0c6a7871.func_basic__b0n17uz1 |
| `swe-fix-r0014-09` | 1 | `f1f303477dad9888…` | tobymao__sqlglot.036601ba.func_pm_op_swap__54knfuhn |
| `swe-fix-r0014-12` | 1 | `320f1df43b4791ee…` | pylint-dev__astroid.b114f6b5.func_basic__o9h0uc6j |

</details>