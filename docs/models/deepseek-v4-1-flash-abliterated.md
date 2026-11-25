# DeepSeek V4.1 Flash Abliterated on Muapi

A long-context Flash endpoint with an optional thinking control. The request schema exposes text prompts and does not expose a tools array.

| Catalog detail | Value |
|---|---|
| Muapi endpoint | <code>deepseek-v4-1-flash-abliterated</code> |
| Context shown in Muapi catalog | 1M tokens |
| Input | Text |
| Input price | $0.66 per million tokens |
| Output price | $2.64 per million tokens |
| Maximum output tokens in current schema | 32768 |

## When to consider this route

Choose for long-context prompts when you want the newer Flash route and an optional thinking switch.

Context is the advertised total input window; max_tokens separately limits generated output. The live Muapi model page is the source of truth if a schema or price changes.

## Request fields

| Field | Type | Required | Notes |
|---|---|---:|---|
| <code>prompt</code> | string | Yes | Prompt text sent to the model. |
| <code>system_prompt</code> | string | No | Optional system-level instruction. |
| <code>max_tokens</code> | integer | No | Optional output cap; route maximum is 32768. |
| <code>thinking</code> | boolean | No | Optional extended-thinking switch. |

The input object requires prompt. Other fields listed above are optional in the current schema. Include image_url only when this route lists Text + image.

## Submit and poll

Set MUAPI_KEY, submit to the endpoint, save the returned request ID, then poll the result endpoint:

```bash
curl -X POST https://api.muapi.ai/api/v1/deepseek-v4-1-flash-abliterated \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Summarize the design trade-offs in this proposal.", "system_prompt": "Be concise and separate facts from assumptions.", "max_tokens": 1024, "thinking": true}'

curl "https://api.muapi.ai/api/v1/predictions/REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_KEY"
```

The submit response contains a request_id. Poll until the job reaches a terminal status and inspect the returned result payload. Handle failed and cancelled separately from completed.

## Streaming

Muapi provides streaming on supported text-generation endpoints. Use POST /api/v1/deepseek-v4-1-flash-abliterated/stream when the live model page confirms streaming for this route. See the [Muapi streaming guide](https://muapi.ai/docs/streaming) and this repository's [streaming example](../../examples/stream.py).

## Pricing

Muapi's catalog currently lists $0.66/M input tokens and $2.64/M output tokens. Actual charge depends on request usage. Verify the live [Muapi catalog](https://muapi.ai/abliterated-llm-api) before budgeting.

## Links

- [Muapi model page](https://muapi.ai/abliterated-llm-api)
- [Muapi API reference](https://muapi.ai/docs/api-reference)
- [Family selection guide](../model-selection.md)
