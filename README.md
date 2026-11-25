# DeepSeek Abliterated API with Muapi

Compare Muapi-hosted DeepSeek R1 distilled baselines and DeepSeek V4.1 Flash Abliterated through one API key.

This guide covers two DeepSeek R1 distilled derivatives and the DeepSeek V4.1 Flash Abliterated route. These are hosted API endpoints; this repository does not distribute model weights.

Muapi uses labels such as abliterated, obliterated, or derestricted for some routes. Those labels describe a model or endpoint; they do not guarantee a response or change Muapi's acceptable-use policy.

## Choose a model

| Muapi model | Context | Input | Input / output per 1M tokens | Output cap | Guide |
|---|---:|---|---:|---:|---|
| DeepSeek V4.1 Flash Abliterated (<code>deepseek-v4-1-flash-abliterated</code>) | 1M | Text | $0.66 / $2.64 | 32768 | [Details](docs/models/deepseek-v4-1-flash-abliterated.md) |
| DeepSeek R1 Distill Llama 70B Abliterated (<code>deepseek-r1-llama-70b-abliterated</code>) | 16K | Text | $1.40 / $1.40 | 8192 | [Details](docs/models/deepseek-r1-llama-70b-abliterated.md) |
| DeepSeek R1 Distill Qwen 32B Abliterated (<code>deepseek-r1-qwen-32b-abliterated</code>) | 16K | Text | $2.80 / $2.80 | 8192 | [Details](docs/models/deepseek-r1-qwen-32b-abliterated.md) |

Catalog rates and availability can change. Prices shown here reflect the Muapi catalog checked on 2026-11-25; verify the live page before production budgeting.

## Quick start

Create a key in the [Muapi dashboard](https://muapi.ai/access-keys), then set it in your shell:

```bash
export MUAPI_KEY='your-muapi-key'
```

Submit a prompt to the first route:

```bash
curl -X POST https://api.muapi.ai/api/v1/deepseek-v4-1-flash-abliterated \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{"prompt":"Explain the trade-offs in this design and list its assumptions."}'
```

The response contains a request_id. Poll it for the result:

```bash
curl "https://api.muapi.ai/api/v1/predictions/REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_KEY"
```

Runnable Python examples are in [examples](examples/). They submit a prompt, poll the result, or stream text when the selected route supports streaming. See the [Muapi streaming guide](https://muapi.ai/docs/streaming).

## Documentation

- [Model selection guide](docs/model-selection.md)
- [API reference and request schemas](docs/api-reference.md)
- [Pricing](docs/pricing.md)
- [Operations and error handling](docs/operations.md)
- [FAQ](docs/faq.md)
- [Glossary](docs/glossary.md)
- [Evaluation protocol](docs/evaluation.md)
- [Prompt templates](prompts.md)
- [Documentation index](docs/README.md)

## Muapi links

- [Muapi home](https://muapi.ai)
- [Create or manage an API key](https://muapi.ai/access-keys)
- [Muapi API reference](https://muapi.ai/docs/api-reference)
- [Muapi model catalog](https://muapi.ai/models)
- [Muapi model-family page](https://muapi.ai/deepseek-r1-abliterated-api)

This repository documents hosted Muapi routes. It does not distribute model weights or independently verify model behavior. Use Muapi's live page for current availability, fields, and prices.
