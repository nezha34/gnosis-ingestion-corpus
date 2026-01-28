# Gnosis Ingestion Corpus

Shared corpus of files to test the ingestion pipeline end-to-end:

- File validation & MIME detection
- Parsing robustness (PDF + images)
- OCR robustness
- Security feature detection (non-fatal flags)

## Repository layout
files/
pdf/
security/   # PDFs expected to ingest but emit security flags (or controlled rejects like password)
parsing/    # PDFs expected to fail parsing / be rejected
ocr/        # OCR / layout / reading-order stress tests (usually should ingest)
image/
security/   # Images/SVGs expected to ingest but emit security flags (when SVG scanner exists)
parsing/    # Images expected to fail parsing / be rejected
ocr/        # OCR / layout stress tests for images
manifest.csv    # Source of truth: expected outcome per file

## Source of truth: `manifest.csv`

Each row describes one file and what we expect ingestion to do.

Typical columns:
- `file_relpath`: path inside this repo (relative)
- `category`: `pdf_security`, `pdf_parsing`, `pdf_ocr`, `image_security`, `image_parsing`, `image_ocr`
- `expected_error_code`: expected ingestion error code if the file should fail
- `expected_security_flags`: pipe-separated list of flags if the file should be flagged
- (optional) `notes`: short description / why this file exists

### Conventions

- **security/**: should generally ingest, but should emit `security_flags` (non-fatal).
- **parsing/**: expected to fail ingestion with an error code.
- **ocr/**: expected to ingest; used to evaluate OCR/layout quality and robustness.

### Important note about SVG flags

SVG “security flags” require an explicit SVG threat scanner (e.g., detecting `<script>`, `<a href>`, `foreignObject`, external refs).
Until that scanner is implemented, SVG files may ingest without emitting flags even if `manifest.csv` expects them.
That’s fine — `manifest.csv` represents the **target behavior**.
## How to add a new file

1. Put the file in the correct folder under `files/...`
2. Add a row in `manifest.csv` with the expected behavior
3. Commit + push

## Quick sanity checks (optional)

From the repo root:

```bash
# list corpus files
find files -type f | sort

# show manifest header + first rows
head -n 30 manifest.csv
