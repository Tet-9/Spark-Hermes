**This round:** rank 5 · Δ vs baseline +0.167 on 6 paired instances · 1 verified.

## Round `r0019` — `5E4iMWRACSJrnbnCLNVfWXjHc5VRkgzRfaAzBiB1VXfkqPUg`

**weight 0.0847** · score 0.0492

| | |
|---|---|
| episodes | 42 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.0492 |
| standard error (incl. reference term) | 0.05584 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0000 |
| score (mean d after the overfit and copy penalties) | +0.0492 |
| correctness gate | passed |
| Δe | api_calls -0.43 · tool_calls -0.41 |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.15 | 0.00 | -0.1533 | frontier |

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
| `swe-fix-r0019-02` | 1 | `42df64e7c1c0e441…` | pylint-dev__astroid.b114f6b5.func_basic__pvppi3p4 |
| `swe-fix-r0019-03` | 2 | `1db85f93f45d9161…` | oauthlib__oauthlib.1fd52536.func_pm_remove_assign__mab9thh9 |
| `swe-fix-r0019-04` | 9 | `f1aa7e64c5480c28…` | tkrajina__gpxpy.09fc46b3.func_pm_remove_cond__u7w4m9dk |
| `swe-fix-r0019-05` | 9 | `a42b15d796d23e4e…` | cantools__cantools.0c6a7871.func_pm_ctrl_shuffle__hmxdgq1i |
| `swe-fix-r0019-06` | 5 | `f760bfd45fe4c4a4…` | marshmallow-code__marshmallow.9716fc62.combine_module__wfo404sc |
| `swe-fix-r0019-09` | 10 | `a3181ea27927d645…` | pylint-dev__astroid.b114f6b5.combine_file__8ixha0c3 |

</details>