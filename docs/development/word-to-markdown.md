---
layout: default
title: Convert Documents to Markdown
parent: Development
last_modified_date: 10:00 08.06.2026
---

# Convert Documents to Markdown with Pandoc

Use the official [`pandoc/core`](https://hub.docker.com/r/pandoc/core) Docker image to batch-convert documents to Markdown - no local Pandoc install required.

The `--network none` flag runs the container fully offline.

## Word (.docx) → Markdown

Recursively convert every `.docx` file in an input directory, preserving the folder structure in the output directory.

### PowerShell

```powershell
docker run --rm --network none `
  -v "C:/path/to/input:/in:ro" `
  -v "C:/path/to/output:/out" `
  --entrypoint sh pandoc/core -c '
  cd /in
  find . -type f -name "*.docx" | while read f; do
    rel="${f#./}"
    mkdir -p "/out/$(dirname "$rel")"
    echo "Converting: $rel"
    pandoc "$f" -o "/out/${rel%.*}.md"
  done
'
```

### Bash / Linux / macOS

```bash
docker run --rm --network none \
  -v "$(pwd)/input:/in:ro" \
  -v "$(pwd)/output:/out" \
  --entrypoint sh pandoc/core -c '
  cd /in
  find . -type f -name "*.docx" | while read f; do
    rel="${f#./}"
    mkdir -p "/out/$(dirname "$rel")"
    echo "Converting: $rel"
    pandoc "$f" -o "/out/${rel%.*}.md"
  done
'
```

## HTML -> Markdown

Same approach, just swap the file extension in the `find` filter:

```powershell
docker run --rm --network none `
  -v "C:/path/to/input:/in:ro" `
  -v "C:/path/to/output:/out" `
  --entrypoint sh pandoc/core -c '
  cd /in
  find . -type f -name "*.html" | while read f; do
    rel="${f#./}"
    mkdir -p "/out/$(dirname "$rel")"
    echo "Converting: $rel"
    pandoc "$f" -o "/out/${rel%.*}.md"
  done
'
```

## Notes

- Replace `C:/path/to/input` and `C:/path/to/output` with your own directories. Use forward slashes for Docker volume paths on Windows.
- `:ro` mounts the input directory read-only so the source files can't be modified.
- `${rel%.*}.md` strips the original extension and appends `.md`.
- Extract embedded images with `--extract-media`:

  ```bash
  pandoc "$f" --extract-media="/out/media" -o "/out/${rel%.*}.md"
  ```

- To convert a single file:

  ```powershell
  docker run --rm --network none `
    -v "C:/path/to/input:/in:ro" `
    -v "C:/path/to/output:/out" `
    pandoc/core "/in/document.docx" -o "/out/document.md"
  ```
