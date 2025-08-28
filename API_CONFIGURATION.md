# Mintlify API 配置说明

本文档说明了如何配置Mintlify的"Try It"功能，使其能够正确处理API密钥和表单参数。

## 配置概述

根据[Mintlify API Playground文档](https://mintlify.com/docs/api-playground/overview)，我们使用了正确的配置方式来启用API的"Try It"功能：

### 1. 主要配置文件

#### `mint.json`
- **Mintlify主配置**: 使用标准的Mintlify配置文件
- **OpenAPI引用**: 通过`openapi`属性引用OpenAPI规范文件
- **API Playground配置**: 启用交互式API测试功能

#### `openapi.json`
- **OpenAPI规范**: 包含所有API端点的完整定义
- **异步API支持**: 正确定义异步API的请求和响应格式
- **参数定义**: 详细的请求参数和响应参数说明

## 配置详解

### OpenAPI规范配置

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "AILabTools API",
    "version": "1.0.0",
    "description": "基于稳定扩散模型的发型编辑Pro功能API"
  },
  "servers": [
    {
      "url": "https://api.ailabtools.com/v1",
      "description": "生产环境"
    }
  ]
}
```

### 导航配置

```json
{
  "navigation": [
    {
      "group": "API参考",
      "openapi": "openapi.json"
    }
  ]
}
```

这个配置告诉Mintlify：
- 自动从OpenAPI规范生成API页面
- 为每个端点创建交互式Playground
- 生成参数录入框和示例代码

### API Playground配置

```json
{
  "api": {
    "playground": {
      "display": "interactive"
    },
    "examples": {
      "languages": ["curl", "python", "javascript"],
      "defaults": "required"
    }
  }
}
```

这个配置：
- 启用交互式API Playground
- 生成多种编程语言的示例代码
- 只显示必需参数（减少复杂性）

## 异步API配置

### 异步API特点

我们的API采用异步处理模式：
1. **提交任务**: 调用API提交处理请求，返回`task_id`
2. **查询结果**: 使用`task_id`查询处理结果
3. **状态轮询**: 定期查询直到任务完成

### OpenAPI中的异步API定义

```json
{
  "/hairstyle-editor-pro": {
    "post": {
      "summary": "发型编辑Pro",
      "description": "基于稳定扩散模型，智能编辑人像图片中的发型和颜色",
      "requestBody": {
        "required": true,
        "content": {
          "application/json": {
            "schema": {
              "type": "object",
              "required": ["image"],
              "properties": {
                "image": {
                  "type": "string",
                  "format": "byte",
                  "description": "Base64编码的图片数据"
                },
                "hairstyle": {
                  "type": "string",
                  "enum": ["short", "medium", "long", ...],
                  "description": "发型类型"
                },
                "hair_color": {
                  "type": "string",
                  "enum": ["black", "brown", "blonde", ...],
                  "description": "发色"
                }
              }
            }
          }
        }
      },
      "responses": {
        "200": {
          "description": "请求成功",
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "result": {
                    "type": "object",
                    "properties": {
                      "task_id": {
                        "type": "string",
                        "description": "异步任务ID，用于查询处理结果"
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

## Try It 功能特性

### 1. 自动生成的参数录入框
- 基于OpenAPI规范自动生成
- 支持必填参数验证
- 提供参数描述和示例值

### 2. 交互式API测试
- 实时发送API请求
- 显示响应结果
- 支持错误处理

### 3. 多语言示例代码
- 自动生成curl、Python、JavaScript示例
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

1. **更新API定义**
   - 修改`openapi.json`文件
   - 更新参数定义和响应格式
   - 确保OpenAPI规范有效

2. **添加新的API端点**
   - 在OpenAPI规范中添加新的路径
   - 定义请求和响应模式
   - Mintlify会自动生成页面

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
      "openapi": "openapi.json"
    }
  ],
  "api": {
    "playground": {
      "display": "interactive"
    },
    "examples": {
      "languages": ["curl", "python", "javascript"],
      "defaults": "required"
    }
  }
}
```

### 异步API的OpenAPI定义

```json
{
  "paths": {
    "/hairstyle-editor-pro": {
      "post": {
        "summary": "发型编辑Pro",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": ["image"],
                "properties": {
                  "image": {
                    "type": "string",
                    "format": "byte",
                    "description": "Base64编码的图片数据"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "请求成功",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "result": {
                      "type": "object",
                      "properties": {
                        "task_id": {
                          "type": "string",
                          "description": "异步任务ID"
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

## 常见问题

### Q: Try It功能无法正常工作？
A: 检查以下配置：
- OpenAPI规范文件是否有效
- `mint.json`中的`openapi`引用是否正确
- API Playground是否设置为`"interactive"`

### Q: 如何添加新的API端点？
A: 按以下步骤操作：
1. 在`openapi.json`中添加新的路径定义
2. 定义请求和响应模式
3. Mintlify会自动生成对应的页面

### Q: 如何配置API认证？
A: 在OpenAPI规范中添加安全定义：
```json
{
  "components": {
    "securitySchemes": {
      "bearerAuth": {
        "type": "http",
        "scheme": "bearer"
      }
    }
  },
  "security": [
    {
      "bearerAuth": []
    }
  ]
}
```

### Q: 参数录入框没有显示？
A: 确保：
- OpenAPI规范中的参数定义正确
- 使用了正确的数据类型和格式
- API Playground设置为`"interactive"`

### Q: 如何处理异步API？
A: 异步API需要：
1. 正确定义请求和响应格式
2. 在响应中包含`task_id`
3. 提供查询任务状态的API端点
4. 在文档中说明轮询机制

## 最佳实践

1. **保持OpenAPI规范更新**
   - 及时更新API定义
   - 确保参数和响应格式准确
   - 提供完整的示例数据

2. **异步API文档**
   - 清楚说明异步处理流程
   - 提供轮询示例代码
   - 说明错误处理方式

3. **参数验证**
   - 使用枚举值限制选项
   - 提供清晰的参数描述
   - 包含格式要求说明

4. **错误处理**
   - 定义完整的错误响应
   - 提供错误码说明
   - 包含错误处理示例

## 技术支持

如果您在使用过程中遇到问题，请：
1. 查看[Mintlify API Playground文档](https://mintlify.com/docs/api-playground/overview)
2. 验证OpenAPI规范的有效性
3. 联系技术支持团队

---

*最后更新: 2024年12月*
