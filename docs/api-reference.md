# API reference

This page summarizes request fields for this repository's routes. The Muapi live model page and OpenAPI schema take precedence if a route changes.

## Authentication and base URL

- Base URL: https://api.muapi.ai/api/v1
- Send your key in the x-api-key header.
- Send JSON with Content-Type: application/json.

## Async request lifecycle

1. Submit POST /api/v1/{model-id} with the required prompt and optional route fields.
2. Save the request_id returned by the submit response.
3. Poll GET /api/v1/predictions/{request_id}/result until the status is terminal.
4. On completed, consume the result payload. Handle failed and cancelled separately.

```bash
curl -X POST https://api.muapi.ai/api/v1/deepseek-v4-1-flash-abliterated \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Summarize this proposal and list its assumptions."}'
```

Poll the returned request ID:

```text
GET https://api.muapi.ai/api/v1/predictions/REQUEST_ID/result
```

## Route field matrix

| Route | Required | Optional fields |
|---|---|---|
| <code>deepseek-v4-1-flash-abliterated</code> | prompt | <code>system_prompt</code>, <code>max_tokens</code>, <code>thinking</code> |
| <code>deepseek-r1-llama-70b-abliterated</code> | prompt | <code>system_prompt</code>, <code>max_tokens</code> |
| <code>deepseek-r1-qwen-32b-abliterated</code> | prompt | <code>system_prompt</code>, <code>max_tokens</code> |

## Field details

### DeepSeek V4.1 Flash Abliterated

| Field | Type | Required | Notes |
|---|---|---:|---|
| <code>prompt</code> | string | Yes | Prompt text sent to the model. |
| <code>system_prompt</code> | string | No | Optional system-level instruction. |
| <code>max_tokens</code> | integer | No | Optional output cap; route maximum is 32768. |
| <code>thinking</code> | boolean | No | Optional extended-thinking switch. |

### DeepSeek R1 Distill Llama 70B Abliterated

| Field | Type | Required | Notes |
|---|---|---:|---|
| <code>prompt</code> | string | Yes | Prompt text sent to the model. |
| <code>system_prompt</code> | string | No | Optional system-level instruction. |
| <code>max_tokens</code> | integer | No | Optional output cap; route maximum is 8192. |

### DeepSeek R1 Distill Qwen 32B Abliterated

| Field | Type | Required | Notes |
|---|---|---:|---|
| <code>prompt</code> | string | Yes | Prompt text sent to the model. |
| <code>system_prompt</code> | string | No | Optional system-level instruction. |
| <code>max_tokens</code> | integer | No | Optional output cap; route maximum is 8192. |

## Streaming

Muapi supports Server-Sent Events on supported LLM routes. For routes whose live model page confirms streaming, append /stream to the endpoint and send the same route-specific JSON fields.

```bash
curl -N -X POST https://api.muapi.ai/api/v1/deepseek-v4-1-flash-abliterated/stream \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Write a concise explanation of event-driven systems."}'
```

- [Muapi API reference](https://muapi.ai/docs/api-reference)
- [Muapi streaming guide](https://muapi.ai/docs/streaming)
- [OpenAPI specification](https://api.muapi.ai/openapi.json)
