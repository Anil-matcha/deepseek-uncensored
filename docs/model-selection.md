# Choosing a DeepSeek route

This guide covers two DeepSeek R1 distilled derivatives and the DeepSeek V4.1 Flash Abliterated route. These are hosted API endpoints; this repository does not distribute model weights.

## Compare the current routes

| Route | Context | Input | Input / output per 1M tokens | Maximum output | Selection note |
|---|---:|---|---:|---:|---|
| <code>deepseek-v4-1-flash-abliterated</code> | 1M | Text | $0.66 / $2.64 | 32768 | Choose for long-context prompts when you want the newer Flash route and an optional thinking switch. |
| <code>deepseek-r1-llama-70b-abliterated</code> | 16K | Text | $1.40 / $1.40 | 8192 | Choose when you specifically want an R1-distilled Llama 70B baseline. |
| <code>deepseek-r1-qwen-32b-abliterated</code> | 16K | Text | $2.80 / $2.80 | 8192 | Choose when you specifically want an R1-distilled Qwen 32B baseline. |

The table is a shortlist by documented interface, context, and price. It is not a quality ranking.

## A practical selection process

1. Start with input type. Use image_url only on a route whose Muapi schema lists image input.
2. Match the advertised context window to the total prompt size and leave room for the generated answer.
3. Set max_tokens to the output length your task needs; the cap varies by endpoint.
4. Estimate cost from expected input and output token counts using the separate rates.
5. For close choices, run the same prompts on each route and score them against your own criteria. This repository publishes no comparative benchmark scores.

## Model cards

- [DeepSeek V4.1 Flash Abliterated](models/deepseek-v4-1-flash-abliterated.md) — Choose for long-context prompts when you want the newer Flash route and an optional thinking switch.
- [DeepSeek R1 Distill Llama 70B Abliterated](models/deepseek-r1-llama-70b-abliterated.md) — Choose when you specifically want an R1-distilled Llama 70B baseline.
- [DeepSeek R1 Distill Qwen 32B Abliterated](models/deepseek-r1-qwen-32b-abliterated.md) — Choose when you specifically want an R1-distilled Qwen 32B baseline.

Check the [Muapi live page](https://muapi.ai/deepseek-r1-abliterated-api) for current availability and pricing.
