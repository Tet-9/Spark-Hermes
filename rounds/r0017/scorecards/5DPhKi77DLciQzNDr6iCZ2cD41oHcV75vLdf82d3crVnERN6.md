**This round:** not ranked · Δ vs baseline +0.000 on 6 paired instances · 0 verified.

## Round `r0017` — `5DPhKi77DLciQzNDr6iCZ2cD41oHcV75vLdf82d3crVnERN6`

**weight 0.4604** · score 0.1658

| | |
|---|---|
| episodes | 48 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.1658 |
| standard error (incl. reference term) | 0.054777 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0957 |
| score (mean d after the overfit and copy penalties) | +0.1658 |
| correctness gate | passed |
| Δe | api_calls +0.03 · tool_calls +0.31 |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.18 | 0.00 | -0.1783 | frontier |

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
| `swe-fix-r0017-00` | 7 | `73dbd36f22283c1f…` | pylint-dev__astroid.b114f6b5.lm_rewrite__t5os4bjm |
| `swe-fix-r0017-01` | 4 | `abee37a6b63e135a…` | andialbrecht__sqlparse.e57923b3.func_basic__w5xxgnz7 |
| `swe-fix-r0017-03` | 3 | `59e4a63df4de4d39…` | pylint-dev__astroid.b114f6b5.combine_file__eeo3zas1 |
| `swe-fix-r0017-04` | 1 | `c84601baba423ecc…` | tkrajina__gpxpy.09fc46b3.lm_rewrite__ar7f0i4u |
| `swe-fix-r0017-06` | 3 | `3e2fb0b5b2f451e0…` | tobymao__sqlglot.036601ba.lm_rewrite__0g2hcgqg |
| `swe-fix-r0017-07` | 8 | `c89fa12fc6964741…` | cantools__cantools.0c6a7871.combine_file__xalpxrfc |

</details>