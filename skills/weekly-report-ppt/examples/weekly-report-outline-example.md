# 张三 周报 | 2026.06.19 - 2026.06.25

> 模板规范: [style-specification.md](file:///Users/aohan/aohan_dev/skills-private/skills/weekly-report-ppt/references/style-specification.md)

> [!NOTE] 
> 本示例展示了**高阶模式**（具备 pptx 技能）下的元数据 JSON 生成规范。
> 如果您的 Agent 启动了**降级模式**（无 pptx 技能），请**彻底省略**所有 `<!-- pptx-layout-metadata ... -->` 注释块，只保留常规文本和 `>` 排版提示。

---

## 第1页：封面

**张三 周报** | 2026.06.19 - 2026.06.25

> 排版提示：页面背景 #FAF9F5，垂直居中，"张三 周报"衬线体 33pt/400/-0.4pt #141413，"|" Hairline色 #E6DFD8 18pt，"2026.06.19 - 2026.06.25"无衬线 18pt/400 #6C6A64，标题与日期上下排列间距 0.4cm，无其他装饰。封面页隐藏通栏页脚块。

<!-- pptx-layout-metadata
{
  "slide_type": "cover",
  "background": "#FAF9F5",
  "rhythm": "canvas",
  "alignment": "center",
  "title": {
    "primary": "张三 周报",
    "primary_font": "serif",
    "primary_size": "33pt",
    "primary_color": "#141413",
    "separator": "|",
    "date": "2026.06.19 - 2026.06.25",
    "date_font": "sans-serif",
    "date_size": "18pt",
    "date_color": "#6C6A64"
  },
  "footer": {
    "show": false
  }
}
-->

---

## 第2页：重构商户端后台

```
┌─────────────────────────────────┐  ╔═════════════════════════════════╗
│ [已完成] 提现申请模块重构       │  ║ [重点] 保证金绑定流程优化       ║
│ - 重新设计状态机，修复流转异常  │  ║ - 简化了商户入驻时的保证金校验  ║
└─────────────────────────────────┘  ╚═════════════════════════════════╝
              默认卡片                            重点卡片
     (渲染端依据 state: success 自动      (渲染端依据 state: starred 自动
      拼装已完成 Emoji✅ 与背景样式)        拼装重点 Emoji⭐ 与左珊瑚边框)
```

进度：85%

> 排版提示：页面背景 #FAF9F5，页标题"重构商户端后台"衬线体 22pt/400/-0.2pt #141413 + 珊瑚装饰线(1.5pt高/1.0cm宽 #CC785C)，进度 85% 右侧同行 11pt #6C6A64，2列网格，卡片间距 0.4cm，卡片内边距 0.8cm，圆角 0.3cm。
>
> - 状态拼装：大纲文本不硬编码状态。渲染端通过 `state: "success"` 自动渲染为暖奶油底 #EFE9DE + Hairline边框 0.75pt #E6DFD8 并前置 `✅` 标识；通过 `state: "starred"` 自动渲染为画布底 #FAF9F5 + 珊瑚左边框 2pt #CC785C 并前置 `⭐` 标识。
> - 页脚：页面底部展示通栏页脚块，左侧为 "张三 | 周报汇报"，右侧展示页码。

<!-- pptx-layout-metadata
{
  "slide_type": "project_output",
  "background": "#FAF9F5",
  "rhythm": "canvas",
  "title": {
    "text": "重构商户端后台",
    "font": "serif",
    "size": "22pt",
    "color": "#141413",
    "accent_line": { "height": "1.5pt", "width": "1.0cm", "color": "#CC785C" }
  },
  "progress": {
    "value": "85%",
    "font": "sans-serif",
    "size": "11pt",
    "color": "#6C6A64"
  },
  "layout": {
    "type": "grid",
    "columns": 2,
    "gap": "0.4cm",
    "padding": "0.8cm",
    "border_radius": "0.3cm"
  },
  "cards": [
    {
      "state": "success",
      "title": "提现申请模块重构",
      "description": "重新设计状态机，修复流转异常"
    },
    {
      "state": "starred",
      "title": "保证金绑定流程优化",
      "description": "简化了商户入驻时的保证金校验"
    }
  ],
  "footer": {
    "show": true,
    "theme": "default",
    "left_text": "张三 | 周报汇报",
    "page_number": true
  }
}
-->

---

## 第3页：过渡页 (Rhythm Slide)

**以克制致敬复杂**

> 排版提示：页面背景 #181715 (深色表面)，垂直居中，大标题居中衬线体 22pt/400/-0.2pt #FAF9F5 (On Dark)，副标题无衬线 11pt #A09D96。配置深色通栏页脚块。

<!-- pptx-layout-metadata
{
  "slide_type": "rhythm_slide",
  "background": "#181715",
  "rhythm": "dark",
  "title": {
    "text": "以克制致敬复杂",
    "font": "serif",
    "size": "22pt",
    "color": "#FAF9F5"
  },
  "footer": {
    "show": true,
    "theme": "dark",
    "left_text": "张三 | 周报汇报",
    "page_number": true
  }
}
-->

---

## 第4页：下周计划

**重构商户端后台**
→ 完成保证金退款模块联调
→ 进行边界异常状态测试

**其他**
→ 协助前端排查交易延迟问题

> 排版提示：页面背景 #181715(深色表面)，页标题"下周计划"衬线体 22pt/400/-0.2pt #FAF9F5(On Dark) + 珊瑚装饰线(1.5pt高/1.0cm宽 #CC785C)，配置深色通栏页脚块。
>
> - 自适应横向布局：使用 `"alignment": "horizontal"` 将多个项目的下周计划横向分栏排布（从左到右分列，左列为 "重构商户端后台"，右列为 "其他"），栏间距 0.6cm，栏内边距 0.8cm。每一栏内，项目名小标题无衬线 12pt/500 #FAF9F5(On Dark)，列表条目无衬线 11pt/400 #A09D96(On Dark Soft)。

<!-- pptx-layout-metadata
{
  "slide_type": "next_steps",
  "background": "#181715",
  "rhythm": "dark",
  "title": {
    "text": "下周计划",
    "font": "serif",
    "size": "22pt",
    "color": "#FAF9F5",
    "accent_line": { "height": "1.5pt", "width": "1.0cm", "color": "#CC785C" }
  },
  "alignment": "horizontal",
  "sections": [
    {
      "subtitle": "重构商户端后台",
      "subtitle_font": "sans-serif",
      "subtitle_size": "12pt",
      "subtitle_color": "#FAF9F5",
      "items": [
        "完成保证金退款模块联调",
        "进行边界异常状态测试"
      ],
      "item_font": "sans-serif",
      "item_size": "11pt",
      "item_color": "#A09D96",
      "item_prefix": "→"
    },
    {
      "subtitle": "其他",
      "subtitle_font": "sans-serif",
      "subtitle_size": "12pt",
      "subtitle_color": "#FAF9F5",
      "items": [
        "协助前端排查交易延迟问题"
      ],
      "item_font": "sans-serif",
      "item_size": "11pt",
      "item_color": "#A09D96",
      "item_prefix": "→"
    }
  ],
  "spacing": "0.6cm",
  "footer": {
    "show": true,
    "theme": "dark",
    "left_text": "张三 | 周报汇报",
    "page_number": true
  }
}
-->
