# Tax Transcript Request System

## Project Overview
A Python project for uploading tax transcript request PDF files and to extract the data from the tax transcript PDF file using OpenAI's GPT. The extracted JSON file will be used by this system to request the tax transcripts on behalf of client for applying for a loan.

## Use Case & Workflow
Current scenario the banker manually enters the data from clients tax transcript PDF file in to the Tax transcript request system. Using OpenAI this will replace the manual entry and automate the extraction process.A web-based Python application for managing tax transcript request PDF files with AI-powered extraction, structured data processing, and automated evaluation using LangSmith.

## AI Features to be Implemented
- **Web-based UI** — Built with Flask, accessible at http://127.0.0.1:5000
- **PDF Upload & Management** — Upload tax transcript PDFs with automatic timestamping
- **File Viewing** — Open uploaded PDFs using system default viewer
- **Form Field Extraction** — Extract user-entered data from PDF forms using pypdf
- **AI-Powered Processing** — Process extracted data with OpenAI GPT models using custom system prompts
- **Structured Data Output** — Convert form fields to structured JSON with client_name, SSN, address, tax_form, and year
- **LangSmith Evaluation** — Automated evaluation using CSV dataset with detailed scoring metrics
- **Automatic Dependency Management** — Installs required packages (flask, pypdf, openai, langsmith) on first run
- **Comprehensive Error Handling** — Robust error handling for PDF processing, API calls, and evaluation
- **JSON Export** — Save extracted data as JSON files alongside PDFs

## System Prompt
The application uses the following system prompt for OpenAI extraction:
```
Extract information from the json into a dictionary using OpenAI and langsmith for evaluation. 
The dictionary keys are client_name (f1_1[0]), SSN(f1_2[0]), current address(f1_5[0]), previous address(f1_6[0]), phone number (f1_13[0]), tax form (f1_8[0]), tax year f1_17[0] f1_20[0] f1_23[0] f1_26[0]. 
Make sure the output is in proper JSON with double quotes around the keys and values.
```

## Prerequisites
- Python 3.8 or higher
- OpenAI API key (set as environment variable `OPENAI_API_KEY`)
- LangSmith API key (optional, for evaluation features - set as `LANGSMITH_API_KEY`)
- Code Editor ( IDE ) VScode or other editor

## Project Structure
```
TaxTranscript/
├── tax_transcript.py   # Main application code
├── README.md            # This file
└── uploads/             # Directory for uploaded PDFs and extracted JSONs
```

### Installation and Startup

1. Navigate to the `TaxTranscript` directory:
   ```
   cd TaxTranscript
   ```

2. Set your OpenAI API key (required):
   ```
   set OPENAI_API_KEY=your_api_key_here
   ```

3. (Optional) Set your LangSmith API key for evaluation:
   ```
   set LANGSMITH_API_KEY=your_langsmith_key_here
   ```

4. Run the application:
   ```
   python tax_transcript.py
   ```
   
   **Note:** Dependencies (flask, pypdf, openai, langsmith) are automatically installed on first run if not present.
   
   If the `python` command is not in your PATH, use the full path:
   ```
   C:\Users\User\AppData\Local\Python\pythoncore-3.14-64\python.exe tax_transcript.py
   ```

5. Open your browser and go to: **http://127.0.0.1:5000**

6. You'll see output like:
   ```
   === Starting Tax Transcript System ===
   === Starting Evaluation on Tax Transcripts ===
   === Evaluation Complete ===
   Results: {...}
   
   === Tax Transcript Web System ===
   Open your browser and go to: http://127.0.0.1:5000
   * Running on http://127.0.0.1:5000
   ```

## Web Interface Routes
| Route | Description |
|-------|-------------|
| `/` | Upload - Upload tax transcript PDF files with automatic timestamping |
| `/view` | View Files - List all uploaded PDFs with file details and open functionality |
| `/open/<filename>` | Open File - Open a specific PDF file using system default viewer |
| `/extract` | Extract Data - Select a PDF and extract user-entered form data to JSON |
| `/extract_data` | Process Extraction - Process selected PDF and display extracted data |


### Upload a tax transcript request PDF

<img width="851" height="307" alt="image" src="https://github.com/user-attachments/assets/501f2aac-48a4-4259-a05c-a08bc4e6c4a8" />


### Confirmation of uploaded file

<img width="846" height="361" alt="image" src="https://github.com/user-attachments/assets/37f6ddd1-b133-42e1-a9c2-43bb2214ff55" />


### View an uploaded PDF file

<img width="845" height="428" alt="image" src="https://github.com/user-attachments/assets/b6c2cf5c-9856-49a6-92df-59d5c9ca2158" />


### Extract PDF data to JSON

<img width="856" height="259" alt="image" src="https://github.com/user-attachments/assets/dc5048da-93e9-4a5c-967b-0468c97fa0b7" />


## Expected Outputs - JSON Output Format
When you extract a PDF to JSON, the output includes three main sections:
- **form_data**: Key-value pairs of user-entered form fields

### Structured output

```json
{
  "form_data": {
    "f1_1": "John Smith",
    "f1_2": "123-45-6789",
    "f1_5": "123 Main Street, New York, NY 10001",
    "f1_8": "1040",
    "f1_17": "2025"
  },
  "metadata": {
    "source_file": "tax_transcript_20260501_143022_request.pdf",
    "extracted_at": "2026-05-01T14:30:22.123456"
  },
  "structured": {
    "client_name": "John Smith",
    "SSN": "123456789",
    "address": "123 Main Street, New York, NY 10001",
    "tax_form": "1040",
    "year": "2025"
  }
}
```

### Sections:
- **form_data** — Raw extracted form fields from PDF (keys like f1_1, f1_2, etc.)
- **metadata** — File information and extraction timestamp
- **structured** — AI-processed structured data with standardized field names

## LLM Processing
The application processes PDF form data through a multi-step pipeline:

1. **PDF Form Extraction** — Uses `pypdf.PdfReader.get_form_text_fields()` to extract fillable form fields
2. **Data Serialization** — Converts extracted form data to JSON format
3. **OpenAI Processing** — Sends form data to GPT-4o-mini with custom system prompt
4. **JSON Parsing** — Robust parsing with fallback regex extraction for malformed responses
5. **Structured Output** — Returns standardized dictionary with client_name, SSN, address, tax_form, year


### Processing Example
**Input Form Data:**
```json
{
  "f1_1": "John Smith",
  "f1_2": "123-45-6789",
  "f1_5": "123 Main Street, New York, NY 10001",
  "f1_8": "1040",
  "f1_17": "2025"
}
```

**After OpenAI Processing:**
```json
{
  "form_data": { ... },
  "metadata": { ... },
  "structured": {
    "client_name": "John Smith",
    "SSN": "123456789",
    "address": "123 Main Street, New York, NY 10001",
    "tax_form": "1040",
    "year": "2025"
  }
}
```

### Error Handling
- **Empty Responses** — Returns error message for empty OpenAI responses
- **Markdown Removal** — Strips code block formatting from responses
- **JSON Parsing** — Regex fallback for malformed JSON responses
- **API Errors** — Comprehensive exception handling for OpenAI API calls

## LangSmith Evaluation

The application uses LangSmith to evaluate the accuracy of PDF form field extraction:

1. **Dataset Name:** `tax_transcript_class`
2. **Scoring Method:** Compares extracted fields against expected values
3. **Metrics:**
   - **client_name** — Exact match (case-insensitive)
   - **SSN** — Match after removing formatting (dashes, spaces)
   - **address** — Partial match (substring search, 0.5-1.0 score)
   - **tax_form** — Exact match (case-insensitive)
   - **year** — Exact match
4. **Overall Score:** Average of all field scores (0.0 to 1.0)

### Running Evaluation
When you start the application, it automatically:
1. Runs LangSmith evaluation using the uploaded dataset
2. Prints evaluation results to the console
3. Continues running the Flask web server

### Evaluation Output Example
```
=== Starting Tax Transcript System ===
=== Starting Evaluation on Tax Transcripts ===
=== Evaluation Complete ===
Results: {...}
```

### Evaluation Scoring Methodology
The `perform_eval()` function calculates accuracy scores for each field:

- **client_name**: 1.0 for exact match (case-insensitive), 0.0 otherwise
- **SSN**: 1.0 for match after removing dashes/spaces, 0.0 otherwise  
- **address**: 1.0 for exact substring match, 0.5 for partial match, 0.0 for no match
- **tax_form**: 1.0 for exact match (case-insensitive), 0.0 otherwise
- **year**: 1.0 for exact match, 0.0 otherwise

**Final Score**: Average of all field scores (ranges from 0.0 to 1.0)


## Observability Plan
- Add logging to the Application. Log the prompt requests, any errors and events like any GPT-4 PDF calls.
- Python's logging module with JSON formatting would be one good way for adding logging

## Dependencies
The application automatically installs these dependencies on first run:
- **flask** — Web framework for UI
- **pypdf** — PDF form field extraction (PdfReader, get_form_text_fields)
- **openai** — LLM integration for structured extraction (GPT-4o-mini)
- **langsmith** — Evaluation framework and client for automated testing
- **json** — Built-in Python module for data serialization
- **pathlib** — Built-in Python module for file path operations
- **datetime** — Built-in Python module for timestamps

## Core Classes and Functions

### TaxTranscriptManager Class
- **`upload_transcript(file_path)`** — Upload and timestamp PDF files
- **`list_uploads()`** — List all uploaded PDF files with metadata
- **`view_file(filename)`** — Open PDF files using system default viewer
- **`extract_to_json(filename)`** — Extract form fields and process with OpenAI
- **`process_with_openai(form_data)`** — Send data to OpenAI and parse response
- **`list_json_files()`** — List extracted JSON files

### Evaluation Functions
- **`perform_eval(llm_result, dataset_item)`** — Compare LLM output against expected values
- **`run_evaluation()`** — Run complete LangSmith evaluation pipeline
- **`make_call_to_llm(input)`** — Process PDF files for evaluation (uses uploads directory)

### Flask Routes
- **`/` (index)** — Upload page
- **`/upload`** — Handle file uploads
- **`/view`** — List uploaded files
- **`/open/<filename>`** — Open specific PDF file
- **`/extract`** — Data extraction page
- **`/extract_data`** — Process extraction and display results

## Notes
- Only PDF files are accepted
- Uploaded files are stored in the `uploads` subdirectory
- Filenames include timestamps to ensure uniqueness

## Troubleshooting

### Issue: `ModuleNotFoundError: No module named 'flask'`
**Solution:** The application automatically installs dependencies on startup. If this error persists:
```
pip install flask pypdf openai langsmith
```

### Issue: `python command not found`
**Solution:** Use the full path to Python:
```
C:\Users\User\AppData\Local\Python\pythoncore-3.14-64\python.exe tax_transcript.py
```

### Issue: OpenAI API errors
**Solution:** Verify your API key is set:
- Windows: `echo %OPENAI_API_KEY%` should show your key
- Ensure you have API credits available
- Check that your API key is valid in the OpenAI dashboard

### Issue: `No PDF files found in uploads`
**Solution:** This is expected on first run. Upload a PDF file via the web interface (`/` route) and then try extraction.

### Issue: PDF extraction returns empty form fields
**Solution:** The PDF may not have fillable form fields. Try:
- Using a different PDF with form fields
- Checking the PDF in Adobe Reader to confirm it has editable fields

### Issue: Browser won't connect to http://127.0.0.1:5000
**Solution:**
- Ensure the Flask server is running (you should see "Running on..." message)
- Check if port 5000 is already in use by another application
- Try accessing `http://localhost:5000` instead

### Issue: LangSmith evaluation not working
**Solution:** Set your LangSmith API key:
```
set LANGSMITH_API_KEY=your_langsmith_key_here
```
If evaluation is not critical, the app will work without it.

### Issue: `Error loading dataset: [error]`
**Solution:** The dataset must be uploaded to LangSmith separately. Ensure the dataset name `tax_transcript_class` exists in your LangSmith account and contains the required fields.

### Issue: `No PDF files found in uploads`
**Solution:** Upload PDF files via the web interface first, then try extraction or evaluation.

### Issue: OpenAI responses contain markdown formatting
**Solution:** The application automatically strips markdown code blocks. If you see raw markdown in results, check the OpenAI response parsing logic.

### Issue: `Could not parse JSON` errors
**Solution:** The application uses regex fallback for malformed JSON. Check the OpenAI system prompt to ensure it returns valid JSON format.

### Issue: Flask app won't start on port 5000
**Solution:** Check if another application is using port 5000:
```
netstat -ano | findstr :5000
```
Use a different port by modifying the `app.run()` call in the code.
