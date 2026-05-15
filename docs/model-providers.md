# Model Providers

Clip Lab has a provider-agnostic clip-intelligence layer. The pipeline can run without model keys
using deterministic local heuristics. Model-backed intelligence is opt-in.

## Providers

`fake` or `dev`:

- no network
- no keys
- deterministic JSON
- useful for tests and fixture runs

`openrouter`:

- OpenAI-compatible chat completions API
- JSON-only responses
- schema validation in Clip Lab
- no keys required unless the provider is actually used
- free models can be rate-limited, unavailable, or return empty or alternate response shapes

## Environment

Put the real OpenRouter key only in your local `.env` file. The tracked `.env.example` file is a
safe template and must contain placeholders only. Fixture mode still needs no model keys unless
`--use-model-provider` is enabled.

```bash
CLIP_LAB_MODEL_PROVIDER=openrouter
OPENROUTER_API_KEY=
OPENROUTER_BASE_URL=https://openrouter.ai/api/v1

CLIP_LAB_CANDIDATE_MODEL=
CLIP_LAB_CRITIC_MODEL=
CLIP_LAB_PACKAGING_MODEL=

CLIP_LAB_CANDIDATE_FALLBACK_MODEL=
CLIP_LAB_CRITIC_FALLBACK_MODEL=
CLIP_LAB_PACKAGING_FALLBACK_MODEL=

CLIP_LAB_EVAL_MODEL_1=
CLIP_LAB_EVAL_MODEL_2=
CLIP_LAB_EVAL_MODEL_3=
CLIP_LAB_EVAL_MODEL_4=
CLIP_LAB_EVAL_MODEL_5=
```

Default model roles:

- `CLIP_LAB_CANDIDATE_MODEL` mines plausible clip candidates.
- `CLIP_LAB_CRITIC_MODEL` reviews and rejects weak or badly bounded candidates.
- `CLIP_LAB_PACKAGING_MODEL` produces final title, hook, caption, platform fit, and risk metadata.

Fallback model variables are optional. If the primary OpenRouter model returns a provider error,
unavailable-model error, empty response, or malformed JSON after retries, Clip Lab tries the
matching fallback once:

- `CLIP_LAB_CANDIDATE_FALLBACK_MODEL`
- `CLIP_LAB_CRITIC_FALLBACK_MODEL`
- `CLIP_LAB_PACKAGING_FALLBACK_MODEL`

OpenRouter model IDs are intentionally not pinned in `.env.example`. Free model availability, rate
limits, and response behavior can change without a Clip Lab code change. Pick current model IDs from
OpenRouter, keep them in local `.env`, and expect occasional provider-side failures or empty
responses.

## CLI Usage

Fixture mode without a model:

```bash
clip-lab ./fixtures/sample.mp4 \
  --transcript-json ./fixtures/sample.transcript.json \
  --no-render
```

Fake provider:

```bash
clip-lab ./fixtures/sample.mp4 \
  --transcript-json ./fixtures/sample.transcript.json \
  --use-model-provider \
  --model-provider fake \
  --no-render
```

OpenRouter:

```bash
clip-lab input.mp4 --use-model-provider --model-provider openrouter
```

If `OPENROUTER_API_KEY` or a purpose-specific model variable is missing, the command fails before
sending a model request.

## Three Passes

1. Candidate mining selects plausible clips.
2. Critic/editor rejects weak, context-dependent, rambling, or badly bounded clips.
3. Packaging metadata improves title, hook, caption, platform fit, and risk flags.

Prompt files are versioned under:

```text
packages/clip_intelligence/cliplab_clip_intelligence/prompts/
```

Model output is parsed as JSON and then validated against Pydantic schemas before the pipeline uses
it.
