# Pricing

The figures below are Muapi catalog rates per million tokens, checked on 2026-11-25. Input and output rates can differ. These values are a dated snapshot; verify the live Muapi page before budgeting.

| Model | Input / 1M | Output / 1M | Context | Input type |
|---|---:|---:|---:|---|
| <code>deepseek-v4-1-flash-abliterated</code> | $0.66 | $2.64 | 1M | Text |
| <code>deepseek-r1-llama-70b-abliterated</code> | $1.40 | $1.40 | 16K | Text |
| <code>deepseek-r1-qwen-32b-abliterated</code> | $2.80 | $2.80 | 16K | Text |

## Estimate a request

A rough estimate is:

```text
estimated cost = (input tokens × input rate + output tokens × output rate) ÷ 1,000,000
```

Actual charges depend on usage and Muapi's current billing rules. Check the response usage or cost fields and your Muapi dashboard for account totals.

## Price changes

Model availability, context limits, fields, and rates can change. Verify the live [Muapi model page](https://muapi.ai/deepseek-r1-abliterated-api) or the [Muapi catalog](https://muapi.ai/models).
