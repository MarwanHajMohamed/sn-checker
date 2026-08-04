# SN Checker

An offline tool for scanning QR / barcodes, keeping the **last 10 characters** of
each code, building a table of them, and then **highlighting the matching rows in
your Excel sheet**.

Everything runs locally in your browser. Nothing is uploaded and the page never
contacts any website — you can use it with the network unplugged.

## The file

- **`sn-scanner.html`** — a single, self-contained page. Double-click it to open
  in any browser (Chrome, Edge, Firefox). No install, works offline. The Excel
  reading/writing library ([ExcelJS](https://github.com/exceljs/exceljs)) is
  bundled inside the file, so there is nothing else to download.

## What it does

**Step 1 — Scan codes**

- Click the big scan box, then scan a pack with a USB / Bluetooth barcode
  scanner (they type the code and press Enter, just like a keyboard).
- The tool takes each scanned string, throws away everything except the **last
  10 characters**, and adds that code to a table. It then waits for the next
  scan and adds it to the same table.
- Duplicate codes are skipped by default (you can turn this off).
- The number of trailing characters to keep is adjustable (default **10**).
- Your table is saved in the browser, so a refresh won't lose it.
- You can **Copy codes**, **Copy the table** (ready to paste into Excel),
  **Export a CSV**, or **Clear all**.

**Step 2 — Highlight matches in Excel**

- Load your `.xlsx` file and pick the worksheet.
- Choose how to match:
  - **Match when** — *Cell contains the code* (default) highlights a row when
    the code appears **anywhere inside** a cell's value, so it works even when
    the sheet stores longer strings around the code. *Cell exactly equals the
    code* requires a whole-cell match.
  - **Look in** — *Any column (whole row)* (default) searches every column, or
    pick a single column to restrict the search.
- Every matching row gets highlighted (whole row, colour of your choice —
  yellow by default). Untick "Highlight the whole row" to colour only the
  matching cell instead.
- You download a **new** highlighted copy — your original file is never changed.
- A short report tells you how many rows were highlighted and lists any scanned
  codes that were **not** found.

Matching options: ignore leading/trailing spaces (on by default) and ignore
upper/lowercase (off by default).

## Typical workflow

1. Open `sn-scanner.html`.
2. Scan every pack. Watch the table fill up (last 10 characters of each code).
3. Go to Step 2, load your Excel sheet, choose the column with the serials, and
   click **Highlight matches & download**.
4. Open the downloaded `…-highlighted.xlsx` — the matching rows are highlighted.

## Notes

- The comparison uses the code's **last 10 characters**. With the default
  *Cell contains the code* match, it will still find that code inside a longer
  string in your sheet, so you don't need to pre-trim the column.
- `.xls` (old format) is not supported — save as `.xlsx` first.
