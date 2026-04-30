# Tax Transcript Request System

A simple Python project for uploading tax transcript request PDF files.

## Features
- Upload tax transcript request PDF files
- Automatic file naming with timestamps to prevent overwrites
- List all previously uploaded files
- View uploaded PDF files using system default viewer
- **Extract PDF data to JSON** — captures both text and user-entered form field values
- List all extracted JSON files
- Simple CLI interface

## Project Structure
```
TaxTranscript/
├── tax_transcript.py   # Main application code
├── README.md            # This file
└── uploads/             # Directory for uploaded PDFs and extracted JSONs
```

## How to Run
1. Navigate to the `TaxTranscript` directory.
2. Run the application:
   ```
   python tax_transcript.py
   ```
3. Follow the CLI prompts:

## Menu Options
| Option | Description |
|--------|-------------|
| 1 | Upload a tax transcript request PDF |
| 2 | List all uploaded files |
| 3 | View an uploaded PDF file |
| 4 | Extract PDF data to JSON |
| 5 | List extracted JSON files |
| 6 | Exit |

## Usage Example
```
=== Tax Transcript Request System ===

1. Upload a tax transcript request PDF
2. List all uploaded files
3. View an uploaded PDF file
4. Extract PDF data to JSON
5. List extracted JSON files
6. Exit

Select an option: 1
Enter the path to the PDF file: C:\Users\John\Documents\tax_request.pdf

✓ File uploaded successfully!
```

## JSON Output Format
When you extract a PDF to JSON, the output includes:
- **form_data**: Key-value pairs of user-entered form fields (if any)

```json
{
  "taxpayer": {
    "name": "John Doe",
    "ssn": "123-45-6789",
    "street_address": "123 Main St,",
    "city": "Detroit",
    "state": "MI",
    "zip_code": "48201",
    "previous_address": null
  },
  "spouse": {
    "name": null,
    "ssn": null
  },
  "transcript_request": {
    "type": "RETURN_TRANSCRIPT", 
    "form_number": "1040",
    "tax_year": "2025,2024,2023,2022"
  },
  "signature_date": "2026-04-30",
  "consent": true
}
```
  Filename: tax_transcript_20260430_143022_tax_request.pdf
  Size: 12345 bytes
  Uploaded at: 2026-04-30T14:30:22.123456
```

## Notes
- Only PDF files are accepted
- Uploaded files are stored in the `uploads` subdirectory
- Filenames include timestamps to ensure uniqueness
