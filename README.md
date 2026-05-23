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

## How to join them in Tableau

```
constituents.fundraiser_id  →  fundraisers.fundraiser_id
actions.constituent_id      →  constituents.constituent_id
gifts.constituent_id        →  constituents.constituent_id
proposals.constituent_id    →  constituents.constituent_id
```

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

All data is fictional and generated for educational purposes.
