# AILabTools API 文档 - Mintlify版本

这是专门为Mintlify平台准备的AILabTools API文档，可以直接部署到Mintlify使用。

## 📁 目录结构

```
mintlify-docs/
├── docs.json                    # Mintlify主配置文件
├── index.mdx                    # 首页
├── quickstart.mdx               # 快速开始
├── development.mdx              # 开发指南
├── api-reference/               # API参考
│   ├── _meta.json              # API导航配置
│   ├── overview.mdx            # API概览
│   ├── hairstyle-editor-pro.mdx # 发型编辑Pro
│   ├── async-task-results.mdx  # 异步任务查询
│   └── face-analysis.mdx       # 人脸分析
├── essentials/                  # 基础指南
│   ├── _meta.json              # 指南导航配置
│   ├── authentication.mdx      # 认证方式
│   ├── image-requirements.mdx  # 图片要求
│   ├── error-handling.mdx      # 错误处理
│   ├── best-practices.mdx      # 最佳实践
│   ├── errors.mdx              # 错误码
│   └── pricing.mdx             # 价格说明
├── snippets/                    # 代码片段
│   ├── _meta.json              # 片段导航配置
│   └── javascript.mdx          # JavaScript代码
├── images/                      # 图片资源
├── logo/                        # Logo资源
└── favicon.svg                  # 网站图标
```

## 🚀 快速部署

### 1. 安装Mintlify CLI

```bash
npm install -g mintlify
```

### 2. 进入文档目录

```bash
cd mintlify-docs
```

### 3. 本地预览

```bash
mintlify dev
```

### 4. 部署到Mintlify

```bash
mintlify deploy
```

## 📝 文档内容

### 首页 (`index.mdx`)
- 产品介绍和功能展示
- 快速导航卡片
- 技术特点说明

### 快速开始 (`quickstart.mdx`)
- 5分钟上手指南
- 多语言代码示例
- 常见问题解答

### API参考
- **API概览** (`api-reference/overview.mdx`): 基础信息和快速开始
- **发型编辑Pro** (`api-reference/hairstyle-editor-pro.mdx`): 核心API文档
- **异步任务查询** (`api-reference/async-task-results.mdx`): 异步处理API
- **人脸分析** (`api-reference/face-analysis.mdx`): 验证API

### 基础指南
- **认证方式** (`essentials/authentication.mdx`): API密钥管理
- **图片要求** (`essentials/image-requirements.mdx`): 图片规范
- **错误处理** (`essentials/error-handling.mdx`): 错误处理指南
- **最佳实践** (`essentials/best-practices.mdx`): 使用最佳实践
- **错误码** (`essentials/errors.mdx`): 完整错误码列表
- **价格说明** (`essentials/pricing.mdx`): 定价方案

### 开发指南 (`development.mdx`)
- 多平台集成方案
- React、Vue、Node.js、Python集成
- 开发工具和配置

### 代码片段 (`snippets/`)
- 可复用的代码示例
- 多种编程语言支持

## ⚙️ 配置说明

### docs.json 配置

主要配置项：
- `name`: 文档名称
- `colors`: 主题色彩配置
- `navigation`: 导航结构
- `topbarLinks`: 顶部链接
- `anchors`: 侧边锚点
- `footerSocials`: 底部社交链接

### 自定义配置

1. **修改主题色彩**:
```json
{
  "colors": {
    "primary": "#667eea",
    "light": "#764ba2",
    "dark": "#4c63d2"
  }
}
```

2. **添加自定义域名**:
```json
{
  "cname": "docs.ailabtools.com"
}
```

3. **配置分析工具**:
```json
{
  "analytics": {
    "posthog": {
      "apiKey": "YOUR_POSTHOG_API_KEY"
    }
  }
}
```

## 🎨 自定义样式

Mintlify支持以下自定义组件：

### 基础组件
- `<Note>` - 提示信息
- `<Warning>` - 警告信息
- `<Tip>` - 小贴士
- `<CTA>` - 行动号召按钮

### 布局组件
- `<Grid>` - 网格布局
- `<Card>` - 卡片组件
- `<Hero>` - 英雄区域
- `<Accordion>` - 手风琴组件

### API组件
- `<RequestExample>` - 请求示例
- `<ResponseExample>` - 响应示例
- `<Tabs>` - 标签页

## 📱 响应式支持

文档自动支持：
- 桌面端完整布局
- 平板端自适应
- 移动端优化显示

## 🔍 搜索功能

配置了全文搜索，支持：
- API端点搜索
- 代码示例搜索
- 错误码搜索
- 指南内容搜索

## 🚀 部署选项

### 1. Vercel部署
1. 将代码推送到GitHub
2. 在Vercel中导入项目
3. 设置构建命令：`mintlify build`
4. 设置输出目录：`mintlify`
5. 部署

### 2. 自定义域名
在 `docs.json` 中配置：
```json
{
  "cname": "docs.ailabtools.com"
}
```

## 📞 支持

如有问题，请联系：
- 邮箱: support@ailabtools.com
- 官网: https://www.ailabtools.com

## 📄 许可证

MIT License
