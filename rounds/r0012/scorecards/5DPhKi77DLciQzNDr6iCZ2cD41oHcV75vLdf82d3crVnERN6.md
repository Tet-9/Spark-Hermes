**This round:** rank 1 · Δ vs baseline +0.200 on 6 paired instances · 2 verified.

## Round `r0012` — `5DPhKi77DLciQzNDr6iCZ2cD41oHcV75vLdf82d3crVnERN6`

**weight 0.4625** · score 0.2006

| | |
|---|---|
| episodes | 42 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.2006 |
| standard error (incl. reference term) | 0.060548 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.1231 |
| score (mean d after the overfit and copy penalties) | +0.2006 |
| correctness gate | passed |
| Δe | api_calls -0.21 · tool_calls +0.17 |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.21 | 0.26 | 0.049 | frontier |

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
| `swe-fix-r0012-04` | 1 | `8ee99209cfd9cad3…` | tkrajina__gpxpy.09fc46b3.lm_rewrite__mkmq07zn |
| `swe-fix-r0012-05` | 5 | `df1de8be0fd29c0c…` | python-openxml__python-docx.0cf6d71f.combine_file__lychidet |
| `swe-fix-r0012-10` | 5 | `c0d53c8c996e5cd3…` | python-openxml__python-docx.0cf6d71f.combine_file__zrhaslff |
| `swe-fix-r0012-14` | 3 | `a1207b88a6ba21f9…` | andialbrecht__sqlparse.e57923b3.func_basic__4ud5my8w |
| `swe-fix-r0012-18` | 1 | `9f2010b56fbccebe…` | pylint-dev__astroid.b114f6b5.func_basic__izqrok37 |
| `swe-fix-r0012-19` | 4 | `5fa7af02e9285687…` | pylint-dev__astroid.b114f6b5.pr_2182 |

</details>