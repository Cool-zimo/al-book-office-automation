# Chapter 1 · Batch File Processing · Chapter Test

## Multiple Choice

```quiz
type: choice
q: What is the difference between Path(".").iterdir() and Path(".").rglob("*.pdf")?
options:
- The former recurses, the latter does not
- The former is one level, the latter recurses
- They are identical
- Neither can traverse
answer: 1
explain: iterdir is one level, rglob is recursive
```

```quiz
type: choice
q: What does str.rpartition("_") return for "report_final_2024.pdf"?
options:
- ("report", "_", "final_2024.pdf")
- ("report_final", "_", "2024.pdf")
- ("", "_", "report_final_2024.pdf")
- raises an error
answer: 1
explain: rpartition cuts from the right
```

```quiz
type: choice
q: shutil.move's destination directory does not exist. What should you do first?
options:
- move directly
- target_dir.mkdir(parents=True, exist_ok=True)
- os.remove(target_dir)
- nothing
answer: 1
explain: create the destination directory first
```

```quiz
type: choice
q: What does Path.suffix return for "report.pdf"?
options:
- "report"
- ".pdf"
- "pdf"
- ""
answer: 1
explain: suffix includes the dot
```

```quiz
type: choice
q: When organizing Downloads, why `if not p.is_file(): continue`?
options:
- to speed things up
- to avoid moving subdirectories as if they were files
- to make the code shorter
- it does nothing
answer: 1
explain: directories are not files, exclude them
```

## Hands-on

```quiz
type: function
q: Write a function safe_rename(files) where files is a list of filenames each like "report_2024.pdf". Return the new names in the format "2024-report.pdf" (swap the two parts around the underscore, keep the .pdf suffix).
func: safe_rename
starter: |
  def safe_rename(files):
      return []
cases: |
  ["report_2024.pdf"] -> ["2024-report.pdf"]
  ["bill_2023.pdf", "roster_2022.pdf"] -> ["2023-bill.pdf", "2022-roster.pdf"]
hint: strip the suffix, split on _, swap, reassemble
explain: a pure-logic renaming exercise
```

```quiz
type: local
q: Write a script that sorts every .log file in a given directory into a subfolder named by the year of its modification time (e.g. 2024/), keeping the filename unchanged. Print the "file -> destination path" plan first, then execute after confirmation.
starter: |
  from pathlib import Path
  import shutil
  from datetime import datetime

  def organize_by_year(root):
      # write your code here
      pass
checklist:
- Use Path.iterdir() to traverse the directory
- Process only .log files
- Use the year from the modification time st_mtime as the destination subfolder
- Print the "old name -> destination path" plan first, execute after confirming
hint: preview then execute to avoid mistakes
explain: combines sorting and date handling
```

## Mini Project

Sort every file in `~/Downloads` into four categories — `Images/`, `Docs/`, `Archives/`, `Other/` — based on extension. Requirements:
1. Define the extension mapping in a `RULES` dict
2. First run with `dry_run=True` and print the plan; only execute once confirmed
3. If a destination already exists, skip it and print a notice
4. Print a summary line at the end: how many files were moved
