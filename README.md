# CSV Data Cleaner for SKUs

**Python script to validate and clean product CSV files for Byrd Dashboard, reducing errors during CSV upload.**

---

## Overview

This script was developed while working at **byrd technologies GmbH** to help automate the process of uploading products to the **Byrd Customer Dashboard**.  

Uploading products via CSV often requires strict adherence to specific formatting rules. Minor mistakes (wrong barcode format, decimal separators, empty mandatory fields, etc.) would normally raise errors in the dashboard and require support intervention. This script **pre-processes CSV files**, ensuring they meet the dashboard’s requirements and reducing the need for customer support.

It handles:

- Validation and correction of **mandatory fields** (`SKU`, `name`, `netValue`)
- Standardization of **barcode types** (`code_128`, `ean_13`, `gs1_128`, `qr_code`)
- Correction of **numeric formats** for weight and net value (handling commas, dots, currency symbols)
- Validation of **boolean fields** (`organic`, `fragile`, `lotsEnabled`)
- Removal of empty columns
- Splitting CSV files into multiple smaller files (max 100 products per file, as per dashboard limits)

---

## Supported CSV Fields

According to the [Byrd support documentation](https://support.getbyrd.com/en/knowledge-base/uploading-products-from-a-csv-file), the CSV headers include:

| Header | Example | Description |
|--------|---------|-------------|
| sku | sku-a | SKU identifier, mandatory |
| name | prod-a | Product name, mandatory |
| netValue | 1.01 | Supplier cost, mandatory |
| organic | FALSE | TRUE/FALSE |
| lotsEnabled | FALSE | TRUE/FALSE |
| fragile | TRUE | TRUE/FALSE |
| description | example description | Product description |
| barcode | ABC-abc-1234 | Barcode of the product |
| barcodeType | code_128 | Type of barcode: `ean_13`, `code_128`, `gs1_128`, `qr_code` |
| reorderPoint | 10 | Stock threshold for notifications |
| customsTariffNumber | 111111 | 6, 8, or 10 digit tariff number |
| originCountryCode | DE | Two-letter country code |
| weight | 0.25 | Product weight |

> Only the first three columns (`SKU`, `name`, `netValue`) are mandatory. Other fields are optional, but if included, the script will ensure valid formatting.

---

## Requirements

- Python 3.x
- Standard `csv` library (built-in)

---

## How to Use

1. Place your product CSV file in the same folder as the script.
2. Run the script:

```bash
python csv_cleaner.py
