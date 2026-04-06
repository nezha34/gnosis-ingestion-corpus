# PDF profile samples

This folder holds **small, license-friendly** PDFs used as **conformance / baseline** references (minimal standard PDF, future PDF/A or PDF/UA fixtures, etc.).

- **`pdf_standard_mozilla_helloworld.pdf`** — Minimal PDF 1.7 from the [pdf.js](https://github.com/mozilla/pdf.js) tree (Apache-2.0). Baseline “ordinary” PDF for MIME validation and happy-path parsing.

## Adding PDF/A or PDF/UA

Do **not** commit unclear rights. Prefer:

1. **Official** sample packs or **explicitly licensed** test files.
2. **Generate** your own minimal tagged PDF/A or PDF/UA with a known toolchain, document the command in `SOURCES.md`.

Until a binary is present, document intended `pdf_profile` values in [`docs/pdf_conformance_profiles.md`](../../docs/pdf_conformance_profiles.md) only.

## See also

- [`SOURCES.md`](SOURCES.md) — provenance and optional download URLs for future fixtures.
