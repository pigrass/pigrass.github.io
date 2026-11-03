## 1. 场景与公式

这篇文章脱胎于上篇关于反向`TEXTSPLIT`函数的讨论,为了将复杂的`=TEXTJOIN("/", FALSE, BYROW(A1:B3, LAMBDA(r, TEXTJOIN(",", FALSE, r))))`函数,精简为`TEXTJOIN2D`这类简单的形式,我们使用了excel的自定义函数功能.但是随工作增加,自定义函数增加,如何管理备份就成了问题.因为excel目前不支持导出自定义名称函数.

## 2. ✅ 解决方案 - VBA函数批量导入自定义函数
### 2.1 完整代码 - 可维护结构版（直接复制可用）

> ⚠️ 使用前：VBE → 工具 → 引用 → 勾选 **Microsoft Scripting Runtime**（Dict 用）

```vba
'=========================================================
'  LAMBDA 函数库注入器
'  用法：在模块中维护 FunctionDefs 字典，调用 InjectAll 即可
'=========================================================

Option Explicit

'=========================================================
'  主入口：注入所有 LAMBDA 函数
'=========================================================
Sub InjectLambdaLib()

    Dim dict As Object
    Set dict = CreateFunctionDefs()

    Dim key As Variant
    Dim count As Long: count = 0

    For Each key In dict.Keys
        If InjectOne(CStr(key), CStr(dict(key))) Then
            count = count + 1
        End If
    Next key

    MsgBox "LAMBDA 函数库注入完成！" & vbCrLf & _
           "成功注入 " & count & " 个函数：" & vbCrLf & _
           JoinDictKeys(dict), vbInformation, "完成"

End Sub

'=========================================================
'  单个函数注入（核心逻辑）
'=========================================================
Private Function InjectOne(funcName As String, lambdaStr As String) As Boolean

    On Error GoTo ErrHandler

    ' 删除旧定义（如果存在）
    On Error Resume Next
    ActiveWorkbook.Names(funcName).Delete
    On Error GoTo ErrHandler

    ' 注入新定义
    ActiveWorkbook.Names.Add _
        Name:=funcName, _
        RefersTo:=lambdaStr

    InjectOne = True
    Exit Function

ErrHandler:
    MsgBox "注入失败：" & funcName & vbCrLf & _
           "错误：" & Err.Description, vbExclamation, "错误"
    InjectOne = False
End Function

'=========================================================
'  函数定义字典 —— 在这里添加你的 LAMBDA 函数
'=========================================================
Private Function CreateFunctionDefs() As Object

    Dim dict As Object
    Set dict = CreateObject("Scripting.Dictionary")

    '-----------------------------------------------------
    '  JOIN2D：二维数组合并为一维文本
    '  参数：array, col_delimiter, row_delimiter
    '  示例：=JOIN2D(A1:B3, ",", "/")
    '-----------------------------------------------------
    dict.Add "JoinRow", _
        "=LAMBDA(r,col_delimiter,TEXTJOIN(col_delimiter,FALSE,r))"

    dict.Add "JOIN2D", _
        "=LAMBDA(array,col_delimiter,row_delimiter," & _
        "TEXTJOIN(row_delimiter,FALSE,BYROW(array,LAMBDA(r,JoinRow(r,col_delimiter)))))"

    '-----------------------------------------------------
    '  SPLIT2D：一维文本拆分为二维数组（JOIN2D 的反向）
    '  参数：text, col_delimiter, row_delimiter
    '  示例：=SPLIT2D("1,A/2,B/3,C", ",", "/")
    '-----------------------------------------------------
    dict.Add "SPLIT2D", _
        "=LAMBDA(text,col_delimiter,row_delimiter," & _
        "TEXTSPLIT(text,col_delimiter,row_delimiter))"

    '-----------------------------------------------------
    '  JOIN2D_IGNORE：二维数组合并（忽略空单元格）
    '  参数：array, col_delimiter, row_delimiter
    '-----------------------------------------------------
    dict.Add "JoinRowIgnore", _
        "=LAMBDA(r,col_delimiter,TEXTJOIN(col_delimiter,TRUE,r))"

    dict.Add "JOIN2D_IGNORE", _
        "=LAMBDA(array,col_delimiter,row_delimiter," & _
        "TEXTJOIN(row_delimiter,TRUE,BYROW(array,LAMBDA(r,JoinRowIgnore(r,col_delimiter)))))"

    '-----------------------------------------------------
    '  FLATTEN2D：二维数组展平为一维数组（单列）
    '  参数：array
    '  示例：=FLATTEN2D(A1:B3)
    '-----------------------------------------------------
    dict.Add "FLATTEN2D", _
        "=LAMBDA(array,TOCOL(array,0))"

    '-----------------------------------------------------
    '  UNIQUE2D：二维数组去重
    '  参数：array
    '-----------------------------------------------------
    dict.Add "UNIQUE2D", _
        "=LAMBDA(array,UNIQUE(TOCOL(array,1)))"

    ' ★★★ 在这里继续添加新函数 ★★★
    ' dict.Add "函数名", "=LAMBDA(参数, 公式)"

    Set CreateFunctionDefs = dict
End Function

'=========================================================
'  辅助：拼接已注入的函数名列表
'=========================================================
Private Function JoinDictKeys(dict As Object) As String
    Dim key As Variant, result As String
    For Each key In dict.Keys
        result = result & "• " & CStr(key) & vbCrLf
    Next key
    JoinDictKeys = Left(result, Len(result) - 1)
End Function

'=========================================================
'  快捷：只注入 JOIN2D（单独调试用）
'=========================================================
Sub InjectJOIN2D_Only()
    Dim dict As Object
    Set dict = CreateObject("Scripting.Dictionary")

    dict.Add "JoinRow", _
        "=LAMBDA(r,col_delimiter,TEXTJOIN(col_delimiter,FALSE,r))"
    dict.Add "JOIN2D", _
        "=LAMBDA(array,col_delimiter,row_delimiter," & _
        "TEXTJOIN(row_delimiter,FALSE,BYROW(array,LAMBDA(r,JoinRow(r,col_delimiter)))))"

    InjectOne "JoinRow", dict("JoinRow")
    InjectOne "JOIN2D", dict("JOIN2D")

    MsgBox "JOIN2D 注入成功！", vbInformation
End Sub
```
---
### 2.2 使用方式

| 操作 | 步骤 |
| --- | --- |
| 注入全部函数 | 运行 `InjectLambdaLib` |
| 只注入 JOIN2D | 运行 `InjectJOIN2D_Only` |
| 添加新函数 | 在 `CreateFunctionDefs` 里加一行 `dict.Add` |
| 绑定按钮 | 把 `InjectLambdaLib` 放到快速访问工具栏 |

---

### 2.3 添加新函数的标准模板

```vba
' 1. 如果有内层辅助 LAMBDA，先加：
dict.Add "HelperName", _
    "=LAMBDA(参数, 公式)"

' 2. 再加主函数：
dict.Add "MYFUNCTION", _
    "=LAMBDA(参数1,参数2, 你的公式)"
```
### 2.4 已内置的函数一览

| 函数名 | 功能 | 示例 |
| --- | --- | --- |
| `JOIN2D` | 二维→一维文本（不忽略空值） | `=JOIN2D(A1:B3,",","/")` |
| `SPLIT2D` | 一维文本→二维数组 | `=SPLIT2D("1,A/2,B"," ",",","/")` |
| `JOIN2D_IGNORE` | 二维→一维文本（忽略空值） | `=JOIN2D_IGNORE(A1:B3,",","/")` |
| `FLATTEN2D` | 二维展平为一列 | `=FLATTEN2D(A1:B3)` |
| `UNIQUE2D` | 二维去重 | `=UNIQUE2D(A1:B3)` |

---

### 2.5 注意事项

1. **名称首字符不能是 **`_`（Excel 限制）
2. **内层辅助函数必须先于外层函数定义**（字典按顺序注入）
3. 文件必须是 `.xlsm`
4. 如果某个函数注入失败，其他函数不受影响（容错设计）

## 3. ❌ 尝试过的其他方案
### 3.1 维护一份保存了所有自定义函数的excel文档
这是一个相对简单的做法,其他人需要时把这份文档发给他就好,算不上是差的方案.拿这个模板做的新文件自带函数.
### 3.2 封装成excel加载宏(.xlam)
这是当时跟AI讨论时,AI给出的第1个方案,做法如下
#### 3.2.1 制作函数库文件
1. 新建一个空白 Excel
2. 打开 **公式 → 名称管理器 → 新建**
3. 建好你的 `JOIN2D`：

```excel
名称：JOIN2D
引用位置：
=LAMBDA(array, col_delimiter, row_delimiter,
    TEXTJOIN(row_delimiter, FALSE,
        BYROW(array, LAMBDA(r, TEXTJOIN(col_delimiter, FALSE, r)))
    )
)
```

4. 文件 → 另存为
类型选：**Excel 加载项 (\*****.xlam)**
文件名：`MyLambdaLib.xlam`
路径用默认 AddIns 文件夹（或自己记一下）

#### 3.2.2 安装加载宏（只需一次）

1. 文件 → 选项 → 加载项
2. 底部“管理：Excel 加载项” → 转到
3. 浏览 → 选中 `MyLambdaLib.xlam` → 勾选启用

#### 3.3.3 导入加载项后,使用`JOIN2D`函数,单元格报错`#NAME?`,问题在哪?
##### 根本原因:
> **LAMBDA 自定义名称默认是“工作簿级名称”**
> 放在 `.xlam` 里，它属于「加载宏工作簿自己」，不会自动注入到「当前新建工作簿」的名称空间。
> 所以新文档直接写 `=JOIN2D(...)` → Excel 在当前工作簿找不到这个名字 → `#NAME?`
---

##### 为什么加载宏没生效（3 个常见坑）

坑 1：以为 xlam 勾选后，函数会“全局注册”

>实际上：
>- xlam 里的 LAMBDA 只在 **xlam 自己内部** 可见
>- 新工作簿要调用，必须显式带文件名前缀，或把名字注入新簿

坑 2：调用方式不对

>如果加载宏文件叫 `MyLambdaLib.xlam`，新文档里应该写：
```excel
=MyLambdaLib.xlam!JOIN2D(A1:B3, ",", "/")
```
>（注意：文件名别带空格，前缀要和加载宏文件名一致）

✅ 这样是能用的，但体验很差，自动补全也没有。

坑 3：xlam 是“另存为”出来的，名称没带过去

>正确做法：
>**先在普通 xlsx 里建好名称管理器 → 测试通过 → 另存为 xlam**
>（不是先存 xlam 再打开编辑，容易丢定义）



## 4. 核心总结

###  方案 A：VBA 一键把 LAMBDA 注入当前工作簿（最推荐）

在 `PERSONAL.xlsb` 里放上述宏：

✅ 新文档立即可用
✅ 不依赖加载宏前缀
✅ 适合常用 VBA 的场景

###  方案 B：用“模板文件 .xltx”（适合固定业务）

把 JOIN2D 建好 → 另存为 **Excel 模板**
以后“新建”都从模板建，天然带函数。

###  方案 C：接受带前缀调用（最稳，不改架构）

加载宏名：`MyLambdaLib.xlam`

✅ 优点：零风险
❌ 缺点：名字长、不优雅

## 5. 备注
因为加载宏的做法一开始即报错,所以即使后来AI解释应该如何正确调用,我后面也没有继续尝试.目前是使用第2节的可维护结构的VBA宏方案