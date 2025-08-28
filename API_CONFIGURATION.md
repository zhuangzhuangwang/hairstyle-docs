# Mintlify API 配置说明

本文档说明了如何配置Mintlify的"Try It"功能，使其能够正确处理API密钥和表单参数。

## 配置概述

为了确保Mintlify的"Try It"功能正常工作，我们进行了以下配置：

### 1. 主要配置文件

#### `docs.json`
- **API基础配置**: 设置API基础URL和认证方式
- **Try It配置**: 启用Try It功能并设置默认值
- **OpenAPI规范引用**: 指向统一的OpenAPI规范文件

#### `api-reference/openapi.yaml`
- **统一OpenAPI规范**: 包含所有API端点的完整定义
- **认证方案**: Bearer Token认证配置
- **请求/响应模式**: 详细的数据结构定义
- **示例数据**: 多种场景的请求和响应示例

### 2. 各API文档文件

每个API文档文件（如`hairstyle-editor-pro.mdx`）都包含：
- **OpenAPI规范**: 在frontmatter中定义的完整OpenAPI配置
- **认证要求**: 明确指定需要Bearer Token认证
- **参数定义**: 详细的请求参数和响应参数说明
- **示例代码**: 多种编程语言的调用示例

## 配置详解

### API认证配置

```yaml
components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
      description: "请输入您的API密钥，格式为 sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

这个配置告诉Mintlify：
- 使用Bearer Token认证
- 在Try It界面中显示API密钥输入框
- 提供清晰的格式说明

### 请求参数配置

```yaml
HairstyleEditorRequest:
  type: object
  required:
    - image
  properties:
    image:
      type: string
      format: byte
      description: "Base64编码的图片数据"
    hairstyle:
      type: string
      enum: ["short", "medium", "long", ...]
      description: "发型类型"
    hair_color:
      type: string
      enum: ["black", "brown", "blonde", ...]
      description: "发色"
```

这个配置确保：
- 必填参数（image）被正确标记
- 可选参数有明确的枚举值
- 参数类型和格式被正确定义

### 响应示例配置

```yaml
responses:
  "200":
    description: "请求成功"
    content:
      application/json:
        schema:
          $ref: "#/components/schemas/HairstyleEditorResponse"
        examples:
          success:
            summary: "成功响应"
            value:
              request_id: "req_123456789"
              error_code: 0
              result:
                task_id: "task_abcdef123456"
```

这个配置提供：
- 成功响应的示例
- 错误响应的示例
- 不同状态码的详细说明

## Try It 功能特性

### 1. API密钥管理
- 用户可以在Try It界面中输入API密钥
- 密钥格式验证和提示
- 安全的密钥存储（仅在浏览器中）

### 2. 参数输入
- 自动生成表单字段
- 必填参数验证
- 枚举值下拉选择
- 文件上传支持（Base64编码）

### 3. 请求示例
- 多种预设示例
- 一键切换不同场景
- 实时参数预览

### 4. 响应展示
- 格式化的JSON响应
- 状态码说明
- 错误信息展示

## 使用指南

### 对于开发者

1. **获取API密钥**
   - 访问 [AILabTools控制台](https://console.ailabtools.com)
   - 生成新的API密钥

2. **使用Try It功能**
   - 在API文档页面点击"Try It"
   - 输入您的API密钥
   - 填写必要的参数
   - 点击"Send"发送请求

3. **查看响应**
   - 查看实时响应结果
   - 分析响应状态和内容
   - 复制响应数据用于开发

### 对于文档维护者

1. **更新API配置**
   - 修改`api-reference/openapi.yaml`文件
   - 更新相应的MDX文档文件
   - 确保配置一致性

2. **添加新的API端点**
   - 在OpenAPI规范中添加新的路径
   - 定义请求和响应模式
   - 创建对应的MDX文档

3. **测试配置**
   - 验证Try It功能正常工作
   - 检查参数验证是否正确
   - 确认示例数据有效

## 常见问题

### Q: Try It功能无法正常工作？
A: 检查以下配置：
- API密钥格式是否正确
- 必填参数是否已填写
- 网络连接是否正常
- 服务器是否可访问

### Q: 如何添加新的API端点？
A: 按以下步骤操作：
1. 在`openapi.yaml`中添加新的路径定义
2. 创建对应的MDX文档文件
3. 在`docs.json`的导航中添加新页面
4. 测试Try It功能

### Q: 如何自定义认证方式？
A: 修改`openapi.yaml`中的`securitySchemes`部分：
```yaml
components:
  securitySchemes:
    YourAuth:
      type: http
      scheme: basic  # 或其他认证方式
```

## 最佳实践

1. **保持配置一致性**
   - OpenAPI规范和MDX文档保持一致
   - 示例数据与实际API响应一致

2. **提供详细说明**
   - 为每个参数提供清晰的描述
   - 包含使用示例和注意事项

3. **错误处理**
   - 定义完整的错误响应
   - 提供有意义的错误信息

4. **版本管理**
   - 使用语义化版本号
   - 记录API变更历史

## 技术支持

如果您在使用过程中遇到问题，请：
1. 查看本文档的常见问题部分
2. 检查配置文件的语法正确性
3. 联系技术支持团队

---

*最后更新: 2024年12月*
