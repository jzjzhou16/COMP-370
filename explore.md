# COMP 370/570 Homework 4 — Dataset Exploration

## Task 3: Explore My Little Pony Dataset Properties

Dataset used: `clean_dialog.csv`

### 1. How big is the dataset?

Commands used:

```bash
ls -lh clean_dialog.csv
wc -l clean_dialog.csv
```

What to record:
- `ls -lh` gives the file size.
- `wc -l` gives the number of rows/lines in the file.
- Remember that the first row may be the header, so if you want the number of data rows only, subtract 1.

Result:

- File size: **[FILL IN]**
- Total rows including header: **[FILL IN]**
- Data rows excluding header: **[FILL IN]**

---

### 2. What is the structure of the data?

Commands used:

```bash
head clean_dialog.csv
csvtool head 5 clean_dialog.csv
```

To inspect the column names:

```bash
head -n 1 clean_dialog.csv
```

To inspect specific columns:

```bash
csvtool col 1 clean_dialog.csv | head
csvtool col 2 clean_dialog.csv | head
csvtool col 3 clean_dialog.csv | head
```

Result:

The dataset contains the following fields:

- **[FIELD 1]** — [brief description / example]
- **[FIELD 2]** — [brief description / example]
- **[FIELD 3]** — [brief description / example]
- **[ADD MORE IF NEEDED]**

Example row:

```text
[PASTE ONE EXAMPLE ROW HERE]
```

---

### 3. How many episodes does the dataset cover?

First identify which column contains the episode identifier/name.

If the episode is in column `N`, run:

```bash
csvtool col N clean_dialog.csv | tail -n +2 | sort | uniq | wc -l
```

You can also inspect the unique episode values with:

```bash
csvtool col N clean_dialog.csv | tail -n +2 | sort | uniq
```

Result:

- Number of unique episodes: **[FILL IN]**

---

### 4. Unexpected aspect of the dataset

Use commands such as:

```bash
head -20 clean_dialog.csv
tail -20 clean_dialog.csv
grep -n 'pattern' clean_dialog.csv | head
csvtool col N clean_dialog.csv | sort | uniq -c | sort -nr | head -20
```

Possible things to look for:
- inconsistent speaker names
- capitalization differences
- punctuation or commas inside dialogue
- missing values
- unusual character names
- duplicate-looking rows
- episode names stored inconsistently

Unexpected issue found:

**[DESCRIBE ONE REAL ISSUE YOU FOUND]**

Why this could matter later:

**[EXPLAIN HOW IT COULD AFFECT COUNTING, FILTERING, OR ANALYSIS]**

Command(s) used to discover it:

```bash
[PASTE COMMANDS HERE]
```

---

## Task 4: Analyze Speaker Frequency

The assignment asks for these MAIN ponies:

- Twilight Sparkle
- Rarity
- Pinkie Pie
- Rainbow Dash
- Fluttershy

First determine which column contains the speaker name.

If the speaker field is column `N`, you can inspect it with:

```bash
csvtool col N clean_dialog.csv | head
```

### Count how often each pony speaks

The assignment specifically asks you to use `grep`.

Example commands:

```bash
grep -c 'Twilight Sparkle' clean_dialog.csv
grep -c 'Rarity' clean_dialog.csv
grep -c 'Pinkie Pie' clean_dialog.csv
grep -c 'Rainbow Dash' clean_dialog.csv
grep -c 'Fluttershy' clean_dialog.csv
```

Record the results:

| Pony | Total line count |
|---|---:|
| Twilight Sparkle | **[FILL IN]** |
| Rarity | **[FILL IN]** |
| Pinkie Pie | **[FILL IN]** |
| Rainbow Dash | **[FILL IN]** |
| Fluttershy | **[FILL IN]** |

> Check a few matching rows with `grep` before trusting the counts. A simple text search can accidentally match a pony's name when it appears somewhere other than the speaker field.

Example:

```bash
grep 'Twilight Sparkle' clean_dialog.csv | head
```

---

### Calculate percentage of all spoken lines

Find the total number of spoken lines:

```bash
wc -l clean_dialog.csv
```

If the CSV has one header row:

```bash
expr $(wc -l < clean_dialog.csv) - 1
```

Percentage formula:

```text
percent_all_lines = (pony_line_count / total_spoken_lines) * 100
```

You can calculate each percentage with `awk`. Example:

```bash
awk 'BEGIN {printf "%.2f\n", (PONY_COUNT / TOTAL_LINES) * 100}'
```

Replace `PONY_COUNT` and `TOTAL_LINES` with your values.

Record the results:

| Pony | Total line count | Percent of all lines |
|---|---:|---:|
| Twilight Sparkle | **[FILL IN]** | **[FILL IN]%** |
| Rarity | **[FILL IN]** | **[FILL IN]%** |
| Pinkie Pie | **[FILL IN]** | **[FILL IN]%** |
| Rainbow Dash | **[FILL IN]** | **[FILL IN]%** |
| Fluttershy | **[FILL IN]** | **[FILL IN]%** |

---

## Line_percentages.csv

Create a second file called `Line_percentages.csv` with exactly these fields:

```csv
pony_name,total_line_count,percent_all_lines
Twilight Sparkle,[COUNT],[PERCENT]
Rarity,[COUNT],[PERCENT]
Pinkie Pie,[COUNT],[PERCENT]
Rainbow Dash,[COUNT],[PERCENT]
Fluttershy,[COUNT],[PERCENT]
```

You can create/edit it with:

```bash
nano Line_percentages.csv
```

---

## Task 5: Commit and push your work

Make sure your repository contains at least:

```text
explore.md
Line_percentages.csv
```

Then run:

```bash
git status
git add explore.md Line_percentages.csv
git commit -m "Complete Homework 4 dataset exploration"
git push origin main
```
