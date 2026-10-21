# PDF Invoice Data Extraction Pipeline – n8n + Gemini API

An end-to-end n8n workflow that turns invoice PDFs into structured data. Upload a PDF through a form, and the workflow extracts the text, uses the Gemini API to parse the key fields, cleans and validates the result, and logs it to Google Sheets. No manual data entry.

## What it does

1. **Form trigger** – accepts an invoice PDF upload.
2. **Text extraction** – pulls the raw text out of the PDF.
3. **Gemini API (HTTP Request)** – prompts the model to return structured JSON with:
   - Invoice number
   - Date
   - Customer
   - Vendor
   - Line items
   - Quantities
   - Totals
4. **Code node** – cleans and validates the AI-generated JSON.
5. **Google Sheets** – appends each invoice as a new row.

## Tech stack

- [n8n](https://n8n.io) (workflow automation)
- Google Gemini API
- Google Sheets API
- JavaScript (Code node)

## Setup

### Prerequisites

- An n8n instance (cloud or self-hosted)
- A Gemini API key from [Google AI Studio](https://aistudio.google.com)
- A Google account with a Sheet ready to receive the data

### Import the workflow

1. Download the workflow `.json` file from this repo.
2. In n8n, go to **Workflows → Import from File** and select it.
3. Open the workflow and set up credentials:
   - **Gemini API key**: add it where the HTTP Request node calls Gemini.
   - **Google Sheets**: connect your Google account and choose your target spreadsheet and sheet.
4. Match the Google Sheet column headers to the fields above (invoice number, date, customer, vendor, items, quantities, total).
5. Activate the workflow and open the form URL to test it with a sample invoice.

> **Note:** Credentials are not included in the exported JSON. You need to add your own.

## Usage

Open the form trigger's URL, upload an invoice PDF, and submit. A new row with the extracted fields appears in your Google Sheet within seconds.

## Repo contents

```
.
├── README.md
└── pdf-invoice-data processing pipeline.json   # n8n workflow export 
```

## Possible improvements

- Support scanned invoices with an OCR step
- Add error handling and a notification when parsing fails
- Flag invoices with missing or mismatched totals

## Author

**Kinjal Poptani**: AI & Automation Developer, Pune
