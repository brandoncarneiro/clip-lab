# Quickstart

## Backend-First Docker Path

```bash
git clone https://github.com/sommbc/clip-lab.git
cd clip-lab
cp .env.example .env
docker compose up -d --build --wait
```

In another terminal, run the fixture pipeline without rendering:

```bash
docker compose exec -T api clip-lab /app/fixtures/sample.mp4 \
  --transcript-json /app/fixtures/sample.transcript.json \
  --output-root /app/output \
  --job-id quickstart-fixture \
  --no-render
```

Then run the full render path:

```bash
docker compose exec -T api clip-lab /app/fixtures/sample.mp4 \
  --transcript-json /app/fixtures/sample.transcript.json \
  --output-root /app/output \
  --job-id quickstart-render
```

Inspect results:

```bash
find output/quickstart-fixture -maxdepth 4 -type f | sort
```

## Expected Output

Each run creates `output/<job_id>/` with source media, extracted audio, raw clips, vertical clips,
render props, metadata, transcript, scene data, and `export.zip`. Full render also writes MP4 files under
`clips/rendered/`.

## API Path

```bash
curl -F "file=@./fixtures/sample.mp4" \
  -F "transcript_json_path=/app/fixtures/sample.transcript.json" \
  -F "render=false" \
  http://localhost:8000/api/jobs
```

Check status:

```bash
curl http://localhost:8000/api/jobs/<job_id>
```

## Optional Browser UI

The web app is not required for backend development:

```bash
docker compose --profile web up --build
```
