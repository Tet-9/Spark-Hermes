**This round:** not ranked · Δ vs baseline +0.000 on 6 paired instances · 0 verified.

## Round `r0010` — `5C5JKnm8M8pyn6neLqwmAKZ7DoyzJf7ZB1Mabv62LwfSEsHh`

**weight 0.0481** · score 0.0201

| | |
|---|---|
| episodes | 24 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.0201 |
| standard error (incl. reference term) | 0.075628 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0000 |
| score (mean d after the overfit and copy penalties) | +0.0201 |
| correctness gate | passed |
| Δe | — |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.19 | 0.26 | 0.0726 | frontier |

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
| `swe-fix-r0010-00` | 7 | `75dcb686a6e10e67…` | cantools__cantools.0c6a7871.lm_rewrite__68i7a30o |
| `swe-fix-r0010-05` | 3 | `1d56ca5f00af441e…` | andialbrecht__sqlparse.e57923b3.combine_file__ntlkm4ui |
| `swe-fix-r0010-06` | 1 | `b4f52137d1798d7e…` | cantools__cantools.0c6a7871.lm_rewrite__pmmbpkot |
| `swe-fix-r0010-07` | 3 | `79faaf0760d9007b…` | python-openxml__python-docx.0cf6d71f.func_basic__lwpo0ghu |
| `swe-fix-r0010-08` | 3 | `0c1419dcde93d671…` | scanny__python-pptx.278b47b1.lm_rewrite__rala1oem |
| `swe-fix-r0010-10` | 1 | `648ba391de01725e…` | cantools__cantools.0c6a7871.func_pm_remove_assign__2hwa7vf6 |

</details>