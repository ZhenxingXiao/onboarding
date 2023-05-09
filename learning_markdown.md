### 1.1 标题

```
# 一级标题
## 二级标题
### 三级标题
```

### 1.2 字体

```
**加粗**
*斜体*
***斜体加粗***
~~删除线~~
```

### 1.3 引用

```
> 引用内容
```

### 1.4 分割线

```
---
```

### 1.5 图片

```
![图片alt](图片地址 ''图片title'')
```

### 1.6 超链接

```
[超链接名](超链接地址 "超链接title")
```

### 1.7 列表

```
- 列表内容
+ 列表内容
* 列表内容
```

### 1.8 表格

```
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容
```

### 1.9 代码

```
`代码内容`
```

### 1.10* 流程图

```
graph TD
A[方形] -->B(圆角)
    B --> C{条件a}
    C -->|a=1| D[结果1]
    C -->|a=2| E[结果2]
    F[横向流程图]
```

### 1.11* 序列图

```
sequenceDiagram
    participant 张三
    participant 李四
    张三->王五: 王五你好吗？
    loop 健康检查
        王五->王五: 与疾病战斗
    end
    Note right of 王五: 合理 食物 <br/>看医生...
    李四-->>张三: 很好!
    王五->李四: 你怎么样?
```

### 1.12* 甘特图

```
gantt
    dateFormat YYYY-MM-DD
    title 产品计划
    section 初期阶段
    需求:done,des1, 2014-01-06,2014-01-08
    原型:active,des2, 2014-01-09, 3d
    UI设计:des3, after des2, 5d
    未来任务:des4, after des3, 5d
```

### 1.13* 数学公式

```
$$
f(x) = \int_{-\infty}^\infty
    \hat f(\xi)\,e^{2 \pi i \xi x}
    \,d\xi
$$
```

### 1.14* 时序图

```
sequenceDiagram
    loop every day
        Alice->>John: Hello John, how are you?
        John-->>Alice: Great!
    end
```