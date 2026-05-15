# Examples

The tracked fixture example is intentionally small and deterministic:

```text
fixtures/sample.mp4
fixtures/sample.transcript.json
```

Run it without external model calls or WhisperX:

```bash
docker compose up -d --build --wait
docker compose exec -T api clip-lab /app/fixtures/sample.mp4 \
  --transcript-json /app/fixtures/sample.transcript.json \
  --output-root /app/output \
  --job-id example-fixture \
  --no-render
```

Expected files:

```text
output/example-fixture/
  audio/source.wav
  clips/raw/clip_01.mp4
  clips/vertical/clip_01.mp4
  metadata.json
  render_props/clip_01.json
  scenes.json
  source/sample.mp4
  transcript.json
  export.zip
```

Generated outputs are not committed. Recreate them locally with the command above.
