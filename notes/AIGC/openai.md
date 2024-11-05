# OpenAI使用

## 认证

OpenAI API采用API密钥机制进行身份验证，以确保访问的安全性和权限的控制。API密钥分为两个层级：`项目密钥`和`用户密钥`。每个层级的API密钥具有不同的权限范围和作用域，具体如下：

- 项目密钥：提供对单个项目的访问（**官方推荐**）。

- 用户密钥：提供对用户已添加到的所有组织和所有项目的访问。



所有API请求都应在`授权`HTTP标头中包含您的API密钥，如下所示：

```http
Authorization: Bearer OPENAI_API_KEY
```



## 第一个请求

基于项目的密钥发送第一个请求:

```shell
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
     "model": "gpt-4o-mini",
     "messages": [{"role": "user", "content": "Hello World!"}],
     "temperature": 0.7
   }'
```

> 如果使用旧版用户密钥且有多个项目，HTTP请求头需要设置[项目ID](https://platform.openai.com/docs/api-reference/authentication)如下：
> 
> ```http
> OpenAI-Organization: org-RV6wQKGeHBTR1scNzuHyi82u
> ```



响应：

```json
{
  "id": "chatcmpl-AQ465RLBXWm6AsXtDlm5x09rCkHIN",
  "object": "chat.completion",
  "created": 1730775641,
  "model": "gpt-4o-mini-2024-07-18",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Hello! How can I assist you today?",
        "refusal": null
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 10,
    "completion_tokens": 9,
    "total_tokens": 19,
    "prompt_tokens_details": {
      "cached_tokens": 0
    },
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  },
  "system_fingerprint": "fp_0ba0d124f1"
}
```


