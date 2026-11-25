# Prompt templates for DeepSeek models

Starting templates only; they are not tested outputs or benchmark prompts. Replace bracketed text and use only fields supported by the chosen route.

## Reasoning review

```text
Review this proposed design. State assumptions, identify two failure cases, and finish with a concise recommendation: [design].
```

## Code explanation

```text
Explain what this function does, list edge cases, and suggest one test for each edge case: [code].
```

## Long context

```text
Read the supplied material and return a short summary, key claims, and open questions. Separate what the text says from your inferences: [material].
```

## Image prompts

For a route that accepts image_url, provide the image as a separate request field and refer to it in prompt. Do not assume a text-only route can fetch or inspect an image URL.
