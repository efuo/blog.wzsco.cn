---
title: Solitude 绘图：Mermaid
tags:
  - Solitude
  - Mermaid
categories:
  - [ 我的项目,Solitude ]
abbrlink: 79c5646c
date: 2024-03-02 00:00:00
cover: https://p.wzsco.top/9c134d5a943d998f13d5a7d6f24136bf.png/cover
---

## Mermaid

Mermaid 是一个用于绘制流程图、时序图、甘特图的工具，它使用简单的文本语法来描述图表，然后将其转换为图形。

[Mermaid 官网](https://mermaid.js.org/)

[Mermaid 中文网](https://mermaid.nodejs.cn/)

## 流程图

```markdown
{% mermaid %}
graph TD
    A[方形] -->|实线| B(圆角)
    B --> C{条件}
    C -->|a| D[结果1]
    C -->|b| E[结果2]
{% endmermaid %}
```

{% mermaid %}
graph TD
    A[方形] -->|实线| B(圆角)
    B --> C{条件}
    C -->|a| D[结果1]
    C -->|b| E[结果2]
{% endmermaid %}

## 时序图

```markdown
{% mermaid %}
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail...
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
{% endmermaid %}
```

{% mermaid %}
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail...
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
{% endmermaid %}

## 甘特图

```markdown
{% mermaid %}
gantt
    title 甘特图
    dateFormat  YYYY-MM-DD
    section 项目A
    任务1: 2014-01-01, 30d
    任务2: 2014-01-12, 30d
    section 项目B
    任务3: 2014-01-02, 30d
    任务4: 2014-01-14, 30d
{% endmermaid %}
```

{% mermaid %}
gantt
    title 甘特图
    dateFormat  YYYY-MM-DD
    section 项目A
    任务1: 2014-01-01, 30d
    任务2: 2014-01-12, 30d
    section 项目B
    任务3: 2014-01-02, 30d
    任务4: 2014-01-14, 30d
{% endmermaid %}

## 类图

```markdown
{% mermaid %}
classDiagram
    Class01 <|-- AveryLongClass : Cool
    Class03 *-- Class04
    Class05 o-- Class06
    Class07 .. Class08
    Class09 --> C2 : Where am i?
    Class09 --* C3
    Class09 --|> Class07
    Class07 : equals()
    Class07 : Object[] elementData
    Class01 : size()
    Class01 : int chimp
    Class01 : int gorilla
    Class08 <--> C2: Cool label
{% endmermaid %}
```

{% mermaid %}
classDiagram
    Class01 <|-- AveryLongClass : Cool
    Class03 *-- Class04
    Class05 o-- Class06
    Class07 .. Class08
    Class09 --> C2 : Where am i?
    Class09 --* C3
    Class09 --|> Class07
    Class07 : equals()
    Class07 : Object[] elementData
    Class01 : size()
    Class01 : int chimp
    Class01 : int gorilla
    Class08 <--> C2: Cool label
{% endmermaid %}

## 状态图

```markdown
{% mermaid %}
stateDiagram-v2
    [*] --> Still
    Still --> [*]
    Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]
{% endmermaid %}
```

{% mermaid %}
stateDiagram-v2
    [*] --> Still
    Still --> [*]
    Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]
{% endmermaid %}

## 饼图

```markdown
{% mermaid %}
pie
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
{% endmermaid %}
```

{% mermaid %}
pie
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
{% endmermaid %}

## ER 图

```markdown
{% mermaid %}
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
{% endmermaid %}
```

{% mermaid %}
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
{% endmermaid %}

{% note info %}
Mermaid 支持的图表类型非常丰富，可以满足大部分的绘图需求。
{% endnote %}