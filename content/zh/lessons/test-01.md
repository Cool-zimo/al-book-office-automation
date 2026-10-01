# 第 1 章 · 文件批处理 · 章测

## 选择题

```quiz
type: choice
q: Path(".").iterdir() 与 Path(".").rglob("*.pdf") 的区别是？
options:
- 前者递归，后者不递归
- 前者只遍历一层，后者递归
- 两者完全一样
- 两者都不能遍历
answer: 1
explain: iterdir 一层，rglob 递归
```

```quiz
type: choice
q: str.rpartition("_") 对 "报告_终版_2024.pdf" 返回什么？
options:
- ("报告", "_", "终版_2024.pdf")
- ("报告_终版", "_", "2024.pdf")
- ("", "_", "报告_终版_2024.pdf")
- 报错
answer: 1
explain: rpartition 从右边切一刀
```

```quiz
type: choice
q: shutil.move 的目标目录不存在，应该先做什么？
options:
- 直接 move
- target_dir.mkdir(parents=True, exist_ok=True)
- os.remove(target_dir)
- 什么都不做
answer: 1
explain: 先创建目标目录
```

```quiz
type: choice
q: Path.suffix 对 "报告.pdf" 返回什么？
options:
- "报告"
- ".pdf"
- "pdf"
- ""
answer: 1
explain: suffix 含点
```

```quiz
type: choice
q: 整理下载文件夹时，为什么要 if not p.is_file(): continue？
options:
- 加快速度
- 避免把子目录当成文件移动
- 让代码更短
- 没什么用
answer: 1
explain: 目录不是文件，要排除
```

## 动手题

```quiz
type: function
q: 写一个函数 safe_rename(files)，files 是文件名列表，每个形如 "报告_2024.pdf"。返回新名字列表，格式为 "2024-报告.pdf"（把下划线前后的两部分交换，保留 .pdf 后缀）。
func: safe_rename
starter: |
  def safe_rename(files):
      return []
cases: |
  ["报告_2024.pdf"] -> ["2024-报告.pdf"]
  ["账单_2023.pdf", "名单_2022.pdf"] -> ["2023-账单.pdf", "2022-名单.pdf"]
hint: 先去后缀，再按 _ 分割，交换后拼回去
explain: 重命名的纯逻辑练习
```

```quiz
type: local
q: 写一个脚本，把指定目录下所有 .log 文件按修改年份归类到 年份/ 子目录，文件名保持不变。先打印「文件 -> 目标路径」的计划，确认后再执行。
starter: |
  from pathlib import Path
  import shutil
  from datetime import datetime

  def organize_by_year(root):
      # 在这里写
      pass
checklist:
- 用 Path.iterdir() 遍历目录
- 只处理 .log 后缀的文件
- 用修改时间 st_mtime 的年份作为目标子目录
- 先打印「原名 -> 目标路径」的计划，确认后再执行
hint: 先预览再执行，避免改错
explain: 综合应用归类与日期
```

## 小项目

把 `~/Downloads` 里所有文件按「图片 / 文档 / 压缩包 / 其他」四类整理到对应子目录。要求：
1. 先用一个 `RULES` 字典定义后缀映射
2. 先 `dry_run=True` 打印计划，确认无误再执行
3. 遇到目标已存在的文件要跳过并打印提示
4. 最后打印一句汇总：共移动了多少个文件
