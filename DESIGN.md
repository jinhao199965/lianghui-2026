# 2026两会全球视野 - 设计文档

> 版本: v1.0  
> 更新: 2026-03-12  
> 作者: 小金专属龙虾 🦞

---

## 📐 页面结构

```
┌─────────────────────────────────────────────────────────────┐
│  Nav (固定顶部, z-index: 1000)                              │
│  ├─ Logo (左)                                               │
│  ├─ 2D/3D切换按钮 (右)                                       │
│  └─ 刷新按钮 (右)                                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Hero Section (100vh)                                       │
│  ├─ 3D地球 / 2D地图 (绝对定位, 全屏背景)                      │
│  │   ├─ 3D模式: Three.js Earth                             │
│  │   └─ 2D模式: 天地图 Map                                  │
│  │                                                          │
│  └─ Hero Content (左下角, z-index: 10)                      │
│      ├─ 副标题 (GLOBAL PERSPECTIVE 2026)                    │
│      ├─ 主标题 (2026全国两会...)                            │
│      ├─ 描述文案 (根据模式切换)                              │
│      └─ CTA按钮 (探索数据 →)                                │
│                                                             │
│  └─ Instruction (右下角浮动提示)                            │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  News Modal (fixed, z-index: 2000)                          │
│  ├─ 国家标题 + 关闭按钮                                     │
│  ├─ 可折叠的媒体机构列表                                     │
│  │   └─ 新闻卡片列表                                        │
│  └─ 点击外部/ESC关闭                                        │
├─────────────────────────────────────────────────────────────┤
│  Section: 核心数据                                          │
│  ├─ 标题 (核心数据)                                         │
│  └─ 4列统计卡片网格                                         │
│      ├─ GDP总量: 140.19 万亿元                              │
│      ├─ GDP增长率: 5.0%                                     │
│      ├─ 城镇新增就业: 1267 万人                             │
│      └─ 粮食产量: 1.43 万亿斤                               │
├─────────────────────────────────────────────────────────────┤
│  Section: 趋势洞察                                          │
│  ├─ 标题 (趋势洞察)                                         │
│  └─ ECharts 折线图容器                                       │
├─────────────────────────────────────────────────────────────┤
│  Section: 全球权威报道                                      │
│  ├─ 标题 (全球权威报道)                                     │
│  └─ 4列媒体卡片网格                                         │
│      ├─ 🇨🇳 中国媒体                                        │
│      ├─ 🇺🇸 美国媒体                                        │
│      ├─ 🇬🇧 英国媒体                                        │
│      └─ 🇯🇵🇩🇪🇫🇷 欧亚媒体                                 │
├─────────────────────────────────────────────────────────────┤
│  Loading Screen (fixed, z-index: 9999)                      │
│  ├─ 旋转动画                                                 │
│  └─ 3秒后自动隐藏                                           │
└─────────────────────────────────────────────────────────────┘
```

---

## 🎨 设计系统

### 颜色变量 (CSS Variables)

```css
:root {
  --ai-cyan: #00f0ff;           /* 主色调 - 科技青 */
  --ai-purple: #b347ff;         /* 辅助色 - 霓虹紫 */
  --ai-dark: #0a0a1a;           /* 深背景 */
  --ai-darker: #050510;         /* 更深背景 */
  --ai-glass: rgba(10, 20, 40, 0.8);  /* 毛玻璃背景 */
  
  /* 语义化颜色 */
  --text-primary: #ffffff;
  --text-secondary: rgba(255, 255, 255, 0.8);
  --text-muted: rgba(255, 255, 255, 0.6);
  --border-glow: rgba(0, 240, 255, 0.3);
  --border-subtle: rgba(0, 240, 255, 0.1);
}
```

### 渐变规范

```css
/* 标题渐变 */
background: linear-gradient(135deg, #fff 0%, var(--ai-cyan) 100%);

/* Logo渐变 */
background: linear-gradient(135deg, var(--ai-cyan) 0%, var(--ai-purple) 100%);

/* 按钮渐变 */
background: linear-gradient(135deg, 
  rgba(0, 240, 255, 0.2) 0%, 
  rgba(179, 71, 255, 0.2) 100%
);

/* 背景渐变 */
background: linear-gradient(135deg, 
  var(--ai-darker) 0%, 
  var(--ai-dark) 50%, 
  #0d0d2b 100%
);
```

---

## 🔧 组件详细规格

### 1. Navigation Bar

```
┌────────────────────────────────────────────────────────────┐
│ Logo              [3D地球 | 2D地图] [↻ 刷新]              │
└────────────────────────────────────────────────────────────┘

样式:
- Position: fixed, top: 0, left: 0, right: 0
- Height: ~60px
- Padding: 15px 30px
- Background: var(--ai-glass) + backdrop-filter: blur(20px)
- Border-bottom: 1px solid var(--border-subtle)
- Z-index: 1000

Logo:
- Font-size: 1.3rem
- Font-weight: 700
- Gradient text (cyan → purple)

2D/3D切换按钮:
- Container: flex, border-radius: 25px
- Background: rgba(0,0,0,0.4)
- Border: 1px solid var(--border-glow)
- Button padding: 8px 20px
- Active state: gradient background + cyan color
- Transition: all 0.3s

刷新按钮:
- Padding: 8px 16px
- Border-radius: 20px
- Gradient border + transparent bg
- Hover: box-shadow glow
- Spinning animation on refresh
```

### 2. Hero Section

```
┌────────────────────────────────────────────────────────────┐
│                                                            │
│   ┌──────────────────────────────────────────────┐        │
│   │                                                │        │
│   │   [3D Earth / 2D Map Background]               │   🌍   │
│   │                                                │ 提示   │
│   │                                                │        │
│   └──────────────────────────────────────────────┘        │
│                                                            │
│   GLOBAL PERSPECTIVE 2026                                  │
│   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                 │
│   2026全国两会                                             │
│   世界在看                                                 │
│                                                            │
│   "十五五"开局之年，全球目光聚焦中国。                      │
│   拖动旋转地球，点击光点查看各国报道。                      │
│                                                            │
│   ┌────────────────┐                                      │
│   │  探索数据 →    │                                      │
│   └────────────────┘                                      │
│                                                            │
└────────────────────────────────────────────────────────────┘

布局:
- Height: 100vh
- Display: flex
- Align-items: flex-end
- Padding: 0 0 80px 60px
- Position: relative

Earth/Map Container:
- Position: absolute
- Top: 0, Left: 0
- Width: 100%, Height: 100%
- Z-index: 1

Hero Content:
- Position: relative
- Z-index: 10
- Max-width: 500px
- Pointer-events: none (子元素 auto)

副标题:
- Font-size: 12px
- Letter-spacing: 0.4em
- Text-transform: uppercase
- Color: var(--ai-cyan)

主标题:
- Font-size: 3rem (移动端: 2rem)
- Font-weight: 900
- Line-height: 1.2
- Gradient text (white → cyan)
- Margin-bottom: 20px

描述:
- Font-size: 1rem
- Color: rgba(255,255,255,0.7)
- Line-height: 1.8

CTA按钮:
- Padding: 12px 30px
- Border-radius: 30px
- Gradient border + subtle bg
- Color: var(--ai-cyan)
- Hover: 光晕效果

Instruction (右下角):
- Position: absolute
- Bottom: 30px, Right: 40px
- Background: var(--ai-glass)
- Padding: 12px 25px
- Border-radius: 30px
- Border: 1px solid var(--border-subtle)
- Font-size: 13px
- Color: var(--ai-cyan)
```

### 3. View Toggle (2D/3D)

**3D模式显示:**
- 地球容器: `display: block`
- 地图容器: `display: none`
- 提示: "拖动旋转地球，点击光点查看各国报道。"
- 指令: "🌍 拖动旋转 · 点击光点查看"

**2D模式显示:**
- 地球容器: `display: none`
- 地图容器: `display: block`
- 提示: "点击地图上的标记查看各国报道。"
- 指令: "🗺️ 点击标记 · 查看报道"

### 4. News Modal

```
┌────────────────────────────────────────────────────────────┐
│  ← 黑色遮罩 rgba(5,5,16,0.9) →                            │
│                                                            │
│   ┌─────────────────────────────────────────────────┐     │
│   │ 🇨🇳 中国                                    ✕   │     │
│   ├─────────────────────────────────────────────────┤     │
│   │                                                 │     │
│   │  📰 新华社                          ▼  [5条]   │     │
│   │  ─────────────────────────────────────────────  │     │
│   │  ┌─────────────────────────────────────────┐   │     │
│   │  │ 2026年3月9日                            │   │     │
│   │  │ 十四届全国人大四次会议举行第二次全体会议   │   │     │
│   │  │ 国际媒体密切关注...                     │   │     │
│   │  │ 阅读全文 →                              │   │     │
│   │  └─────────────────────────────────────────┘   │     │
│   │  ┌─────────────────────────────────────────┐   │     │
│   │  │ ... 更多新闻                            │   │     │
│   │  └─────────────────────────────────────────┘   │     │
│   │                                                 │     │
│   │  📰 人民日报                        ▶  [4条]   │     │
│   │  📰 央视新闻                        ▶  [6条]   │     │
│   │                                                 │     │
│   └─────────────────────────────────────────────────┘     │
│                                                            │
└────────────────────────────────────────────────────────────┘

容器:
- Position: fixed
- Top: 0, Left: 0
- Width: 100%, Height: 100%
- Background: rgba(5, 5, 16, 0.9)
- Z-index: 2000
- Display: flex (居中)
- Padding: 20px

内容区:
- Background: var(--ai-glass)
- Border: 1px solid var(--border-glow)
- Border-radius: 20px
- Max-width: 800px
- Max-height: 85vh
- Overflow-y: auto

Header:
- Padding: 25px
- Border-bottom: 1px solid var(--border-subtle)
- Flex layout (space-between)
- Title: gradient text

媒体机构列表:
- 可折叠 accordion
- 默认第一个展开
- Header: gradient bg + pointer cursor
- Content: max-height transition

新闻卡片:
- Padding: 15px
- Margin-bottom: 10px
- Background: rgba(255,255,255,0.03)
- Border-radius: 10px
- Left border: 3px solid var(--ai-cyan)
```

### 5. Stats Section

```
┌────────────────────────────────────────────────────────────┐
│                                                            │
│              核心数据                                      │
│              ════════                                      │
│                                                            │
│   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│   │  140.19  │  │   5.0%   │  │   1267   │  │   1.43   │  │
│   │  ──────  │  │  ──────  │  │  ──────  │  │  ──────  │  │
│   │GDP总量   │  │GDP增长率 │  │城镇新增  │  │粮食产量  │  │
│   │(万亿元)  │  │          │  │就业(万人)│  │(万亿斤)  │  │
│   └──────────┘  └──────────┘  └──────────┘  └──────────┘  │
│                                                            │
└────────────────────────────────────────────────────────────┘

Section:
- Padding: 100px 50px
- Max-width: 1200px
- Margin: 0 auto

标题:
- Font-size: 2.5rem
- Font-weight: 700
- Text-align: center
- Gradient text

Grid:
- Display: grid
- Grid-template-columns: repeat(auto-fit, minmax(250px, 1fr))
- Gap: 30px

卡片:
- Background: var(--ai-glass)
- Border: 1px solid var(--border-subtle)
- Border-radius: 20px
- Padding: 40px
- Text-align: center

数字:
- Font-size: 3.5rem
- Font-weight: 900
- Gradient text (cyan → purple)

标签:
- Font-size: 1rem
- Color: var(--text-secondary)
```

### 6. Chart Section

```
┌────────────────────────────────────────────────────────────┐
│                                                            │
│              趋势洞察                                      │
│                                                            │
│   ┌────────────────────────────────────────────────────┐  │
│   │                                                    │  │
│   │          ╭────────────────────────────╮           │  │
│   │         ╱                              ╲          │  │
│   │    140 ─●                                ●        │  │
│   │       ╱ ╲                              ╱          │  │
   │  130 ─┤   ╲                          ╱            │  │
│   │       │    ╲                      ●              │  │
│   │  120 ─┤      ╲                  ╱                │  │
│   │       │        ●──────────────●                  │  │
│   │  110 ─┤       ╱                                  │  │
│   │       │      ╱                                   │  │
│   │       └──────┬──────┬──────┬──────┬──────        │  │
│   │             2021  2022  2023  2024  2025         │  │
│   │                                                    │  │
│   └────────────────────────────────────────────────────┘  │
│                                                            │
└────────────────────────────────────────────────────────────┘

Chart Container:
- Height: 400px
- Background: var(--ai-glass)
- Border: 1px solid var(--border-subtle)
- Border-radius: 20px
- Padding: 20px

ECharts 样式:
- 背景: transparent
- 轴线: rgba(0,240,255,0.3)
- 标签: rgba(255,255,255,0.7)
- 网格线: rgba(0,240,255,0.1)
- 折线: #00f0ff, width: 3
- 区域填充: cyan gradient (top 50% → bottom 0%)
```

### 7. Media Section

```
┌────────────────────────────────────────────────────────────┐
│                                                            │
│              全球权威报道                                  │
│                                                            │
│   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────┐ │
│   │ 🇨🇳 中国媒体 │ │ 🇺🇸 美国媒体 │ │ 🇬🇧 英国媒体 │ │ ... │ │
│   │             │ │             │ │             │ │     │ │
│   │ 新华社 -    │ │ Reuters -   │ │ BBC News -  │ │ ... │ │
│   │ 两会专题    │ │ China News  │ │ China       │ │ ... │ │
│   │ ─────────── │ │ ─────────── │ │ ─────────── │ │     │ │
│   │ 人民日报 -  │ │ Bloomberg - │ │ FT -        │ │ ... │ │
│   │ 两会专题    │ │ Asia        │ │ China       │ │ ... │ │
│   │ ─────────── │ │ ─────────── │ │ ─────────── │ │     │ │
│   │ 央视新闻 -  │ │ NYT -       │ │ Guardian -  │ │ ... │ │
│   │ 两会报道    │ │ Asia        │ │ China       │ │ ... │ │
│   │             │ │             │ │             │ │     │ │
│   └─────────────┘ └─────────────┘ └─────────────┘ └─────┘ │
│                                                            │
└────────────────────────────────────────────────────────────┘

Grid:
- Grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))
- Gap: 25px

卡片:
- Background: var(--ai-glass)
- Border: 1px solid var(--border-subtle)
- Border-radius: 16px
- Padding: 25px

标题:
- Color: var(--ai-cyan)
- Font-size: 1.2rem
- Margin-bottom: 15px

链接:
- Display: block
- Padding: 10px 0
- Color: rgba(255,255,255,0.8)
- Border-bottom: 1px solid var(--border-subtle)
- Hover: color → var(--ai-cyan)
```

### 8. Loading Screen

```
┌────────────────────────────────────────────────────────────┐
│                                                            │
│                                                            │
│                    ╭──────────╮                            │
│                    │  ⟳      │   ← 旋转动画                │
│                    ╰──────────╯                            │
│                                                            │
│              INITIALIZING AI SYSTEM...                     │
│                                                            │
│                                                            │
└────────────────────────────────────────────────────────────┘

样式:
- Position: fixed
- Top: 0, Left: 0
- Width: 100%, Height: 100%
- Background: var(--ai-darker)
- Z-index: 9999
- Display: flex (居中)
- Transition: opacity 0.5s

旋转动画:
- Width: 80px, Height: 80px
- Border: 3px solid rgba(0,240,255,0.2)
- Border-top-color: var(--ai-cyan)
- Border-radius: 50%
- Animation: spin 1s linear infinite

文字:
- Margin-top: 20px
- Color: var(--ai-cyan)
- Letter-spacing: 2px
- Font-size: 14px

自动隐藏:
- 3秒后添加 .hidden class
- Opacity: 0, pointer-events: none
```

---

## 📱 响应式断点

```css
/* 桌面 (默认) */
/* >= 1024px */

/* 平板 */
@media (max-width: 1024px) {
  .stats-grid { grid-template-columns: repeat(2, 1fr); }
}

/* 手机 */
@media (max-width: 768px) {
  .hero {
    padding: 0 20px 60px 20px;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  .hero-title { font-size: 2rem; }
  .section { padding: 60px 20px; }
  nav { padding: 12px 20px; }
  .stats-grid { grid-template-columns: 1fr; }
  .media-grid { grid-template-columns: 1fr; }
}
```

---

## 🎯 交互规范

| 元素 | 交互 | 效果 |
|------|------|------|
| 2D/3D切换 | Click | 切换显示模式 + 更新提示文案 |
| 刷新按钮 | Click | 旋转动画 → 刷新新闻数据 |
| 3D地球 | Drag | 旋转地球 |
| 3D地球 | Click marker | 打开新闻弹窗 |
| 2D地图 | Click marker | 打开新闻弹窗 |
| 新闻弹窗 | Click外部/ESC | 关闭弹窗 |
| 媒体机构 | Click header | 折叠/展开列表 |
| CTA按钮 | Hover | 光晕阴影效果 |
| 链接 | Hover | 颜色变为 cyan |
| 卡片 | Hover | 轻微上浮 + 边框高亮 |

---

## 🗂️ 文件结构

```
lianghui-2026/
├── index.html          # 主页面
├── assets/
│   └── (纹理图片从CDN加载)
└── README.md
```

---

## 🔌 第三方依赖

```html
<!-- Three.js (3D地球) -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>

<!-- ECharts (图表) -->
<script src="https://cdn.jsdelivr.net/npm/echarts@5.4.3/dist/echarts.min.js"></script>

<!-- 天地图API (2D地图) -->
<script src="https://api.tianditu.gov.cn/api?v=4.0&tk=YOUR_KEY"></script>
```

---

## 💡 开发提示

1. **纹理加载**: 使用国内CDN链自动降级，避免白屏
2. **地图Key**: 天地图需要申请Key，有免费额度
3. **性能优化**: Three.js使用requestAnimationFrame
4. **移动端**: 触摸事件需要单独处理
5. **兼容性**: 检测WebGL支持，不支持时降级到2D模式

---

*Made with 🦞 by 小金专属龙虾*
