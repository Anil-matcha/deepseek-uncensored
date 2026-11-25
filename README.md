# DeepSeek V4.1 Flash Abliterated API with Muapi

This repository uses the requested short name, **deepseek-uncensored**, for a Muapi-focused developer guide. Muapi provides a DeepSeek V4.1 Flash Abliterated endpoint that may reduce refusals; it does not guarantee unrestricted output. This guide also compares that text-only route with Muapi's standard multimodal DeepSeek V4.1 Flash endpoint.

## Related Projects

- [Muapi Uncensored AI API guide](https://github.com/Anil-matcha/Uncensored-AI-API) — setup and examples for Muapi's abliterated LLM endpoints.
- [Awesome Abliterated LLMs](https://github.com/Anil-matcha/awesome-abliterated-llms) — model comparisons, access notes, and evaluation guidance.
- [Open Generative AI](https://github.com/Anil-matcha/Open-Generative-AI) — a creative AI workspace that connects to Muapi.

## Muapi routes

| Route | Inputs and controls | Notes |
|---|---|---|
| **deepseek-v4-1-flash** | **prompt**, optional **image_url**, **system_prompt**, and **reasoning_effort** | Standard route; accepts image URLs and offers configurable reasoning effort. |
| **deepseek-v4-1-flash-abliterated** | **prompt**, optional **system_prompt**, **max_tokens** (up to 32,768), and **thinking** | Abliterated route; text input only. The modified model may reduce refusals, but does not guarantee unrestricted output. |

Both routes support a 1M-token context window and asynchronous submission. Each has an SSE streaming endpoint ending in **/stream**. The standard model accepts **reasoning_effort**: **none**, **minimal**, **low**, **medium**, **high**, **xhigh**, or **max**. The abliterated model uses a boolean **thinking** control instead.

The standard route follows DeepSeek's published peak/off-peak and cached-input rates ([official pricing](https://api-docs.deepseek.com/quick_start/pricing/)). The abliterated route's current Muapi catalog lists **$0.66 per million input tokens** and **$2.64 per million output tokens**. Rates can change; use the live [DeepSeek V4.1 Flash playground](https://muapi.ai/playground/deepseek-v4-1-flash) and [abliterated LLM API page](https://muapi.ai/abliterated-llm-api) to confirm current availability and pricing. Muapi returns the actual charge with each request/result.

## Quick start

Create a key at [Muapi API Keys](https://muapi.ai/access-keys), then:

~~~bash
export MUAPI_KEY="your-muapi-key"
~~~

Submit to the standard multimodal route:

~~~bash
curl -X POST https://api.muapi.ai/api/v1/deepseek-v4-1-flash \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Summarize the main point of this image.",
    "image_url": "https://example.com/image.jpg",
    "reasoning_effort": "medium"
  }'
~~~

To use the text-only abliterated route, submit to its separate endpoint:

~~~bash
curl -X POST https://api.muapi.ai/api/v1/deepseek-v4-1-flash-abliterated \
  -H "x-api-key: $MUAPI_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Explain the trade-offs between a monolith and microservices.",
    "max_tokens": 4096,
    "thinking": true
  }'
~~~

Both submit responses include a **request_id**. Poll the result:

~~~bash
curl "https://api.muapi.ai/api/v1/predictions/REQUEST_ID/result" \
  -H "x-api-key: $MUAPI_KEY"
~~~

For live SSE output, use the route's **/stream** suffix and **curl -N**.

## Python example

Requires Python 3.9+ and **requests**. Choose a route with **--abliterated**; add **--image-url** only for the standard route.

~~~bash
python -m pip install -r requirements.txt
python examples/submit.py "Explain how a mixture-of-experts model works."
python examples/submit.py --abliterated "Summarize this algorithm and its trade-offs." --thinking
~~~

## Links

- [DeepSeek V4.1 Flash on Muapi](https://muapi.ai/playground/deepseek-v4-1-flash)
- [DeepSeek V4.1 Flash Abliterated on Muapi](https://muapi.ai/playground/deepseek-v4-1-flash-abliterated)
- [Muapi API reference](https://muapi.ai/docs/api-reference)
- [Create or manage an API key](https://muapi.ai/access-keys)
- [Muapi](https://muapi.ai)

Model availability, request fields, and prices can change. This guide reflects the Muapi catalog checked on 2026-11-25; the live Muapi pages are authoritative.
