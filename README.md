# APRA Talk — Sample Dataset

Synthetic major gifts portfolio data for a Tableau intro workshop.

## Tables

| File | Rows | Description |
|------|------|-------------|
| `fundraisers.csv` | 5 | Major Gifts Officers with territory |
| `constituents.csv` | ~418 | Householded prospect records |
| `actions.csv` | ~3,500 | Contact reports (multiple per constituent) |
| `gifts.csv` | ~690 | Gift history (multiple per constituent) |
| `proposals.csv` | ~212 | Formal solicitation proposals |
| `ratings.csv` | ~1,050 | Wealth screening ratings (2–3 per constituent) |

## How to join them in Tableau

```
constituents.fundraiser_id  →  fundraisers.fundraiser_id
actions.constituent_id      →  constituents.constituent_id
gifts.constituent_id        →  constituents.constituent_id
proposals.constituent_id    →  constituents.constituent_id
ratings.constituent_id      →  constituents.constituent_id
```

Note: `fundraiser_name` only lives in `fundraisers.csv` — you need the join to get it.

## Useful calculated fields to try

**Most recent action only**
```
[action_number] = 1
```

**Most recent gift only**
```
[gift_number] = 1
```

**Lapsed donors (no gift in 12 months)**
```
DATEDIFF('day', [gift_date], TODAY()) > 365 OR ISNULL([gift_date])
```

**Open pipeline value**
```
IF [status] = "Pending" THEN [ask_amount] ELSE 0 END
```

## Rating categories

| Category | Value type | Source |
|----------|-----------|--------|
| Estimated Capacity | Dollar amount | DonorSearch, iWave, WealthEngine, Blackbaud Target Analytics |
| Likelihood to Give | Percentage | same |
| Real Estate | Dollar amount | same |

All data is fictional and generated for educational purposes.
