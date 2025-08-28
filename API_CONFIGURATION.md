# Mintlify API 配置说明

本文档说明了如何配置Mintlify的"Try It"功能，使其能够正确处理API密钥和表单参数。

## 配置概述

根据Mintlify的文档和实际测试，我们采用了MDX API页面配置方式，这是目前最稳定和可靠的配置方法：

### 1. 主要配置文件

#### `mint.json`
- **Mintlify主配置**: 使用标准的Mintlify配置文件
- **导航结构**: 定义文档的导航和分组
- **基础设置**: 品牌、颜色、链接等配置

#### API文档文件
每个API文档文件（如`hairstyle-editor-pro.mdx`）都包含：
- **API端点定义**: 使用`api: "POST /endpoint"`格式
- **参数定义**: 使用`<Field>`组件定义参数
- **示例代码**: 多种编程语言的调用示例
- **详细说明**: 参数要求、错误处理等

## 配置详解

### API端点配置

```yaml
---
title: 发型编辑Pro
api: "POST /hairstyle-editor-pro"
description: 编辑人像图片中的发型和颜色
---
```

这个配置：
- 定义了API端点路径
- 指定了HTTP方法
- 提供了API描述
- 启用了Try It功能

### 参数定义

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

这个配置：
- 使用`<Field>`组件定义参数
- 指定参数名称、类型和是否必需
- 提供参数描述
- 自动生成参数录入框

## 异步API配置

### 异步API特点

我们的API采用异步处理模式：
1. **提交任务**: 调用API提交处理请求，返回`task_id`
2. **查询结果**: 使用`task_id`查询处理结果
3. **状态轮询**: 定期查询直到任务完成

### MDX中的异步API定义

```mdx
---
title: 异步任务查询
api: "GET /async-task-results"
description: 查询异步任务的处理结果
---

<Field name="task_id" type="string" required>
异步任务ID，从其他API响应中获取
</Field>
```

## Try It 功能特性

### 1. 自动生成的参数录入框
- 基于`<Field>`组件自动生成
- 支持必填参数验证
- 提供参数描述和类型检查

### 2. 交互式API测试
- 实时发送API请求
- 显示响应结果
- 支持错误处理

### 3. 多语言示例代码
- 提供curl、Python、JavaScript示例
- 包含正确的参数格式
- 提供完整的请求示例

### 4. 异步API支持
- 正确处理异步API的请求/响应
- 提供任务ID查询功能
- 支持状态轮询说明

## 使用指南

### 对于开发者

1. **获取API密钥**
   - 访问 [AILabTools控制台](https://console.ailabtools.com)
   - 生成新的API密钥

2. **使用Try It功能**
   - 在API文档页面点击"Try It"
   - 输入您的API密钥
   - 填写必要的参数（image为必填）
   - 点击"Send"发送请求
   - 查看响应结果

3. **处理异步响应**
   - 获取返回的`task_id`
   - 使用异步任务查询API检查状态
   - 轮询直到任务完成

### 对于文档维护者

1. **更新API文档**
   - 修改对应的MDX文件
   - 更新参数定义和响应格式
   - 确保`<Field>`组件配置正确

2. **添加新的API端点**
   - 创建新的MDX文件
   - 使用正确的frontmatter格式
   - 定义`<Field>`组件参数
   - 在`mint.json`的导航中添加新页面

3. **测试配置**
   - 验证Try It功能正常工作
   - 检查参数验证是否正确
   - 确认示例代码可用

## 配置示例

### 完整的mint.json配置

```json
{
  "$schema": "https://mintlify.com/schema.json",
  "name": "AILabTools API",
  "navigation": [
    {
      "group": "API参考",
      "pages": [
        "api-reference/overview",
        "api-reference/hairstyle-editor-pro",
        "api-reference/async-task-results",
        "api-reference/face-analysis"
      ]
    }
  ]
}
```

### API页面的MDX配置

```mdx
---
title: 发型编辑Pro
api: "POST /hairstyle-editor-pro"
description: 编辑人像图片中的发型和颜色
---

# 发型编辑Pro

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

## 常见问题

### Q: Try It功能无法正常工作？
A: 检查以下配置：
- MDX文件中的`api`字段格式是否正确
- `<Field>`组件是否正确定义
- 参数类型和必需性是否正确设置

### Q: 如何添加新的API端点？
A: 按以下步骤操作：
1. 创建新的MDX文件
2. 使用正确的frontmatter格式
3. 使用`<Field>`组件定义参数
4. 在`mint.json`的导航中添加新页面

### Q: 如何配置API认证？
A: 当前配置中，用户需要手动添加Authorization头：
- 格式：`Bearer YOUR_API_KEY`
- 在API调用时手动设置

### Q: 参数录入框没有显示？
A: 确保：
- 使用了`<Field>`组件而不是表格
- 参数类型和名称正确
- MDX文件的frontmatter格式正确

### Q: 如何处理异步API？
A: 异步API需要：
1. 正确定义请求和响应格式
2. 在响应中包含`task_id`
3. 提供查询任务状态的API端点
4. 在文档中说明轮询机制

## 最佳实践

1. **保持配置一致性**
   - 所有API文档使用相同的格式
   - 参数定义清晰明确
   - 示例代码准确

2. **提供详细说明**
   - 为每个参数提供清晰的描述
   - 包含使用示例和注意事项
   - 说明参数格式要求

3. **异步API文档**
   - 清楚说明异步处理流程
   - 提供轮询示例代码
   - 说明错误处理方式

4. **错误处理**
   - 提供完整的错误码说明
   - 包含错误处理示例
   - 说明常见问题解决方案

## 技术支持

如果您在使用过程中遇到问题，请：
1. 查看[Mintlify官方文档](https://mintlify.com/docs)
2. 检查配置文件的语法正确性
3. 联系技术支持团队

---

*最后更新: 2024年12月*
