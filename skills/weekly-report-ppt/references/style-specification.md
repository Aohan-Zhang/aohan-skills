# 个人周报 PPT 大纲模板设计规范 (Style Specification)

> 日期: 2026-06-25
> 作者: ah

## 全局样式规范

### 配色方案
核心三色：奶油底 + 珊瑚强调 + 深墨文字，辅以深色表面与强奶油底制造起伏节奏。

#### 表面色 (Surface)
| 用途 | 色值 | 说明 |
|---|---|---|
| 页面背景（Canvas） | #FAF9F5 | 暖奶油色，不是纯白。风格的决定性选择 |
| 柔和区域（Surface Soft） | #F5F0E8 | 区段分隔、柔和条带背景 |
| 卡片背景（Surface Card） | #EFE9DE | 比画布深一级的暖奶油，用于默认卡片底色 |
| 强调奶油（Surface Cream Strong） | #E8E0D2 | 最深奶油变体，用于过渡节奏页、选中态标签、强调区域 |
| 深色表面（Surface Dark） | #181715 | 深色，用于下周计划页底色、过渡节奏页或强调页 |
| 深色抬升（Surface Dark Elevated） | #252320 | 深色表面内的抬升卡片 |
| 深色柔和（Surface Dark Soft） | #1F1E1B | 略浅深色，用于深色区域内的代码块/嵌套区域 |

#### 文字色 (Text)
| 用途 | 色值 | 说明 |
|---|---|---|
| 主文字（Ink） | #141413 | 所有标题和主要文字，暖调深墨 |
| 强调文字（Body Strong） | #252523 | 段落强调、引导文字 |
| 正文（Body） | #3D3D3A | 默认正文色 |
| 辅助文字（Muted） | #6C6A64 | 小标题、次要信息 |
| 淡化文字（Muted Soft） | #8E8B82 | 注释、极次要信息 |
| 深色表面文字（On Dark） | #FAF9F5 | 深色表面上的文字，呼应画布色调 |
| 深色表面次要文字（On Dark Soft） | #A09D96 | 深色表面上的次要文字 |

#### 品牌与强调色 (Brand & Accent)
| 用途 | 色值 | 说明 |
|---|---|---|
| 珊瑚强调色（Primary） | #CC785C | 主题色，稀缺使用——重点卡片左边框、装饰线、进度指示 |
| 辅助色 Teal | #5DB8A6 | 进行中/活跃状态指示，少量使用 |
| 辅助色 Amber | #E8A55A | 分类标签、行内高亮 |
| 成功色 | #5DB872 | 完成状态 |
| 错误色（Error） | #C64545 | 错误/校验失败 |
| 珊瑚上文字（On Primary） | #FFFFFF | 珊瑚色背景上的文字 |

#### 边框与分隔线
| 用途 | 色值 | 说明 |
|---|---|---|
| Hairline | #E6DFD8 | 卡片边框、区域分隔线，与珊瑚禁用态同色——边框是抬升而非墨线 |
| Hairline Soft | #EBE6DF | 同一区域内的极淡分隔线 |

### 字体规范
衬线 + 无衬线双轨制——标题用衬线体营造编辑感，正文用无衬线保证可读性。

| 层级 | 字号(Pt) | 字重 | 行高 | 字间距 | 用途 | 字体 |
|---|---|---|---|---|---|---|
| 封面姓名 | 30-36pt | 400 | 1.1 | -0.4pt | 封面主标题 | 衬线体 |
| 封面日期 | 15-18pt | 400 | 1.4 | 0 | 封面副标题 | 无衬线体 |
| 页标题 | 21-24pt | 400 | 1.2 | -0.2pt | 每页项目名/维度名 | 衬线体 |
| 卡片标题 | 14-15pt | 500 | 1.4 | 0 | 卡片内第一行 | 无衬线体 |
| 卡片简述 | 11-12pt | 400 | 1.55 | 0 | 卡片内第二行 | 无衬线体 |
| 辅助信息 | 9-11pt | 400 | 1.4 | 0 | 进度、日期、注释 | 无衬线体 |

* 字体选择：英文衬线使用 Cormorant Garamond / EB Garamond；中文衬线使用思源宋体。英文无衬线使用 Inter；中文无衬线使用思源黑体 / 微软雅黑。
* 关键原则：衬线标题必须使用 weight 400 (Regular) 且配合负字间距（-0.2pt 到 -0.4pt），以体现暖意编辑风格。

### 间距体系 (cm)
- xxs: 0.1cm | xs: 0.2cm | sm: 0.3cm | md: 0.4cm (标准/卡片间距) | lg: 0.6cm | xl: 0.8cm (卡片内边距) | xxl: 1.2cm | section: 2.5cm

### 圆角体系 (cm)
- xs: 0.1cm | sm: 0.15cm | md: 0.2cm | lg: 0.3cm (内容卡片圆角) | xl: 0.4cm | pill: 全圆

---

## 页面结构与排版

### 1. 封面页
- **背景**：Canvas (#FAF9F5)
- **排版**：垂直居中，标题主文字衬线体 33pt/400/-0.4pt #141413，日期范围无衬线 18pt/400 #6C6A64，二者间距 md (0.4cm)。

### 2. 开发产出页（每项目一页）
- **页标题**：项目名称（如"[项目名称]"），衬线体 22pt/400/-0.2pt，下方加珊瑚色装饰线（1.5pt高/1.0cm宽 #CC785C）。右侧对齐进度指示。
- **内容卡片**：2-3列网格，间距 md (0.4cm)，内边距 xl (0.8cm)，圆角 lg (0.3cm)。
  - **原子状态支持 (Atomic States)**：大纲中不硬编码状态 Emoji，而是使用 `"state": "success" | "pending" | "starred"` 属性驱动自动装配：
    - `"state": "success"` (已完成/成功)：对应 Emoji `✅`。使用默认卡片：暖奶油底 #EFE9DE + Hairline 边框 (0.75pt #E6DFD8)。
    - `"state": "pending"` (进行中/等待)：对应 Emoji `⏳`。使用进行中卡片：Canvas (#FAF9F5) + Teal 虚线边框 (0.75pt dashed #5DB8A6)。
    - `"state": "starred"` (重点关注)：对应 Emoji `⭐`。使用重点卡片：Canvas (#FAF9F5) + 珊瑚色左边框 (2pt #CC785C)。
- **限制规则**：单页内容卡片数 $\le 6$。若超出该限制，必须应用“自动分页原则”拆分为两页，例如第一页标题为“项目名称 (1/2)”，第二页标题为“项目名称 (2/2)”。

### 3. 动态维度页与过渡节奏页
- **过渡节奏页（Rhythm Slide）**：
  - **触发条件**：当 PPT 总页数（含封面和计划页）超过 5 页时强制触发。
  - **排版**：在第 3 或第 4 页位置插入一页过渡页，使用 **深色表面** (Surface Dark, #181715) 或 **强调奶油色** (Surface Cream Strong, #E8E0D2) 作为背景，大标题居中衬线体 22pt，提供一个内容喘息点。
- **动态维度页**：根据本周实际工作内容提炼分类（如“调研发现”、“问题排查”）。条目少（2-3条）用列表，多（4条以上）用内容卡片网格。

### 4. 下周计划页 (next_steps)
- **背景**：Surface Dark (#181715)
- **文字**：On Dark (#FAF9F5)，次要文字 On Dark Soft (#A09D96)
- **自适应规划布局**：通过 `"alignment": "vertical" | "horizontal"` 参数控制排版布局，自适应内容长短与数量：
  - **纵向排序 (vertical，默认)**：项目小标题与列表纵向依次堆叠。项目小标题无衬线 12pt/500，列表 `→` 开头无衬线 11pt/400，段间距 lg (0.6cm)。
  - **横向排序 (horizontal)**：当有 2-3 个独立项目且条目较简短时使用，将项目按列横向排列（分栏布局）。分栏间距为 lg (0.6cm)，每栏内边距为 xl (0.8cm)。
- 页标题下方的珊瑚装饰线依然保留。

---

## 标准组件库规范 (Standard Components Library)

为了沉淀多布局组件，在 HTML 与 JSON 中支持以下标准组件的定义：

### 1. 通栏页脚块 (Full-Width Footer Bar)
- **用途**：每页底部固定展示汇报人、密级和页码。
- **CSS 表现**：
  ```css
  .footer-bar {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 13.333in; /* 16:9 标准 PPT 宽度 */
    height: 0.6in;
    background-color: #FAF9F5; /* Canvas 同底，可自适应 */
    border-top: 0.75pt solid #E6DFD8; /* Hairline */
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 0.8in;
    box-sizing: border-box;
  }
  .footer-bar.dark {
    background-color: #181715;
    border-top: 0.75pt solid #252320;
  }
  .footer-text {
    font-family: 'Inter', sans-serif;
    font-size: 9pt;
    color: #8E8B82;
  }
  .footer-text.dark {
    color: #A09D96;
  }
  ```
- **JSON 元数据声明**：
  ```json
  "footer": {
    "show": true,
    "theme": "default", // default (奶油底) | dark (深色底)
    "left_text": "张三 | 周报汇报",
    "right_text": "CONFIDENTIAL",
    "page_number": true
  }
  ```

### 2. 状态标签 (Status Tag)
- **用途**：在标题旁或卡片角展示的胶囊状状态标签。
- **CSS 表现**：
  ```css
  .status-tag {
    display: inline-flex;
    align-items: center;
    padding: 0.1cm 0.3cm;
    border-radius: 9999px; /* pill 圆角 */
    font-family: 'Inter', sans-serif;
    font-size: 9pt;
    font-weight: 500;
  }
  .status-tag.success {
    background-color: #FAF9F5;
    border: 0.75pt solid #5DB872;
    color: #5DB872;
  }
  .status-tag.pending {
    background-color: #FAF9F5;
    border: 0.75pt solid #5DB8A6;
    color: #5DB8A6;
  }
  ```
- **JSON 元数据声明**：
  ```json
  "status_tag": {
    "text": "已发布",
    "state": "success" // success | pending | error
  }
  ```
