**This round:** rank 1 · Δ vs baseline +0.278 on 6 paired instances · 2 verified.

## Round `r0013` — `5DPhKi77DLciQzNDr6iCZ2cD41oHcV75vLdf82d3crVnERN6`

**weight 0.4771** · score 0.2102

| | |
|---|---|
| episodes | 48 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.2102 |
| standard error (incl. reference term) | 0.059521 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.1340 |
| score (mean d after the overfit and copy penalties) | +0.2102 |
| correctness gate | passed |
| Δe | api_calls -0.51 · tool_calls -0.35 |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.21 | 0.26 | 0.0467 | frontier |

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
| `swe-fix-r0013-01` | 1 | `6c98ba7064ea2f8b…` | pylint-dev__astroid.b114f6b5.lm_rewrite__38a7otea |
| `swe-fix-r0013-03` | 2 | `433b8a604167056b…` | cantools__cantools.0c6a7871.combine_file__f6vezn2z |
| `swe-fix-r0013-04` | 6 | `f0118bf75c43d850…` | python-openxml__python-docx.0cf6d71f.func_basic__kroszka6 |
| `swe-fix-r0013-06` | 7 | `402b7d0abbb301f5…` | python-openxml__python-docx.0cf6d71f.combine_file__iyoh8wky |
| `swe-fix-r0013-08` | 7 | `aef057a406c123dc…` | pylint-dev__astroid.b114f6b5.func_basic__bla0eya9 |
| `swe-fix-r0013-11` | 1 | `85703647385b2b80…` | tkrajina__gpxpy.09fc46b3.combine_file__cj7fx7u3 |

</details>