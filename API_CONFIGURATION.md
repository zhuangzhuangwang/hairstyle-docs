# Mintlify API 配置说明

本文档说明了如何配置Mintlify的"Try It"功能，使其能够正确处理API密钥和表单参数。

## 配置概述

根据[Mintlify官方文档](https://mintlify.com/docs)，我们使用了正确的配置方式来启用API的"Try It"功能：

### 1. 主要配置文件

#### `mint.json`
- **Mintlify主配置**: 使用标准的Mintlify配置文件
- **API基础配置**: 设置API基础URL和认证方式
- **导航结构**: 定义文档的导航和分组

#### API文档文件
每个API文档文件（如`hairstyle-editor-pro.mdx`）都包含：
- **API端点定义**: 使用`api: "POST /endpoint"`格式
- **Field组件**: 使用`<Field>`组件定义参数
- **示例代码**: 多种编程语言的调用示例

## 配置详解

### API基础配置

```json
{
  "api": {
    "baseUrl": "https://api.ailabtools.com/v1",
    "auth": {
      "type": "bearer",
      "name": "Authorization"
    }
  }
}
```

这个配置告诉Mintlify：
- API的基础URL是`https://api.ailabtools.com/v1`
- 使用Bearer Token认证
- 认证头名称为`Authorization`

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

## Try It 功能特性

### 1. API密钥管理
- 用户可以在Try It界面中输入API密钥
- 自动添加Bearer前缀
- 安全的密钥存储（仅在浏览器中）

### 2. 参数输入
- 自动生成表单字段
- 必填参数验证
- 文本输入支持
- 参数描述显示

### 3. 请求构建
- 自动构建完整的请求URL
- 正确设置请求头
- JSON格式的请求体

### 4. 响应展示
- 格式化的JSON响应
- 状态码显示
- 错误信息展示

## 使用指南

### 对于开发者

1. **获取API密钥**
   - 访问 [AILabTools控制台](https://console.ailabtools.com)
   - 生成新的API密钥

2. **使用Try It功能**
   - 在API文档页面点击"Try It"
   - 输入您的API密钥（不需要添加Bearer前缀）
   - 填写必要的参数
   - 点击"Send"发送请求

3. **查看响应**
   - 查看实时响应结果
   - 分析响应状态和内容
   - 复制响应数据用于开发

### 对于文档维护者

1. **添加新的API端点**
   - 创建新的MDX文件
   - 使用正确的frontmatter格式
   - 使用`<Field>`组件定义参数

2. **更新现有API**
   - 修改参数定义
   - 更新示例代码
   - 确保描述准确

3. **测试配置**
   - 验证Try It功能正常工作
   - 检查参数验证是否正确
   - 确认示例数据有效

## 配置示例

### 完整的API文档示例

```mdx
---
title: 发型编辑Pro
api: "POST /hairstyle-editor-pro"
description: 编辑人像图片中的发型和颜色
---

# 发型编辑Pro

基于稳定扩散模型，智能编辑人像图片中的发型和颜色。

<RequestExample>
```bash
curl -X POST https://api.ailabtools.com/v1/hairstyle-editor-pro \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "image": "data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQ...",
    "hairstyle": "short",
    "hair_color": "black"
  }'
```
</RequestExample>

<ResponseExample>
```json
{
  "request_id": "req_123456789",
  "log_id": "log_987654321",
  "error_code": 0,
  "result": {
    "task_id": "task_abcdef123456"
  }
}
```
</ResponseExample>

## 请求参数

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
- `mint.json`中的API配置是否正确
- API端点路径是否正确
- 参数定义是否使用了`<Field>`组件

### Q: 如何添加新的API端点？
A: 按以下步骤操作：
1. 创建新的MDX文件
2. 使用正确的frontmatter格式
3. 使用`<Field>`组件定义参数
4. 在`mint.json`的导航中添加新页面

### Q: 如何自定义认证方式？
A: 修改`mint.json`中的`api.auth`部分：
```json
{
  "api": {
    "auth": {
      "type": "basic",  // 或其他认证方式
      "name": "Authorization"
    }
  }
}
```

### Q: 参数输入框没有显示？
A: 确保：
- 使用了`<Field>`组件而不是表格
- 参数名称正确
- 类型定义正确

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
