# 第 2 章 · 表格批处理 · 章测

## 选择题

```quiz
type: choice
q: openpyxl 中 A1 单元格的行列号是？
options:
- (0, 0)
- (1, 1)
- (1, 0)
- (0, 1)
answer: 1
explain: 行列都从 1 开始
```

```quiz
type: choice
q: 获取工作表最大行数用？
options:
- len(ws)
- ws.max_row
- ws.rows
- ws.count
answer: 1
explain: max_row 是最大行号
```

```quiz
type: choice
q: 往工作表追加一行最方便的方法是？
options:
- ws.write(...)
- ws.append(row)
- ws.push(...)
- print(...)
answer: 1
explain: append 追加一行
```

```quiz
type: choice
q: 合并多张结构相同的表时，表头应该怎么处理？
options:
- 每张都写
- 只写一次，其余跳过
- 完全不写
- 写到末尾
answer: 1
explain: 避免表头污染数据
```

```quiz
type: choice
q: 对可能为 None 的数量字段，正确的保护写法是？
options:
- 直接相加
- qty = int(qty or 0)
- qty = str(qty)
- 忽略
answer: 1
explain: or 0 处理 None
```

## 动手题

```quiz
type: function
q: 写一个函数 calc_amounts(rows)，rows 是列表，每个元素是 [商品, 数量, 单价]。返回一个新的列表，每个元素是 [商品, 数量, 单价, 金额]，金额=数量×单价。空列表返回空列表。
func: calc_amounts
starter: |
  def calc_amounts(rows):
      return []
cases: |
  [["键盘", 3, 200]] -> [["键盘", 3, 200, 600]]
  [["a", 1, 10], ["b", 2, 5]] -> [["a", 1, 10, 10], ["b", 2, 5, 10]]
hint: 遍历并拼接金额列
explain: 写表前构造计算列的纯逻辑练习
```

```quiz
type: local
q: 写一个脚本，读取目录下所有 门店*.xlsx（结构：商品、数量、单价），按商品汇总总数量和总金额，输出 汇总.xlsx，表头为「商品/总数量/总金额」，末尾追加一行「合计」。
starter: |
  from openpyxl import load_workbook, Workbook
  from pathlib import Path
  from collections import defaultdict

  def build_report(files, out="汇总.xlsx"):
      # 在这里写
      pass
checklist:
- 用 load_workbook 读取每个文件
- 用 defaultdict 按商品汇总总数量和总金额
- 先打印「商品 -> 总数量, 总金额」的汇总计划，确认后再执行
- 输出表含表头、数据行和合计行
hint: 先预览再执行，避免改错
explain: 综合应用读、算、写三段式
```

## 小项目

做一个「月度报表生成器」：读取目录下所有 `.xlsx` 明细表（日期/商品/数量/单价），按商品分组统计总数量与总金额，输出一个格式整齐的 `月度报表.xlsx`。要求：
1. 表头加粗
2. 每行金额列用公式计算（`=数量*单价`）
3. 末尾加合计行
4. 先打印汇总预览，确认后再写文件
