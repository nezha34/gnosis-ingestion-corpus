# PDF conformance profiles (reference)

This corpus tracks **expected ingestion behavior** in `manifest.csv`. The optional `pdf_profile` column summarizes **document shape / conformance intent** for PDFs (not a formal validator output). Each row includes **`raw_url`**: a direct `raw.githubusercontent.com` link to the committed file (PDFs and images), so you can download assets without guessing paths.

## ISO-oriented families (when you need a label)

| Family | Typical use | Corpus notes |
|--------|-------------|--------------|
| **Standard PDF** | General documents | Baseline; most `pdf_security` / `pdf_ocr` samples are “ordinary” PDFs with extra features (JS, links, encryption). |
| **PDF/A** | Archival | Add under `files/pdf/profiles/` when you have a vetted binary + license; set `pdf_profile` to `pdf_a` (or `pdf_a_1b`, etc.). |
| **PDF/UA** | Accessibility (tagged) | Add a tagged sample when available; `pdf_profile` → `pdf_ua`. Ingestion may still treat as standard PDF unless you assert structure checks. |
| **PDF/E**, **PDF/X**, **PDF/VT** | Engineering, print, variable data | Include only if the product cares; same manifest pattern. |
| **PAdES** | Signed PDFs | Use when signature validation or CMS features are in scope. |
| **PDF Healthcare** | Medical workflows | Niche; add if regulated workflows are tested. |
| **Searchable PDF** | Image pages + hidden text (often OCR) | Many `pdf_ocr` scans behave like this after OCR; `pdf_profile` may be `searchable_scanned` when that is the intent. |

## How `pdf_profile` is used here

- **`standard_*`**: Typical PDF without claiming a specific ISO subset (may still embed JS, files, links).
- **`encrypted_*`**: Password or permission-gated.
- **`corrupted`**: Parser failure expected (`pdf_parsing`).
- **`ocr_layout_stress`**: Expected to ingest; stresses OCR/layout/reading order (`pdf_ocr`).
- **`pdf_a` / `pdf_ua`**: Reserved for files **vetted** as PDF/A or PDF/UA (add binaries + update this doc).

Non-PDF assets (e.g. SVG) leave `pdf_profile` empty.

## Vendoring new conformance samples

1. Place the file under `files/pdf/profiles/` (or a subfolder by family).
2. Add a row to `manifest.csv` with `category` `pdf_profile` (or keep `pdf_ocr` / `pdf_security` if the sample is primarily testing that slice).
3. Set `pdf_profile` to the closest label from the table above.
4. Record provenance and license in `files/pdf/profiles/SOURCES.md`.

See also: [profiles README](../files/pdf/profiles/README.md).
