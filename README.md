# FMD Checker

An offline tool (Zeymos Pharma) for scanning QR / barcodes, keeping the part of
each code you choose, and **highlighting the matching rows** in your **Excel
sheet or PDF table** — live, as you scan.

> The page carries the FMD Checker / Zeymos Pharma theme. The logo is an inline
> SVG recreation of the Zeymos wordmark; drop in the exact logo file if you want
> it pixel-perfect (replace the `<svg>` inside the `.brand` element, or embed the
> image as a `data:` URI so the page stays a single offline file).

Everything runs locally in your browser. Nothing is uploaded and the page never
contacts any website — you can use it with the network unplugged.

## The file

- **`sn-scanner.html`** — a single, self-contained page. Double-click it to open
  in any browser (Chrome, Edge, Firefox). No install, works offline. Everything
  it needs is bundled inside the file: [ExcelJS](https://github.com/exceljs/exceljs)
  (read/write `.xlsx`), [pdf.js](https://github.com/mozilla/pdf.js) (read PDF
  text) and [pdf-lib](https://github.com/Hopding/pdf-lib) (write the highlighted
  PDF).

## What it does

**Step 1 — Scan codes**

- Click the big scan box, then scan a pack with a USB / Bluetooth barcode
  scanner (they type the code and press Enter, just like a keyboard).
- The tool takes each scanned string, keeps the part you choose, and adds that
  code to a table. It then waits for the next scan and adds it to the same
  table.
- Two boxes decide which part of each scan is kept:
  - **From character #** — the position to start at (1 = the first character).
  - **Number of characters** — how many characters to keep from that position.
    For example, **From character 12** + **5** saves characters 12–16. Leave
    the count **blank** to keep everything from the start position to the end.
  - A scan shorter than the start position is skipped.
- Duplicate codes are skipped by default (you can turn this off).
- Your table is saved in the browser, so a refresh won't lose it.
- You can **Copy codes**, **Copy the table** (ready to paste into Excel),
  **Export a CSV**, or **Clear all**.

**Step 2 — Highlight rows live (Excel or PDF)**

- **Load your table first** — an Excel `.xlsx` **or** a digital PDF (`.pdf`).
  It appears as a live preview below.
- **Then scan.** Each matching row lights up **immediately** in the preview as
  you scan. Load-first-then-scan or scan-first-then-load both work — loading a
  file highlights everything already scanned.
- When you're done, click **Download highlighted file** to save a **new** copy
  with the rows highlighted. Your original file is never changed.
- A live summary shows how many rows are highlighted and how many of your
  scanned codes have been matched / not found yet.

Matching options (shared):

- **Match when** — *contains the code* (default) highlights a row when the code
  appears **anywhere inside** a cell / line, so it works even when the table
  stores longer strings around the code. *Exactly equals* (Excel only) requires
  a whole-cell match.
- **Ignore upper/lowercase** — off by default.
- Highlight **colour** — yellow by default; the preview and the downloaded file
  use whatever you pick.

Excel-only options: pick the **worksheet**, the **header row**, and which
**column** to look in (or *Any column – whole row*); **highlight the whole row**
or only the matching cell; **format the exported sheet as an Excel table**
(on by default — adds the filter/sort header so the downloaded file is a proper
Excel *Table*); and **no banded row colours** to keep the table plain so only
the highlights stand out (untick for the classic striped look).

**PDF notes:** works on **digital** PDFs whose text is selectable (not scanned
images). Each row is highlighted wherever a scanned code appears in its line of
text, and the whole row gets a translucent band so the text stays readable.
Rotated pages or PDFs with an unusual page origin may highlight slightly off.

## Typical workflow

1. Open `sn-scanner.html` (the scan box shows a green **v4** marker).
2. In Step 2, load your Excel sheet or PDF.
3. Scan every pack — matching rows highlight live.
4. Click **Download highlighted file** and open the `…-highlighted.xlsx` /
   `…-highlighted.pdf`.

## Notes

- `.xls` (old Excel format) is not supported — save as `.xlsx` first.
- Very large PDFs (many pages) take a moment to render the live preview.
