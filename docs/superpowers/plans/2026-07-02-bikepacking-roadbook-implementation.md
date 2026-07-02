# Bikepacking Roadbook Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Generate a Chinese bikepacking route package with a route-comparison document, a complete executable roadbook, and a standalone mobile-first companion invitation page.

**Architecture:** Keep the project dependency-free and file-based. The route comparison, full roadbook, and invitation page are separate hand-authored artifacts so each can be read or shared independently.

**Tech Stack:** Markdown, standalone HTML, CSS, no build system, no npm dependencies.

---

## File Structure

- Create `route-options.md`: records the three route candidates, comparison criteria, and why the final recommendation avoids commercial scenic spots and favors free road scenery.
- Create `roadbook.md`: the primary Chinese field guide for the actual trip, including daily route plan, food, lodging, risks, gear, adjustment logic, and riding-partner expectations.
- Create `ride-with-me.html`: the standalone Chinese mobile-first invitation page for finding riding partners.
- Modify `002-行前准备.md`: remove the stray unclosed Markdown code fence before the maintenance table so the table renders correctly.
- Keep `001-封面.md`, `003.md`, and `roadbook.html` unchanged unless the user later asks to retire or replace them.

## Task 1: Fix Existing Markdown Rendering Issue

**Files:**
- Modify: `002-行前准备.md`

- [ ] **Step 1: Inspect the code fence area**

Run:

```bash
sed -n '183,210p' 002-行前准备.md
```

Expected: output shows a lone line containing three backticks immediately before the maintenance table.

- [ ] **Step 2: Remove the stray code fence**

Edit `002-行前准备.md` so this block:

```markdown
不要前一天才去车店。

```

| 项目 | 建议 |
```

becomes:

```markdown
不要前一天才去车店。

| 项目 | 建议 |
```

- [ ] **Step 3: Verify the table area**

Run:

```bash
sed -n '183,210p' 002-行前准备.md
```

Expected: the maintenance table starts directly after the prose, with no triple-backtick line before it.

## Task 2: Write Route Comparison Document

**Files:**
- Create: `route-options.md`
- Read: `docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md`

- [ ] **Step 1: Re-read the approved design constraints**

Run:

```bash
sed -n '1,120p' docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md
```

Expected: output includes the rider constraints, recommended route direction, and three candidate route concepts.

- [ ] **Step 2: Create `route-options.md` with the route decision**

Write `route-options.md` with this structure:

```markdown
# 国庆 Bikepacking 路线方案对比

## 决策前提

- 从上海高铁 / 动车接驳到起点，不从上海市区直接开骑。
- 总骑行约 11 天，整体不超过 12 天。
- 每日距离约 100 km，后期允许更温和。
- 公路车 28C 外胎，以柏油路为主。
- 大多数日子爬升控制在 1500 m 以内。
- 不露营，优先村镇民宿和特色客栈。
- 不以收费商业景区为目标，优先免费开放的公路风景、山谷、江景和村镇边缘。

## 对比维度

| 维度 | 说明 |
|---|---|
| 风景密度 | 是否每天都有值得骑过去的风景 |
| 公路车友好度 | 28C 公路车是否可接受 |
| 国庆风险 | 车流、住宿、人流和临时变化风险 |
| 强度曲线 | 是否符合前期略硬、后期变温和 |
| 叙事完整度 | 是否像一趟完整旅行，而不是点位拼接 |

## 方案一：安吉 -> 皖南 -> 徽州外围 -> 新安江 -> 富春江 -> 杭州

推荐度：★★★★★

路线弧线：

上海 -> 安吉 / 湖州 -> 安吉 -> 宁国 -> 青龙湾 / 储家滩 -> 绩溪 -> 歙县 / 徽州外围 -> 新安江 / 建德 -> 梅城 -> 桐庐 -> 富阳 -> 杭州 -> 上海

优点：

- 与现有项目主题最契合。
- 前半程有竹海、皖南山水、徽州村镇。
- 后半程顺着新安江和富春江自然降强度。
- 不依赖收费景区也能成立。
- 终点杭州返沪方便。

风险：

- 国庆期间皖南热门自驾路段车流不可忽视。
- 个别县道路况需要出发前用地图和骑行软件复核。
- Day 2-Day 3 需要准备保守版本，不能只看风景不看体感。

结论：

作为默认主路线。正式 Roadbook 按这条线展开。

## 方案二：安吉 / 莫干山外围 -> 千岛湖外围 -> 建德 -> 桐庐 -> 杭州

推荐度：★★★★☆

优点：

- 对 28C 公路车更友好。
- 强度更容易控制。
- 后半程恢复感很好。
- 适合皖南车流或天气风险过高时切换。

风险：

- 徽州文化和山水层次不如方案一。
- 千岛湖周边国庆住宿和车流压力较大。
- 容易变成“好骑但故事性稍弱”的路线。

结论：

作为备用路线，不作为第一推荐。

## 方案三：婺源 / 徽州外围 -> 新安江 -> 富春江 -> 杭州

推荐度：★★★☆☆

优点：

- 高铁抵达后风景兑现快。
- 古村、山水和江河气质强。
- 适合未来做更偏摄影和山水的版本。

风险：

- 前期爬升更难压在 1500 m 以内。
- 国庆人流压力更大。
- 商业化景点诱惑多，容易偏离免费公路风景的初衷。

结论：

作为以后升级版或摄影版路线，不作为本次默认方案。

## 最终选择

本次选择方案一，并吸收方案二后半程的温和收尾逻辑。

最终 Roadbook 的重点不是打卡宏村、西递或其他收费景区，而是把时间放在免费开放的山水公路、村镇边缘、江景和骑行节奏上。
```

- [ ] **Step 3: Verify the document exists and has the expected headings**

Run:

```bash
rg -n "^#|^##" route-options.md
```

Expected: output includes `# 国庆 Bikepacking 路线方案对比`, `## 方案一`, `## 方案二`, `## 方案三`, and `## 最终选择`.

## Task 3: Write Complete Roadbook

**Files:**
- Create: `roadbook.md`
- Read: `route-options.md`
- Read: `docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md`

- [ ] **Step 1: Confirm source documents are present**

Run:

```bash
ls route-options.md docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md
```

Expected: both file paths are printed.

- [ ] **Step 2: Create `roadbook.md`**

Write `roadbook.md` in Chinese with these exact top-level sections:

```markdown
# 徽州 · 富春山居 Bikepacking Roadbook

## 版本信息

## 这趟旅行是什么

## 核心原则

## 路线总览

## 时间与交通策略

## 适合谁

## 不适合谁

## 车辆与装备

## 住宿策略

## 饮食与补给策略

## 每日路线

## 免费风景优先策略

## 风险与撤退方案

## 搭子规则

## 出发前最终检查
```

Required content rules:

- Use Chinese throughout.
- State that the route starts by rail from Shanghai to Anji / Huzhou and returns by rail from Hangzhou.
- State that the plan avoids riding out of Shanghai city.
- State that the route avoids commercial paid scenic spots as core goals.
- Include 11 riding/planning days plus Day 0 transfer.
- Include 28C road-bike constraints.
- Include no-camping accommodation policy.
- Include free-road-scenery priority.

- [ ] **Step 3: Fill the daily route table**

Inside `## 每日路线`, include this summary table:

```markdown
| 日程 | 路线 | 距离 | 爬升 | 气质 | 住宿倾向 |
|---|---:|---:|---:|---|---|
| Day 0 | 上海 -> 安吉 / 湖州 | 接驳 | - | 装车与补给 | 安吉 / 湖州外围 |
| Day 1 | 安吉 -> 广德 / 宁国方向 | 90-105 km | 900-1300 m | 竹海热身 | 村镇民宿 / 客栈 |
| Day 2 | 宁国 -> 青龙湾 / 储家滩 -> 板桥 / 苏红外围 | 80-95 km | 1200-1500 m | 湖景山路 | 山区民宿 |
| Day 3 | 板桥 / 苏红 -> 绩溪外围 / 家朋取舍段 | 75-95 km | 1300-1500 m | 前期关键山地日 | 村镇民宿 |
| Day 4 | 绩溪 -> 歙县 / 徽州区 | 75-95 km | 700-1200 m | 徽州过渡 | 古城外围 / 村镇 |
| Day 5 | 歙县 -> 徽州外围山水公路 -> 黟县 / 休宁 | 70-90 km | 900-1300 m | 免费村镇风景 | 特色民宿 |
| Day 6 | 黟县 / 休宁 -> 淳安或新安江方向 | 90-110 km | 800-1300 m | 山转水 | 江边 / 镇上民宿 |
| Day 7 | 新安江 / 淳安 -> 建德 / 梅城 | 75-95 km | 500-900 m | 江景恢复 | 梅城 / 建德民宿 |
| Day 8 | 梅城 -> 桐庐 | 75-95 km | 400-800 m | 富春江核心 | 桐庐江边 / 镇上 |
| Day 9 | 桐庐 -> 富阳 | 65-85 km | 300-700 m | 温和收尾 | 富阳 / 江边民宿 |
| Day 10 | 富阳 -> 杭州 | 50-75 km | 低 | 仪式感终点 | 杭州或返沪 |
| Day 11 | 机动日 | 灵活 | 灵活 | 天气 / 体力 / 机械缓冲 | 视情况 |
```

- [ ] **Step 4: Add one detailed subsection for each day**

After the summary table, add subsections from `### Day 0` through `### Day 11`.

Each riding day from Day 1 to Day 10 must include these labels:

```markdown
建议出发：
建议到达：
路况判断：
补给策略：
住宿策略：
风景重点：
风险：
保守调整：
```

Day 0 must include rail transfer, bike assembly, and supply check. Day 11 must include weather, fatigue, mechanical, and early-return options.

- [ ] **Step 5: Add practical checklists**

Add these checklists under `## 出发前最终检查`:

```markdown
### 车辆

- [ ] 外胎无明显割伤
- [ ] 刹车片余量充足
- [ ] 链条润滑
- [ ] 变速全档位正常
- [ ] 备用内胎 / 补胎工具齐全
- [ ] 码表、车灯、尾灯充电完成

### 个人装备

- [ ] 头盔
- [ ] 骑行眼镜
- [ ] 防晒
- [ ] 雨具
- [ ] 保暖层
- [ ] 换洗衣物
- [ ] 身份证
- [ ] 充电器 / 充电宝

### 出发前 48 小时

- [ ] 复查天气
- [ ] 复查高铁班次
- [ ] 复查住宿
- [ ] 复查 Day 1-Day 3 路况和施工
- [ ] 导出 GPX 或在骑行 App 中保存路线
```

- [ ] **Step 6: Verify headings and daily coverage**

Run:

```bash
rg -n "^#|^##|^### Day" roadbook.md
```

Expected: output includes every top-level section and `### Day 0` through `### Day 11`.

## Task 4: Build Companion Invitation HTML

**Files:**
- Create: `ride-with-me.html`
- Read: `roadbook.md`
- Read: `docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md`

- [ ] **Step 1: Confirm roadbook exists**

Run:

```bash
ls roadbook.md
```

Expected: `roadbook.md` is printed.

- [ ] **Step 2: Create standalone HTML shell**

Write `ride-with-me.html` with:

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>徽州 · 富春山居 Bikepacking 搭子招募</title>
  </head>
  <body>
  </body>
</html>
```

- [ ] **Step 3: Add CSS design system**

Add an inline `<style>` block in the `<head>` using these design rules:

```css
:root {
  color-scheme: light;
  --paper: #f7f1e6;
  --surface: #fffaf0;
  --ink: #1f2933;
  --muted: #667085;
  --line: #d8cdbb;
  --mountain: #315f45;
  --river: #2f6f8f;
  --warning: #a43d2f;
  --stone: #e8ddcb;
  --white: #ffffff;
}

* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
  background: var(--paper);
  color: var(--ink);
  line-height: 1.65;
  font-size: 16px;
}
```

Then continue styling the page with:

- constrained content width around `1120px` on desktop.
- `24px` mobile side padding.
- cards with `border-radius: 8px`.
- no emoji as structural icons.
- clear focus styles for links and buttons.
- responsive grid that becomes one column on small screens.
- `@media (prefers-reduced-motion: reduce)` to disable smooth scrolling.

- [ ] **Step 4: Add page content sections**

Inside `<body>`, add these sections in order:

```html
<header class="hero">...</header>
<main>
  <section id="snapshot">...</section>
  <section id="route-arc">...</section>
  <section id="daily-plan">...</section>
  <section id="fit">...</section>
  <section id="agreements">...</section>
  <section id="contact">...</section>
</main>
```

Required content:

- Hero says the trip starts by rail from Shanghai and rides from Anji / southern Anhui toward Fuchun River and Hangzhou.
- Snapshot includes `11 天`, `约 900-1050 km`, `每天约 100 km`, `不露营`, `28C 公路车友好`.
- Route arc includes Anji, Ningguo, Qinglongwan / Chujia Tan, Jixi / Shexian, Xin'an River, Meicheng, Tonglu, Fuyang, Hangzhou.
- Daily plan includes cards for Day 0 through Day 11.
- Fit section includes both "适合加入" and "不太适合".
- Agreements include AA, no camping, no planned night riding, safety priority, free-road-scenery priority.
- Contact section contains a visible placeholder text: `联系方式：出发前由我补充。`

- [ ] **Step 5: Verify standalone HTML basics**

Run:

```bash
rg -n "<!doctype html>|<html lang=\"zh-CN\">|<meta name=\"viewport\"|id=\"daily-plan\"|联系方式：出发前由我补充" ride-with-me.html
```

Expected: all searched patterns are found.

## Task 5: Final Verification

**Files:**
- Read: `route-options.md`
- Read: `roadbook.md`
- Read: `ride-with-me.html`
- Read: `002-行前准备.md`

- [ ] **Step 1: Confirm expected files exist**

Run:

```bash
ls route-options.md roadbook.md ride-with-me.html docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md
```

Expected: all four paths are printed.

- [ ] **Step 2: Check no unfinished Chinese placeholders remain**

Run:

```bash
rg -n "待补|待定|之后再写|以后补" route-options.md roadbook.md ride-with-me.html docs/superpowers/specs/2026-07-02-bikepacking-roadbook-design.md
```

Expected: no matches.

- [ ] **Step 3: Check commercial scenic spot guidance**

Run:

```bash
rg -n "宏村|西递|收费|商业化|免费|公路风景" route-options.md roadbook.md ride-with-me.html
```

Expected: matches clearly show that macro guidance avoids commercial paid scenic spots and prioritizes free road scenery.

- [ ] **Step 4: Check Day 0-Day 11 coverage**

Run:

```bash
for d in 0 1 2 3 4 5 6 7 8 9 10 11; do rg -n "Day $d" roadbook.md ride-with-me.html; done
```

Expected: each day appears in both `roadbook.md` and `ride-with-me.html`.

- [ ] **Step 5: Check `002-行前准备.md` has no stray code fence near the maintenance table**

Run:

```bash
sed -n '183,200p' 002-行前准备.md
```

Expected: no triple-backtick line appears before `| 项目 | 建议 |`.

- [ ] **Step 6: Check project remains dependency-free**

Run:

```bash
ls package.json package-lock.json pnpm-lock.yaml yarn.lock 2>/dev/null
```

Expected: no output, because no Node dependency files should exist.

## Commit Note

The current directory is not a Git repository. Do not run commit steps unless the user initializes Git later. If Git is initialized later, commit after each task with messages like:

```bash
git add 002-行前准备.md
git commit -m "fix: repair pre-trip markdown table"

git add route-options.md
git commit -m "docs: add bikepacking route options"

git add roadbook.md
git commit -m "docs: add bikepacking roadbook"

git add ride-with-me.html
git commit -m "feat: add bikepacking companion invite page"
```
