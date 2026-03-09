# 2026年全国两会政府工作报告数据分析 - 部署说明

## 📁 项目结构

```
2026两会政府工作报告数据分析/
├── index.html          # 主页面（包含所有数据、图表和分析）
└── README.md          # 本说明文件
```

## 🚀 部署方式

### 方式一：GitHub Pages（推荐，免费）

1. **创建GitHub仓库**
   - 登录 https://github.com
   - 点击 "New repository"
   - 仓库名：`lianghui-data-analysis`（或其他你喜欢的名字）
   - 选择 "Public"
   - 点击 "Create repository"

2. **上传文件**
   ```bash
   # 在本地文件夹中执行
   git init
   git add index.html README.md
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/你的用户名/lianghui-data-analysis.git
   git push -u origin main
   ```

3. **启用GitHub Pages**
   - 进入仓库 Settings → Pages
   - Source 选择 "Deploy from a branch"
   - Branch 选择 "main"，文件夹选择 "/ (root)"
   - 点击 Save
   - 等待几分钟，访问 `https://你的用户名.github.io/lianghui-data-analysis`

### 方式二：Vercel（推荐，免费，国内访问快）

1. **注册/登录**
   - 访问 https://vercel.com
   - 用GitHub账号登录

2. **导入项目**
   - 点击 "Add New Project"
   - 导入GitHub仓库
   - Framework Preset 选择 "Other"
   - 点击 Deploy

3. **获取地址**
   - 部署完成后会获得类似 `lianghui-data-analysis.vercel.app` 的地址

### 方式三：Netlify（免费）

1. **注册/登录**
   - 访问 https://netlify.com
   - 用GitHub账号登录

2. **部署**
   - 点击 "Add new site" → "Import an existing project"
   - 选择GitHub仓库
   - 点击 Deploy site

### 方式四：腾讯云/阿里云静态网站托管

1. **创建OSS存储桶**
   - 登录云服务商控制台
   - 创建OSS/COS存储桶
   - 开启静态网站托管
   - 上传 index.html

2. **配置CDN**（可选）
   - 开启CDN加速
   - 绑定自定义域名

## 📊 页面内容

网页包含以下内容：

1. **核心数据亮点卡片**
   - 2025年GDP总量：140.19万亿元
   - GDP增长率：5.0%
   - 城镇新增就业：1267万人
   - 粮食产量：1.43万亿斤

2. **六大趋势分析**
   - 经济从高速增长转向高质量发展
   - 新质生产力成为核心驱动力
   - 粮食安全与绿色转型双轮驱动
   - 就业形势总体稳定但结构性压力仍在
   - 从"三驾马车"到"国内大循环"的战略转型
   - 宏观政策更加积极有为

3. **交互式图表**（使用ECharts）
   - GDP趋势图（增长率+总量双轴）
   - 就业数据图（新增就业+失业率）
   - 粮食产量变化图
   - 单位GDP能耗降低图
   - 重点产业数据图（新能源汽车+制造业增长）
   - 历年目标对比图

4. **数据表格**
   - 近五年经济指标完成情况
   - 各年度政府工作报告中设定的主要预期目标
   - 重点产业数据（2021-2025）
   - 2026年发展目标

5. **Tab切换组件**
   - 经济发展
   - 创新驱动
   - 民生福祉
   - 绿色低碳

## 🎨 技术栈

- **HTML5** - 页面结构
- **CSS3** - 响应式布局、动画效果
- **ECharts** - 数据可视化图表
- **原生JavaScript** - 交互逻辑

## 📱 响应式设计

页面支持：
- ✅ PC端（大屏幕）
- ✅ 平板端（中等屏幕）
- ✅ 手机端（小屏幕）

## 🔗 分享地址示例

部署完成后，你可以分享给朋友的地址格式：

- GitHub Pages: `https://你的用户名.github.io/lianghui-data-analysis`
- Vercel: `https://lianghui-data-analysis.vercel.app`
- Netlify: `https://lianghui-data-analysis.netlify.app`

## 📞 帮助

如果在部署过程中遇到问题，可以：
1. 查看GitHub/Vercel/Netlify官方文档
2. 搜索相关教程
3. 询问我（小金专属龙虾🦞）

---

**制作时间**：2026年3月9日  
**数据来源**：2021-2026年政府工作报告、国家统计局  
**制作者**：小金专属龙虾 🦞
