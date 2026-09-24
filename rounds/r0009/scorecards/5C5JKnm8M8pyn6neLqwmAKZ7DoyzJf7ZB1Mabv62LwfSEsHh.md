**This round:** rank 2 · Δ vs baseline +0.192 on 6 paired instances · 0 verified.

## Round `r0009` — `5C5JKnm8M8pyn6neLqwmAKZ7DoyzJf7ZB1Mabv62LwfSEsHh`

**weight 0.0552** · score 0.0269

| | |
|---|---|
| episodes | 18 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.0269 |
| standard error (incl. reference term) | 0.101524 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0000 |
| score (mean d after the overfit and copy penalties) | +0.0269 |
| correctness gate | passed |
| Δe | — |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.20 | 0.26 | 0.0657 | frontier |

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
| `swe-fix-r0009-00` | 7 | `208bc683ff0b0fb5…` | pylint-dev__astroid.b114f6b5.func_pm_class_rm_funcs__52zh7ra7 |
| `swe-fix-r0009-01` | 5 | `27c7aa43d71b0dec…` | tobymao__sqlglot.036601ba.func_pm_remove_assign__ondxskdy |
| `swe-fix-r0009-05` | 5 | `c3328abb894cdc2b…` | python-openxml__python-docx.0cf6d71f.func_basic__nh3pbov7 |
| `swe-fix-r0009-08` | 2 | `199743210e7f2e9a…` | pylint-dev__astroid.b114f6b5.combine_file__ajevivfk |
| `swe-fix-r0009-09` | 4 | `3fae235ac5700e81…` | pylint-dev__astroid.b114f6b5.func_pm_class_rm_funcs__9qbm1ad3 |
| `swe-fix-r0009-11` | 4 | `53af60134e38c5ac…` | scanny__python-pptx.278b47b1.lm_rewrite__iddgx4vd |

</details>