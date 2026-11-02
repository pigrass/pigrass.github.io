## 1. 场景与公式

EXCEL函数,将3行2列的内容合并,行与行之间用"/"分隔,列与列之间用","分隔
|   | A | B |
| --- | --- | --- |
| 1 | 1 | A |
| 2 | 2 | B |
| 3 | 3 | C |

```EXCEL
=TEXTJOIN("/", FALSE, BYROW(A1:B3, LAMBDA(r, TEXTJOIN(",", FALSE, r))))
```
#### 结果
```
1,A/2,B/3,C
```
#### 原理说明
1. `TEXTJOIN(",", FALSE, r)`
→ 将每一行的两列用 **逗号 **`,` 合并
2. `BYROW(...)`
→ 对每一行执行上面的操作
3. **外层 **`TEXTJOIN("/", FALSE, ...)`
→ 把每行结果再用 **斜杠 **`/` 连接起来

## 2. ❌ 有没有像`TEXTSPLIT`那样简单的函数可以合并数组
- `TEXTSPLIT`：**一维文本 → 二维数组**
- Excel 目前**没有**类似 `TEXTJOIN2D(区域, 列分隔符, 行分隔符)` 的原生函数
微软其实**完全可以做**一个这样的函数，但目前还没有.目前版本的office你需要借助`BYROW/LAMBDA`这类非常用函数,如果用旧版office,你甚至需要借助辅助列或其他更复杂的公式

## 3. ✅ 理想中的“对称写法”（如果 Excel 支持）
```excel
=TEXTJOIN2D(A1:B3, ",", "/")
```

但目前只能靠 `TEXTJOIN + BYROW` 模拟。

## 4. 解决方案与建议 - 自定义LAMBDA函数
### ✅ 自定义 LAMBDA 函数：`JOIN2D`
#### 在【名称管理器】中新建

**名称：**

```
JOIN2D
```

**引用位置：**

```excel
=LAMBDA(array, col_delimiter, row_delimiter,
    TEXTJOIN(
        row_delimiter,
        FALSE,
        BYROW(array, LAMBDA(r,
            TEXTJOIN(col_delimiter, FALSE, r)
        ))
    )
)
```

### ✅ 参数说明
| 参数 | 含义 |
| --- | --- |
| `array` | 二维区域或数组（如 `A1:B3`） |
| `col_delimiter` | 列之间的分隔符（如 `,`） |
| `row_delimiter` | 行之间的分隔符（如 `/`） |

> ✅ 两个 `TEXTJOIN` 的 **ignore\_****empty 参数均为 FALSE**
> ✅ 空单元格会保留为连续分隔符

### ✅ 使用示例

#### 数据（A1:B3）

|   | A | B |
| --- | --- | --- |
| 1 | 1 | A |
| 2 | 2 | B |
| 3 | 3 | C |

#### 公式

```excel
=JOIN2D(A1:B3, ",", "/")
```

#### 结果

```
1,A/2,B/3,C
```

### ✅ 含空单元格示例（体现 FALSE 的作用）

|   | A | B |
| --- | --- | --- |
| 1 | 1 |   |
| 2 |   | B |
| 3 | 3 | C |

#### 结果

```
1,/,B/3,C
```

（空单元格不会被忽略）

### ✅ 与 TEXTSPLIT 的“对称关系”

```excel
=TEXTSPLIT(A4, ",", "/")
```

```excel
=JOIN2D(A1:B3, ",", "/")
```

✅ 逻辑上完全对称
✅ 非常适合做 **合并 ↔ 拆分** 的数据处理

### ✅ 适用环境

- ✅ Excel 365 / Excel 2021+
- ✅ WPS 表格（支持 LAMBDA）
- ❌ Excel 2019 及更早版本

## 5. 核心总结

借助自定义`LAMBDA`函数,我们可以将常用的&比较复杂的嵌套函数,精简为简单的函数名.
但是当你工作久了,自定义函数多了,不止需要用在当前excel文档,其他文档也需要借用时,office又没有自定义`LAMBDA`函数批量导入导出功能,难道我们每次新开文档都一个个函数新建进去吗?
下次介绍VBA脚本批量导入自定义`LAMBDA`函数!