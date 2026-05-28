# APRA Talk — Sample Dataset

Synthetic major gifts portfolio data for a Tableau intro workshop. All data is fictional and generated for educational purposes.

---

## Step 1 — Download the data

You do not need a GitHub account or any technical knowledge to download these files.

**Easiest option — download everything at once:**

1. Click the green **Code** button at the top of this page
2. Click **Download ZIP**
3. Unzip the folder somewhere easy to find, like your Desktop

That's it. You'll have all six CSV files ready to go.

**To download a single file:**

1. Click the filename (e.g. `constituents.csv`)
2. Click the **Download raw file** button (the download icon in the top right of the file view)
3. Save it wherever you like

---

## Step 2 — Open the data in Tableau

You'll need **Tableau Desktop** (paid, likely available through your institution) or **Tableau Public** (free at [public.tableau.com](https://public.tableau.com)).

> ⚠️ If you use Tableau Public, do not connect your real donor data — everything saves publicly. This sample dataset is fine since it's already public.

1. Open Tableau
2. Under **Connect**, choose **Text File**
3. Navigate to the folder where you saved the files and open `constituents.csv`
4. You'll land on the data source screen — this is where you'll connect the other tables

---

## Step 3 — Connect the tables

The six files are designed to be joined together. Think of `constituents.csv` as the center — everything else links back to it.

In the data source screen, drag each remaining CSV file from the left panel onto the canvas. Tableau will create a **Relationship** between them. Set the join keys like this:

| Left table | Field | Right table | Field |
|---|---|---|---|
| constituents | `fundraiser_id` | fundraisers | `fundraiser_id` |
| constituents | `constituent_id` | actions | `constituent_id` |
| constituents | `constituent_id` | gifts | `constituent_id` |
| constituents | `constituent_id` | proposals | `constituent_id` |
| constituents | `constituent_id` | ratings | `constituent_id` |

Once connected, click a sheet tab at the bottom to start building.

---

## What's in each file

| File | Rows | Description |
|------|------|-------------|
| `fundraisers.csv` | 5 | The 5 Major Gifts Officers |
| `constituents.csv` | ~418 | Householded prospect records — one row per household |
| `actions.csv` | ~3,400 | Contact reports — multiple rows per constituent |
| `gifts.csv` | ~700 | Gift history — multiple rows per constituent |
| `proposals.csv` | ~230 | Formal solicitation proposals |
| `ratings.csv` | ~1,030 | Wealth screening ratings (2–3 per constituent) |

A few things to know:
- `action_number = 1` is the **most recent** action for that person. Filter on it to get one row per constituent.
- `gift_number = 1` is the **most recent** gift. Same idea.
- `fundraiser_name` only lives in `fundraisers.csv` — join to it via `fundraiser_id` to get the name.

---

## Useful calculated fields to try

**Most recent action only**
```
[action_number] = 1
```

**Most recent gift only**
```
[gift_number] = 1
```

**Days since last action**
```
DATEDIFF('day', [action_date], TODAY())
```

**Lapsed donors — no gift in 12+ months**
```
DATEDIFF('day', [gift_date], TODAY()) > 365 OR ISNULL([gift_date])
```

**Open proposal pipeline value**
```
IF [status] = "Pending" THEN [ask_amount] ELSE 0 END
```

> **Tip:** If a filter isn't working as expected, right-click it on the Filters shelf and choose **Add to Context**. If you can't filter on a number field, right-click the field in the Data pane and choose **Convert to Dimension**.

---

## Rating categories

| Category | Value type |
|----------|------------|
| Estimated Capacity | Dollar amount |
| Likelihood to Give | Percentage (0–100) |
| Real Estate | Dollar amount |

Screening sources represented: DonorSearch, iWave, WealthEngine, Blackbaud Target Analytics.
