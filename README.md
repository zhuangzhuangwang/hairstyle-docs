# AI发型设计 API 文档 - Mintlify 测试版本

这是一个基于 Mintlify 的 AI发型设计 API 文档测试版本，展示了如何将现有的 MD 格式文档转换为 Mintlify 格式。

## 文档结构

```
test-docs/
├── mint.json                    # Mintlify 配置文件
├── index.mdx                    # 首页
├── quickstart.mdx               # 快速开始
├── hairstyle-examples.mdx       # 发型示例展示
├── api-playground.mdx           # API体验测试
├── essentials/                  # 基础文档
│   ├── authentication.mdx       # 认证
│   ├── get-api-key.mdx          # 获取API密钥
│   ├── response-description.mdx # 响应说明
│   ├── image-requirements.mdx   # 图片要求
│   ├── error-handling.mdx       # 错误处理
│   ├── best-practices.mdx       # 最佳实践
│   ├── errors.mdx               # 错误代码
│   └── pricing.mdx              # 定价
├── api-reference/               # API参考
│   ├── overview.mdx             # API概览
│   ├── hairstyle-editor-pro.mdx # 发型编辑Pro API（支持Try It）
│   ├── face-analysis.mdx        # 人脸分析API（支持Try It）
│   └── async-task-results.mdx   # 异步任务查询API（支持Try It）
├── hairstyle-editor-pro/        # 发型编辑Pro
│   ├── api.mdx                  # API文档
│   ├── introduction.mdx         # 功能介绍
│   └── guide.mdx                # 使用指南
├── async-task-results/          # 异步任务结果
│   └── api.mdx                  # API文档
├── images/                      # 图片资源
└── logo/                        # Logo资源
```

## 转换内容

### 已转换的文件

1. **api-docs/get-api-key.md** → **essentials/get-api-key.mdx**
2. **api-docs/response-description.md** → **essentials/response-description.mdx**
3. **api-docs/hairstyle-editor-pro/api.md** → **hairstyle-editor-pro/api.mdx**
4. **api-docs/hairstyle-editor-pro/Introduction.md** → **hairstyle-editor-pro/introduction.mdx**
5. **api-docs/hairstyle-editor-pro/guide.md** → **hairstyle-editor-pro/guide.mdx**
6. **api-docs/async-task-results/api.md** → **async-task-results/api.mdx**

### 新增的页面

1. **index.mdx** - 首页，介绍 AI发型设计 API
2. **quickstart.mdx** - 快速开始指南
3. **api-reference/overview.mdx** - API 参考概览
4. **api-reference/hairstyle-editor-pro.mdx** - 发型编辑Pro API（支持Try It）
5. **api-reference/face-analysis.mdx** - 人脸分析API（支持Try It）
6. **api-reference/async-task-results.mdx** - 异步任务查询API（支持Try It）
7. **essentials/authentication.mdx** - 认证说明
8. **essentials/image-requirements.mdx** - 图片要求
9. **essentials/error-handling.mdx** - 错误处理
10. **essentials/best-practices.mdx** - 最佳实践
11. **essentials/errors.mdx** - 错误代码
12. **essentials/pricing.mdx** - 定价说明
13. **hairstyle-examples.mdx** - 发型示例展示
14. **api-playground.mdx** - API体验测试

## 主要改进

### 1. 文档结构优化
- 按照功能模块重新组织文档结构
- 创建清晰的导航层次
- 添加必要的索引页面

### 2. 内容本地化
- 将所有英文内容翻译为中文
- 调整 frontmatter 为中文标题和描述
- 保持技术术语的准确性

### 3. 用户体验提升
- 使用 Mintlify 组件增强视觉效果
- 添加 Tab 切换展示不同内容
- 使用卡片和网格布局优化展示

### 4. 功能完整性
- 保留所有原始内容
- 添加缺失的文档页面
- 完善错误处理和最佳实践

### 5. API 体验测试
- 创建完整的 OpenAPI 规范文件
- 支持 Mintlify 的 "Try It" 功能
- 提供交互式的 API 测试界面
- 支持文件上传和参数配置

## 使用方法

### 1. 本地预览

```bash
cd test-docs
npm install -g @mintlify/cli
mintlify dev
```

### 2. 部署

```bash
mintlify deploy
```

## 转换要点

### 1. 文件重命名
- `.md` → `.mdx`
- 使用 kebab-case 命名
- 保持文件结构清晰

### 2. Frontmatter 调整
```yaml
---
title: '页面标题'
description: '页面描述'
---
```

### 3. 内容处理
- 保留所有原始内容
- 更新图片路径
- 修复内部链接
- 添加中文翻译

### 4. 组件使用
- `<Tabs>` 和 `<Tab>` 用于分类展示
- `<Warning>` 和 `<Tip>` 用于提示信息
- `<Card>` 和 `<Grid>` 用于布局优化

### 5. API 体验测试配置
- 创建 `openapi.json` 规范文件
- 在 `mint.json` 中配置 API 认证
- 在 MDX 文件中使用 `openapi` 字段引用 API
- 支持文件上传和参数验证

## 下一步

1. **测试功能**：验证所有页面正常显示
2. **优化样式**：调整颜色和布局
3. **测试 API 体验**：验证 Try It 功能正常工作
4. **完善内容**：补充更多示例和说明

## 总结

这个测试版本成功展示了如何将现有的 MD 文档转换为 Mintlify 格式，同时：

- ✅ 保留了所有原始内容
- ✅ 优化了文档结构
- ✅ 提升了用户体验
- ✅ 添加了中文支持
- ✅ 使用了现代化组件
- ✅ **支持完整的 API 体验测试功能**

### API 体验测试特色

- **完整的 OpenAPI 规范**：定义了所有 API 端点和参数
- **交互式测试界面**：支持直接在文档中测试 API
- **文件上传支持**：支持图片文件上传测试
- **参数验证**：自动验证参数格式和必填项
- **实时响应**：显示 API 调用的实时结果
- **认证配置**：支持 API Key 认证

可以作为完整的 Mintlify 文档迁移方案参考，特别适合需要 API 体验测试功能的项目。
