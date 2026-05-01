# Tax Transcript Request System

## Project Overview
A Python project for uploading tax transcript request PDF files and to extract the data from the tax transcript PDF file using OpenAI's GPT. The extracted JSON file will be used by this system to request the tax transcripts on behalf of client for applying for a loan. 

## Use Case & Workflow
Current scenario the banker manually enters the data from clients tax transcript PDF file in to the Tax transcript request system. Using OpenAI this will replace the manual entry and automate the extraction process. Tax transcript request system will use this JSON file to order Tax transcripts from IRS.

## AI Features to be Implemented
- Prompt engineering to upload tax transcript request PDF files
- Automatic file naming with timestamps to prevent overwrites
- List all previously uploaded files
- View uploaded PDF files using system default viewer
- Captures user-entered form field values use Retrieval-Augmented Generation (RAG) and vector databases
- Structured outputs - Extract PDF data to JSON
- Evaluation frameworks
- Observability tools
- List all extracted JSON files

## Prerequisites
- Python 3.11 or higher
- OpenAI Account and API Key (GPT-4 Access required)
- Code Editor ( IDE ) VScode or other editor

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
3. Follow the Prompts.

## User Interface

### Upload a tax transcript request PDF

<img width="851" height="307" alt="image" src="https://github.com/user-attachments/assets/501f2aac-48a4-4259-a05c-a08bc4e6c4a8" />

### Confirmation of uploaded file

<img width="846" height="361" alt="image" src="https://github.com/user-attachments/assets/37f6ddd1-b133-42e1-a9c2-43bb2214ff55" />

### View an uploaded PDF file

<img width="845" height="428" alt="image" src="https://github.com/user-attachments/assets/b6c2cf5c-9856-49a6-92df-59d5c9ca2158" />

### Extract PDF data to JSON

<img width="856" height="259" alt="image" src="https://github.com/user-attachments/assets/dc5048da-93e9-4a5c-967b-0468c97fa0b7" />


### Structured output

<img width="835" height="872" alt="image" src="https://github.com/user-attachments/assets/b00504d3-e515-48b7-a89f-c436833efa50" />


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

## Expected Outputs - JSON Output Format
When you extract a PDF to JSON, the output includes:
- **form_data**: Key-value pairs of user-entered form fields

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

## Evaluation Strategy
- Briefly describe how you would assess your system’s effectiveness.
-  Include any metrics or evaluation methods you would use.

## Observability Plan
-  Note how you would track performance, errors, or usage patterns over time.

## Notes
- Only PDF files are accepted
- Uploaded files are stored in the `uploads` subdirectory
- Filenames include timestamps to ensure uniqueness
- The JSON will be used by downstream system to request Tax Transcript
