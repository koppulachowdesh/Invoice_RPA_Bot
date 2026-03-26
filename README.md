# Invoice Data Extraction Bot

An automated RPA bot built with Python RPA Studio that extracts structured data from PDF invoices using AI and saves the results to an Excel file.

# What It Does

This bot automatically reads PDF invoices from a folder, uses AI to understand and extract the data, and saves everything neatly into an Excel spreadsheet — no manual data entry needed.


## Action Cards — Step by Step

## Action Card 1 — Iterate Through Folder
Scans the invoice folder and loops through every PDF file one by one.

## Action Card 2 — Run Python Script
Runs a Python script that collects all PDF file paths into a list.

## Action Card 3 — For Each (Loop)
Loops through each PDF. Everything below runs once per file.

## Action Card 4 — Read Text from PDF
Opens the current PDF and extracts all raw text from it.

## Action Card 5 — Ask AI (GPT-4o , Gemini...)
Sends the text to GPT-4o to extract invoice fields as JSON.

## Action Card 6a — Add Row → invoice_details sheet
Saves header-level invoice data (number, date, vendor, total) to Excel.

## Action Card 6b — Add Row → item_details sheet
Saves each line item (invoice,description, quantity, price) to Excel.


##  How to Run

1. Open Python RPA Studio
2. Import this project
3. Open variables section and update these values in CONFIGS section:
               invoice_path - Path of the folder where your PDFs are stored 
               excel_path - Path Where you want the Excel file saved 
4. For API Key field In the Ask AI action card:
   - I used an API key from OpenRouter (https://openrouter.ai)
   - Sign up on OpenRouter, generate a free API key, and paste it there
   - The key looks like: sk-or-v1-xxxxxxxxxx
   - Model used: gpt-4o
   - Base URL : `https://openrouter.ai/api/v1
5. Click Run in RPA Studio


## Prompt Used in AI action card
You are an expert invoice data extractor.

The following is raw text extracted from an invoice:

-------------------------
{{ID Of 'READ TEXT FROM PDF' action card}}
-------------------------

Extract the following fields:

- invoice_number
- invoice_date
- vendor_name
- billing_address
- items (list of purchased items with name, quantity, price if available)
- subtotal
- shipping
- total_amount

Rules:
- Return ONLY valid JSON.
- Do NOT include any explanation, notes, or extra text.
- Use exact values from the provided text (DO NOT guess).
- If a field is missing, return null.
- Preserve currency symbols (e.g., $, ₹) if present.
- Dates should be returned exactly as found (do not reformat).
- If multiple items exist, return them as an array.

Output format:

{
  "invoice_number": "",
  "invoice_date": "",
  "vendor_name": "",
  "billing_address": "",
  "items": [
    {
      "name": "",
      "quantity": "",
      "price": ""
    }
  ],
  "subtotal": "",
  "shipping": "",
  "total_amount": ""
}
