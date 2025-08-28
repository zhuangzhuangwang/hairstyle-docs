# Mintlify API 配置说明

本文档说明了如何配置Mintlify的"Try It"功能，使其能够正确处理API密钥和表单参数。

## 当前配置状态

根据[Mintlify官方文档](https://mintlify.com/docs)，我们已经配置了基本的API页面结构，但Try It功能可能需要特定的配置才能正确显示参数录入框。

### 1. 主要配置文件

#### `mint.json`
- **Mintlify主配置**: 使用标准的Mintlify配置文件
- **导航结构**: 定义文档的导航和分组
- **基础设置**: 品牌、颜色、链接等配置

#### API文档文件
每个API文档文件（如`hairstyle-editor-pro.mdx`）都包含：
- **API端点定义**: 使用`api: "POST /endpoint"`格式
- **基础URL配置**: 在frontmatter中指定`baseUrl`
- **参数表格**: 使用表格格式定义参数
- **示例代码**: 多种编程语言的调用示例

## 配置详解

### API端点配置

```yaml
---
title: 发型编辑Pro
api: "POST /hairstyle-editor-pro"
description: 编辑人像图片中的发型和颜色
baseUrl: "https://api.ailabtools.com/v1"
---
```

这个配置：
- 定义了API端点路径
- 指定了HTTP方法
- 提供了API描述
- 设置了基础URL

### 参数定义

```markdown
| 参数名 | 类型 | 必需 | 描述 |
|--------|------|------|------|
| `image` | string | 是 | Base64编码的图片数据，支持PNG、JPG、JPEG格式 |
| `hairstyle` | string | 否 | 发型类型，详见下方发型选项 |
| `hair_color` | string | 否 | 发色，详见下方颜色选项 |
```

这个配置：
- 使用表格格式定义参数
- 指定参数名称、类型和是否必需
- 提供参数描述

## 当前问题分析

### Try It功能不显示参数录入框的可能原因

1. **Mintlify版本问题**
   - 可能需要更新到最新版本的Mintlify
   - 某些功能可能仅在特定版本中可用

2. **配置格式问题**
   - 可能需要使用特定的配置格式
   - 参数定义方式可能需要调整

3. **API页面类型问题**
   - 可能需要将页面标记为特定的API页面类型
   - 可能需要额外的配置来启用Try It功能

## 解决方案

### 方案1: 使用Mintlify的API页面专用配置

尝试在`mint.json`中添加API配置：

```json
{
  "api": {
    "baseUrl": "https://api.ailabtools.com/v1",
    "playground": {
      "enabled": true
    }
  }
}
```

### 方案2: 使用Field组件

尝试在API文档中使用Field组件而不是表格：

```mdx
<Field name="image" type="string" required>
Base64编码的图片数据，支持PNG、JPG、JPEG格式
</Field>

<Field name="hairstyle" type="string">
发型类型，详见下方发型选项
</Field>

<Field name="hair_color" type="string">
发色，详见下方颜色选项
</Field>
```

### 方案3: 使用OpenAPI规范

创建OpenAPI规范文件并在配置中引用：

```yaml
# openapi.yaml
openapi: 3.0.0
info:
  title: AILabTools API
  version: 1.0.0
paths:
  /hairstyle-editor-pro:
    post:
      summary: 发型编辑Pro
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                image:
                  type: string
                  description: Base64编码的图片数据
                hairstyle:
                  type: string
                  description: 发型类型
                hair_color:
                  type: string
                  description: 发色
```

## 使用指南

### 对于开发者

1. **获取API密钥**
   - 访问 [AILabTools控制台](https://console.ailabtools.com)
   - 生成新的API密钥

2. **使用API文档**
   - 查看参数说明和示例代码
   - 参考错误码和处理方式
   - 使用提供的代码示例进行集成

3. **手动测试API**
   - 使用curl命令测试API
   - 使用Postman或其他API测试工具
   - 参考示例代码进行开发

### 对于文档维护者

1. **更新API文档**
   - 修改参数定义
   - 更新示例代码
   - 确保描述准确

2. **测试配置**
   - 验证文档显示正确
   - 检查示例代码可用性
   - 确认错误处理完整

## 常见问题

### Q: Try It功能无法正常工作？
A: 可能的原因：
- Mintlify版本过旧
- 配置格式不正确
- 需要特定的API页面配置

### Q: 如何添加新的API端点？
A: 按以下步骤操作：
1. 创建新的MDX文件
2. 使用正确的frontmatter格式
3. 定义参数表格
4. 在`mint.json`的导航中添加新页面

### Q: 如何配置API认证？
A: 当前配置中，用户需要手动添加Authorization头：
- 格式：`Bearer YOUR_API_KEY`
- 在API调用时手动设置

### Q: 参数输入框没有显示？
A: 可能的原因：
- 需要使用Field组件而不是表格
- 需要特定的Mintlify配置
- 可能需要更新Mintlify版本

## 最佳实践

1. **保持配置一致性**
   - 所有API文档使用相同的格式
   - 参数定义清晰明确
   - 示例代码准确

2. **提供详细说明**
   - 为每个参数提供清晰的描述
   - 包含使用示例和注意事项
   - 说明参数格式要求

3. **错误处理**
   - 提供完整的错误码说明
   - 包含错误处理示例
   - 说明常见问题解决方案

4. **版本管理**
   - 使用语义化版本号
   - 记录API变更历史
   - 保持向后兼容性

## 技术支持

如果您在使用过程中遇到问题，请：
1. 查看[Mintlify官方文档](https://mintlify.com/docs)
2. 检查配置文件的语法正确性
3. 联系技术支持团队

---

*最后更新: 2024年12月*
