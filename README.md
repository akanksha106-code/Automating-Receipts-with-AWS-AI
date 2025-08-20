# Automating Receipts with AWS & AI

##  Background
Managing expenses manually is time-consuming and prone to human error. Many businesses and individuals have stacks of paper receipts that need to be logged for accounting, tax filing, or reimbursement purposes.  
Traditional expense tracking requires manually entering vendor names, totals, and item details into a spreadsheet or accounting software — a tedious and error-prone task.

**This project solves that problem** by creating a fully automated receipt processing system using AWS cloud services and AI-powered text extraction.  
It eliminates manual data entry, reduces errors, and sends instant notifications when a receipt is processed.

---

##  Understanding
The main goal was to automate the journey from **receipt upload** → **data extraction** → **storage** → **notification**.  
Here’s the thought process:
1. **Input Source**: Receipts can be uploaded as images or PDFs to an Amazon S3 bucket.
2. **Processing Engine**: AWS Lambda (serverless function) would handle all the logic.
3. **AI Integration**: AWS Textract would read and understand the receipt contents.
4. **Data Storage**: Amazon DynamoDB would store structured receipt data.
5. **Notification**: AWS SES would send a formatted email report.

---

## ⚙ Implementation

### **Tech Stack**
- **AWS S3** — Storage for uploaded receipts.
- **AWS Lambda** — Serverless function to process receipts.
- **AWS Textract** — AI OCR for extracting data from receipts.
- **Amazon DynamoDB** — NoSQL database for storing structured data.
- **AWS SES** — Email notifications with receipt details.
- **Python (Boto3)** — AWS SDK for coding the Lambda function.

### **Workflow**
1. **Upload Receipt** → User uploads to S3 bucket.
2. **Trigger** → S3 event triggers Lambda function.
3. **Textract Processing** → Lambda sends file to Textract’s `analyze_expense` API.
4. **Data Extraction** → Vendor, date, total, and line items are parsed.
5. **Database Storage** → Lambda saves structured data in DynamoDB.
6. **Email Notification** → SES sends HTML email with receipt details.

---

##  Getting Started

### Prerequisites
- Python 3.10+
- AWS account with permissions for S3, Lambda, Textract, DynamoDB, SES
- AWS CLI configured locally (for local testing/deployment)

### Install
```bash
python -m venv .venv
# Windows PowerShell
. .venv/Scripts/Activate.ps1
pip install -r requirements.txt
```

### Environment
Copy `.env.example` to `.env` and set values if running locally.

### Run linters
```bash
pip install black isort flake8
black . && isort . && flake8 .
```

---

##  Local Testing (optional)
You can emulate the Lambda handler locally by constructing a mock S3 event and calling `lambda_handler`.

```python
# example_local_test.py (not committed)
from lambda_receipt import lambda_handler

mock_event = {
    "Records": [
        {"s3": {"bucket": {"name": "your-bucket"}, "object": {"key": "receipts/sample.pdf"}}}
    ]
}

lambda_handler(mock_event, None)
```

Note: This requires valid AWS credentials and resources.

---

##  Lessons Learned
- **Textract Data Parsing**: The raw Textract output is complex JSON. Writing a clean parser to handle edge cases (missing totals, different vendor formats) was crucial.
- **SES Sandbox Mode**: AWS SES is in "sandbox mode" by default, meaning you can only send to verified emails. This required verification setup.
- **Error Handling**: Not all receipts have clear totals/dates — fallback defaults had to be implemented.
- **URL Encoding**: S3 object keys need to be URL-decoded to handle spaces and special characters.

---

##  Deliverables
- **Working AWS Lambda Python Script** — Handles end-to-end automation.
- **DynamoDB Table** — Stores all extracted receipt data.
- **SES Email Template** — HTML formatted receipt report.
- **Architecture Diagram** — Visual explanation of the workflow.
- **Sample Data** — Example receipts and extracted outputs.

---

##  Security & License
- See `SECURITY.md` for vulnerability reporting.
- Licensed under **Apache-2.0** (see `LICENSE`).

---

## 🤝 Contributing
Please read `CONTRIBUTING.md` and follow the PR/issue templates. CI runs `black`, `isort`, and `flake8` on PRs.
