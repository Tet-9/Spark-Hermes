**This round:** rank 3 · Δ vs baseline +0.167 on 6 paired instances · 2 verified.

## Round `r0011` — `5CoTfEgMhZ46ETtT6RSdt3RQkXizYu3vy9Spg33qTSt3eBtQ`

**weight 0.1469** · score 0.0778

| | |
|---|---|
| episodes | 48 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.0778 |
| standard error (incl. reference term) | 0.042646 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0232 |
| score (mean d after the overfit and copy penalties) | +0.0778 |
| correctness gate | passed |
| Δe | api_calls -0.23 · tool_calls -0.33 |
| overfit rate | 0.00 |
| disqualified episodes | 1 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.18 | 0.26 | 0.0823 | frontier |

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
| `swe-fix-r0011-00` | 5 | `3f05e4bbc990b819…` | cantools__cantools.0c6a7871.func_pm_remove_assign__eu45dl9g |
| `swe-fix-r0011-01` | 1 | `3a8b150cee2e40d7…` | cantools__cantools.0c6a7871.func_basic__n8m48vvt |
| `swe-fix-r0011-02` | 9 | `42364fd7799ecab8…` | cantools__cantools.0c6a7871.func_basic__msp2ns4n |
| `swe-fix-r0011-03` | 6 | `14c78c0f9a987d96…` | marshmallow-code__marshmallow.9716fc62.func_basic__xkq31sad |
| `swe-fix-r0011-05` | 6 | `b913fe6fb499ab75…` | pylint-dev__astroid.b114f6b5.func_basic__nonxkim6 |
| `swe-fix-r0011-07` | 3 | `65ec6109d4db8ea2…` | scanny__python-pptx.278b47b1.combine_file__6q0ljdu3 |

</details>