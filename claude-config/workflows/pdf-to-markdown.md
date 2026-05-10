---
description: Converts a PDF to high-fidelity Markdown with LaTeX support and optimized page-by-page OCR rendering.
source: ported from ~/.gemini/antigravity/global_workflows/pdf-to-markdown.md
---

# PDF to Markdown

When the user wants a PDF converted to markdown (or needs PDF content in a form the AI can work with):

## Workflow

1. **Convert PDF to images (one per page).**
   - Use the global script: `python "C:\Users\the10\.gemini\antigravity\global_scripts\pdf_to_images.py" <path_to.pdf> [output_dir] [--dpi 150]`.
   - Documents >= 10 pages trigger parallel rendering. < 10 pages use sequential rendering.
   - Increase DPI to 300 for complex diagrams if needed.
   - Requires PyMuPDF: `pip install pymupdf`.
   - Output: `<pdf_stem>_pages/page_001.png`, `page_002.png`, etc.

2. **Parse each page image into markdown.**
   - Read each generated PNG with the read/vision tool.
   - Structure output as headings, lists, code blocks, paragraphs.
   - **Answer Blocks**: If the PDF has answer boxes or response placeholders, parse as `**Answer:**` followed by a quote block.
   - **LaTeX**: Use `$ ... $` for inline math and `$$ ... $$` for display math.

3. **Output and Cleanup.**
   - Write a single structured Markdown file (e.g., `<basename>_overview.md`).
   - Delete temporary image assets unless the user says otherwise.

## Notes
- The global script accepts any PDF path and optional output dir — reusable across projects.
- Some PDFs are image-only; parsing is then visual. This workflow assumes image-based parsing for consistency.
