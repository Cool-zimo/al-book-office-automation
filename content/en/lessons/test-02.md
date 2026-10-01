# Chapter 2 · Batch Spreadsheet Processing · Chapter Test

## Multiple Choice

```quiz
type: choice
q: In openpyxl, what are the row and column of cell A1?
options:
- (0, 0)
- (1, 1)
- (1, 0)
- (0, 1)
answer: 1
explain: rows and columns are 1-based
```

```quiz
type: choice
q: How do you get the maximum row number of a worksheet?
options:
- len(ws)
- ws.max_row
- ws.rows
- ws.count
answer: 1
explain: max_row is the maximum row number
```

```quiz
type: choice
q: The easiest way to append a row to a worksheet is?
options:
- ws.write(...)
- ws.append(row)
- ws.push(...)
- print(...)
answer: 1
explain: append adds a row
```

```quiz
type: choice
q: When merging sheets with the same structure, how should the header be handled?
options:
- Write it for every sheet
- Write it once, skip the rest
- Don't write it at all
- Write it at the end
answer: 1
explain: avoid header pollution
```

```quiz
type: choice
q: For a possibly-None quantity field, the correct guard is?
options:
- add directly
- qty = int(qty or 0)
- qty = str(qty)
- ignore
answer: 1
explain: or 0 handles None
```

## Hands-on

```quiz
type: function
q: Write a function calc_amounts(rows) where rows is a list, each element [item, qty, price]. Return a new list where each element is [item, qty, price, amount], with amount = qty * price. Empty list returns an empty list.
func: calc_amounts
starter: |
  def calc_amounts(rows):
      return []
cases: |
  [["keyboard", 3, 200]] -> [["keyboard", 3, 200, 600]]
  [["a", 1, 10], ["b", 2, 5]] -> [["a", 1, 10, 10], ["b", 2, 5, 10]]
hint: iterate and append the amount column
explain: pure-logic practice for building a computed column before writing
```

```quiz
type: local
q: Write a script that reads every store*.xlsx in a directory (structure: item, qty, price), aggregates total qty and total amount per item, and outputs summary.xlsx with columns "Item/Total Qty/Total Amount", ending with a "Total" row.
starter: |
  from openpyxl import load_workbook, Workbook
  from pathlib import Path
  from collections import defaultdict

  def build_report(files, out="summary.xlsx"):
      # write your code here
      pass
checklist:
- Use load_workbook to read each file
- Use defaultdict to aggregate total qty and amount per item
- Print the "item -> total_qty, total_amount" summary plan first, execute after confirming
- Output includes header, data rows, and a total row
hint: preview then execute to avoid mistakes
explain: combines reading, computing, and writing
```

## Mini Project

Build a "monthly report generator": read every `.xlsx` detail sheet in a directory (date/item/qty/price), group by item and compute total qty and total amount, output a tidy `monthly_report.xlsx`. Requirements:
1. Bold the header row
2. Use a formula for the amount column (`=qty*price`)
3. Add a grand-total row at the end
4. Print a summary preview first, then write the file after confirming
