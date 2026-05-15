# Licensing

Clip Lab is distributed under the MIT License in `LICENSE`.

## First-Party Code

The Python packages, FastAPI service, Remotion integration code, browser UI, documentation, tests,
and Docker configuration in this repository are distributed as Clip Lab project code under MIT.

## Bundled Third-Party Asset

The renderer bundles one font file:

```text
apps/renderer/public/fonts/NotoSerif-Bold.ttf
```

That font is from the Noto project and is licensed under the SIL Open Font License, Version 1.1.
The license text is included at `LICENSES/OFL-1.1.txt`, and the attribution is repeated in
`NOTICE.md`.

## Runtime Dependencies

Clip Lab does not vendor third-party application source trees, model weights, private media, or
generated outputs. Runtime dependencies are installed as Python packages, npm packages, Docker image
packages, or system tools. Their own licenses apply when users install or build the stack.

Important runtime surfaces include:

- FFmpeg / ffprobe for media processing
- Remotion packages for rendering
- yt-dlp for URL ingest
- OpenCV and PySceneDetect for visual analysis
- optional WhisperX for transcription
- optional OpenRouter API usage for model-backed clip intelligence

## Redistribution Rule

Do not add copied source trees, model weights, raw uploads, generated clips, or third-party media to
the repository unless the license and attribution are clear and the files are intentionally part of
the public distribution.
