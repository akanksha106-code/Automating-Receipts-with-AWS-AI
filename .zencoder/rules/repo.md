# Repo Info

- Name: Automating Receipts with AWS & AI
- Language: Python
- Primary entry point: lambda_receipt.py
- Infra: AWS S3, Lambda, Textract, DynamoDB, SES
- CI: GitHub Actions (linting with black/isort/flake8 on Python 3.9)
- Package management: requirements.txt + pyproject.toml
- License: Apache-2.0
- Important env vars: DYNAMODB_TABLE, SES_SENDER_EMAIL, SES_RECIPIENT_EMAIL, AWS_DEFAULT_REGION
- Docs: README.md, CONTRIBUTING.md, SECURITY.md, CODE_OF_CONDUCT.md