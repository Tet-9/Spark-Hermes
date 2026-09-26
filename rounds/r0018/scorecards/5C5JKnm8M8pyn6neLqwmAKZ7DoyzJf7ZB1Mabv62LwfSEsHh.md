**This round:** rank 3 · Δ vs baseline +0.167 on 6 paired instances · 1 verified.

## Round `r0018` — `5C5JKnm8M8pyn6neLqwmAKZ7DoyzJf7ZB1Mabv62LwfSEsHh`

**weight 0.2062** · score 0.0992

| | |
|---|---|
| episodes | 48 |
| mean d (your share of checks passed − the baseline's, same instances) | +0.0992 |
| standard error (incl. reference term) | 0.041534 |
| Δc (one-sided 90 % lower bound — how sure the gain is) | 0.0460 |
| score (mean d after the overfit and copy penalties) | +0.0992 |
| correctness gate | passed |
| Δe | api_calls -0.02 · tool_calls +0.22 |
| overfit rate | 0.00 |
| disqualified episodes | 0 |

`mean d` is the share of each task's withheld checks your episodes passed, minus the pinned model's share on the *same instances* with no strategy. Passing tasks is not the achievement — beating that baseline is. `Δc` is the lower bound of that difference, so beating the baseline on average is not enough to be *paid* for beating it.

### The baseline you were measured against

| family | null n | null credit | canon credit | Δc canon | label |
|---|---|---|---|---|---|
| `swe_fix` | 48 | 0.16 | 0.00 | -0.1644 | frontier |

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
| `swe-fix-r0018-01` | 1 | `debbdfa4743b9b72…` | cantools__cantools.0c6a7871.func_basic__vxezr2bg |
| `swe-fix-r0018-05` | 2 | `a2c6796c643ed5e3…` | python-openxml__python-docx.0cf6d71f.lm_rewrite__45j5meax |
| `swe-fix-r0018-06` | 8 | `e62484de83cf14a3…` | cantools__cantools.0c6a7871.func_pm_ctrl_invert_if__5ktbi8j7 |
| `swe-fix-r0018-07` | 5 | `1f2becd7b74ca424…` | pylint-dev__astroid.b114f6b5.func_pm_ctrl_invert_if__rkzmg83q |
| `swe-fix-r0018-08` | 4 | `e03f8b4281bb24a2…` | pylint-dev__astroid.b114f6b5.pr_2229 |
| `swe-fix-r0018-09` | 4 | `8c47fbb2caf298af…` | oauthlib__oauthlib.1fd52536.combine_file__r5mt1rid |

</details>