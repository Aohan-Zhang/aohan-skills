---
name: weekly-report-ppt
description: Generates warm-editorial weekly report PPT outlines from work records, managing surface-rhythm transitions and handling optional git-archaeology checks.
---

# Weekly Report PPT Skill

## 主导词 (Leading Words)

* **编辑风 (warm-editorial)**：视觉精髓为暖奶油底、墨黑文字与极克制的珊瑚强调色。排版上依靠 Regular 字重的衬线页标题与无衬线正文的双轨混排，并通过负字间距增强精细感。具体参数（色值、字号、字距等）均从单一源 [style-specification.md](file:///Users/aohan/aohan_dev/skills-private/skills/weekly-report-ppt/references/style-specification.md) 读取。
* **节奏交替 (surface-rhythm)**：页面在“奶油画布、内容卡片、深色表面”三种表面模式间的交替过渡。**新规**：若 PPT 总页数超 5 页，必须在中间插入至少 1 页 `Surface Dark`（深色表面）或 `Surface Cream Strong` 作为“过渡节奏页”，且尾页必须是深色表面，以明暗起伏的节奏感完成汇报。
* **代码考古 (git-archaeology)**：当用户输入过于简短（少于 15 字）或含糊时，**必须先以 Question 形式向用户询问是否允许扫描仓库**。若获得授权，则通过分析最近 7 天的个人 Git 提交记录及本周代码变动，挖掘具体修改的模块和技术要点，主动还原技术细节。

---

## 依赖规范与参考 (Context Pointers)

* **必须装载样式源**：在开始执行步骤前，你**必须**加载并读取 [style-specification.md](file:///Users/aohan/aohan_dev/skills-private/skills/weekly-report-ppt/references/style-specification.md) 以获取最新的配色、字号、间距与圆角 Token 定义。
* **必须参考大纲格式**：在输出任何大纲 Markdown 文本前，你**必须**读取并参考 [weekly-report-outline-example.md](file:///Users/aohan/aohan_dev/skills-private/skills/weekly-report-ppt/examples/weekly-report-outline-example.md) 以精确复制其页面层级划分、`>` 排版提示的编写格式以及结构化 JSON 注释块。
* **pptx 技能来源**：本地如缺少 `pptx` 技能，可参考外部源 [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) 了解其集成与交互设计。

---

## 执行步骤 (Steps)

### 0. 依赖与环境校验 (Pre-flight Verification)
执行前必须进行以下两项环境与依赖校验：
1. **Git 环境检查**：检查当前目录是否为有效的 Git 仓库，且本地是否安装有 `git` 工具。若不满足，后续涉及 Git log 的探查逻辑自动降级为“依赖用户口述或代码全局检索”，禁止强行执行 `git` 终端命令。
2. **pptx 技能依赖检查**：检查当前 Agent 的可用技能列表（Available Skills）中是否存在名为 `pptx` 的技能。
   - **若存在**：开启高阶模式。后续输出大纲时，**必须**按规范生成 `<!-- pptx-layout-metadata ... -->` 结构化 JSON 注释块。
   - **若不存在**：开启降级模式。**彻底不输出任何 JSON 元数据**以节省 Token 并防止噪音，仅保留 `>` 格式排版提示，并在大纲头部追加提示：`> [!NOTE] 本地未检测到 pptx 技能，无法自动转换为 PPTX，请使用排版提示手动制作。`
* **完成标准**：模型必须在思考中写出：“环境校验结果：Git 可用性 = [是/否]；pptx 技能存在性 = [是/否]”，决定最终的输出模式。

### 1. 探查与信息扩写 (Pre-flight Legwork & archaeology)
* **考古触发判定**：若用户提供的工作记录字数少于 15 字（或含义严重模糊，如“这周写完了收尾”）：
  - **交互询问**：你**必须**首先在对话中向用户提问，请示是否可以扫描本地 Git 提交与修改代码。
  - **执行扫描**（仅在用户同意且步骤 0 确认 Git 可用时执行）：通过 `git-archaeology`，运行 `git log --author="$(git config user.name)" --since="7 days ago" --oneline` 提取最近 7 天的提交，并结合代码全局检索分析具体修改的文件或类。
* **扩写与清点**：将模糊的记录具象化扩写。例如，“商户端收尾”扩写为“重构商户端提现状态机，解决流转异常”。
* **完成标准**：最终的扩写清单必须将技术改动点、模块名称具象化，杜绝空泛描述。

### 2. 划定页面与节奏
依据 **节奏交替 (surface-rhythm)** 规划分页结构，总页数控制在 5-8 页内：
* 封面页（1页）
* 开发产出页：按项目拆分。**自动分页**：若单个项目的开发条目超过 6 条，必须自动拆分为“项目名 (1/2)”和“项目名 (2/2)”两页，以防页面拥挤。
* 动态维度页：非开发工作提炼（如“调研发现”、“问题排查”）。
* 过渡节奏页：**若总页数大于 5 页，必须在中间插入至少 1 页深色底（Surface Dark）或强奶油底（Surface Cream Strong）的页面**作为过渡。
* 下周计划页（1页，必须作为尾页并使用深色表面收尾）。
* **完成标准**：大纲明确标出各页面的背景模式（Canvas / Dark / Cream Strong），且深浅色切换次数满足节奏要求。

### 3. 提炼页面内容
贯彻 **编辑风 (warm-editorial)** 的留白哲学编写每页内容：
* 开发产出页：单页条目限制在 [3, 6] 个。
  - **高阶模式 (有 pptx 技能)**：大纲卡片标题中**严禁**手写 `[已完成]`、`[重点]` 等前缀或状态 Emoji。必须保证大纲文本干净，所有状态依赖结构化 JSON 中的 `state` 属性来声明，由渲染端自动拼装对应的 Emoji (✅, ⏳, ⭐)。
  - **降级模式 (无 pptx 技能)**：大纲中可保留 `[已完成]`、`[进行中]` 等文本示意。
* 动态维度页：少于 3 条使用列表，大于等于 4 条采用卡片网格布局。
* 下周计划页：使用 `→` 开头展现具体动作。
* **完成标准**：单页条目数不超过 6 条，所有段落 and 元素排布保留充裕的视觉留白。

### 4. 附加排版提示与结构化元数据
* 每页末尾必须包含 `>` 格式排版提示。
* 根据步骤 0 的校验结果，若 pptx 技能可用，必须附加结构化的 `<!-- pptx-layout-metadata ... -->` JSON 元数据。在元数据中：
  - **多布局组件支持**：每一页应在元数据中包含 `"footer": { "show": true, "theme": "default" | "dark", "left_text": "...", "page_number": true }` 标准组件，控制通栏页脚块的渲染。
  - **原子状态配置**：开发产出页的 `cards` 数组中，每个卡片必须携带 `"state": "success" | "pending" | "starred"` 属性以驱动状态渲染。
  - **自适应计划对齐**：下周计划页（`next_steps`）中，使用 `"alignment": "vertical" | "horizontal"` 自适应地决策纵向堆叠或横向分栏排布（当项目数不多且列表项简短时使用 `horizontal`）。
* **完成标准**：所有的 JSON 格式数据无缺失，大纲内**严禁残留**诸如 `{{姓名}}` 或 `{{日期}}` 这样的原始占位符。

---

## 常见失效模式与防御 (Failure Modes & Defences)

* **依赖校验失效 (Verification Failure)**：
  - *防御*：严格执行“步骤 0”，若无 pptx 技能，从源头上切断 JSON 的生成，转为纯文本大纲与排版提示输出。
* **信息萎缩与越权扫描 (Information Shrinkage & Unapproved Scan)**：
  - *防御*：当输入极简时，**必须先取得用户明确同意**再执行 `git-archaeology` 的扫描命令，不能直接在后台静默运行以防越权；若用户拒绝，则通过全局检索非侵入式排查或提示用户补充。
* **状态双重编码 (Double-Encoded States)**：
  - *防御*：在高阶模式下，大纲卡片的 `title` 或文本中绝对不能包含 `[已完成]`、`✅` 等手写状态标识；它们与 JSON 元数据中的 `state` 属性冲突。模型必须保持文本纯净，状态呈现交由 `state` 驱动。
* **下周计划横向排版越界 (Next Steps Alignment Overflow)**：
  - *防御*：当项目分类（sections）超过 3 个，或者单个项目下的计划条目数超过 4 条、内容较长时，必须将 `alignment` 显式设为 `vertical`（或不配置以使用默认值），防止在 `horizontal` 布局下横向分列导致文本重叠溢出。
* **节奏崩塌 (Rhythm Collapse)**：
  - *防御*：页数超 5 页时强制校验是否含有过渡深色页/强奶油页，且尾页强制声明使用 `Surface Dark`。
* **卡片超载 (Card Overload)**：
  - *防御*：单页卡片数必须 $\le 6$，一旦超出必须执行**自动分裂分页**，禁止在单页内平铺过多条目。
* **占位符泄露 (Placeholder Leak)**：
  - *防御*：输出大纲前，模型必须进行一步自检，将模板中的所有 `{{占位符}}` 彻底替换为真实信息，无真实信息时替换为默认值（如“无开发计划”或省略该部分），绝对不允许将大花括号输出给用户。
* **JSON语法错误 (JSON Malformation)**：
  - *防御*：所有的 `<!-- pptx-layout-metadata` 注释块中的 JSON 必须格式正确，模型应校验大括号的对称性，防止由于语法错位导致下游解析失败。
