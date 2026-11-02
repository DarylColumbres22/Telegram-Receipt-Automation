Telegram Receipt Photo Processing Automation
An AI-powered receipt processing workflow built using n8n, Telegram, Google Gemini,
Google Sheets, and Google Drive.
This workflow receives receipt photos through Telegram, extracts important transaction
information using Google Gemini, records the extracted data in Google Sheets, and
organizes the original receipt images in Google Drive.
Workflow Overview
The workflow automates receipt photo processing through the following steps:
1. Receives a receipt image submitted through Telegram.
2. Downloads the original image for processing.
3. Sends the receipt image to Google Gemini for analysis.
4. Extracts the merchant name, total amount, and transaction date.
5. Parses the AI-generated JSON response and prepares structured receipt data using
JavaScript.
6. Determines the Telegram submission date.
7. Checks whether the required Google Drive folders exist and creates them when
necessary.
8. Checks whether the Receipt Automation spreadsheet exists and creates it when
necessary.
9. Records the extracted receipt information in Google Sheets.
10.Uploads the original receipt image to Google Drive.
Gemini Receipt Extraction
Google Gemini is instructed to analyze the receipt image and return structured JSON
containing exactly three fields:
• Merchant – Store, business, or merchant name shown on the receipt.
• Amount – Clearly identifiable transaction grand total.
• Date – Actual receipt transaction date.
The extraction instructions emphasize:
• Using only information clearly visible in the image.
• Avoiding fabricated or inferred values.
• Returning an empty value when information is uncertain or unreadable.
• Avoiding the use of unrelated monetary values such as subtotal, tax, change, or
cash payment.
The expected response format is:
{"merchant":"","amount":"","date":""}
Data Processing
A JavaScript Code node processes the response from Google Gemini.
It performs the following tasks:
• Parses the JSON response.
• Extracts the merchant, amount, and receipt date.
• Determines the Telegram submission date.
• Generates a human-readable folder date.
• Creates a structured filename using the submission date and merchant name.
The workflow maintains a distinction between the receipt transaction date and the
Telegram submission date.
Date Handling
The workflow uses two separate dates:
Receipt Date
The transaction date printed on the receipt and extracted by Google Gemini.
Submission Date
The date the receipt image was submitted through Telegram.
The submission date is used for organizing receipt images in Google Drive, while the receipt
date is stored separately in Google Sheets.
Google Drive Organization
Receipt images are organized using the following folder structure:
Telegram Receipt Automation Folder/
└── September 6, 2026/
 └── receipt.jpg
The workflow:
• Searches for the main receipt automation folder.
• Creates the main folder if it does not exist.
• Searches for a folder matching the submission date.
• Creates the date folder when necessary.
• Uploads the original receipt image to the corresponding date folder.
This structure helps keep submitted receipt images organized by submission date.
Google Sheets Logging
The workflow records the following information:
• Merchant
• Amount
• Receipt Date
• Submission Date
• Folder Date
• Filename
Before recording receipt information, the workflow searches for an existing spreadsheet
named Receipt Automation.
If the spreadsheet exists, it reuses it. Otherwise, it creates a new spreadsheet and uses the
resulting Spreadsheet ID for the logging process.
Technologies Used
• n8n – Workflow automation and integration platform.
• Telegram Bot API – Receipt image submission and message triggering.
• Google Gemini – AI-powered receipt image analysis and data extraction.
• JavaScript – JSON parsing, data processing, and filename generation.
• Google Sheets – Structured receipt data logging.
• Google Drive – Receipt image storage and folder organization.
Credential and Environment Setup
The exported workflow does not intentionally include private authentication secrets.
When importing the workflow into another n8n instance, configure the following
credentials:
• Telegram
• Google Gemini API
• Google Drive OAuth2
• Google Sheets OAuth2
Telegram Bot Setup
1. Create a Telegram bot using BotFather.
2. Copy the generated bot token.
3. Create a Telegram credential in n8n using the bot token.
4. Assign the credential to the Telegram Trigger node.
5. Send a test receipt image to the bot.
The Telegram bot token is not included in the exported workflow.
Google Services Setup
1. Configure Google Gemini API credentials.
2. Connect a Google Drive account.
3. Connect a Google Sheets account.
4. Ensure the connected accounts have the necessary permissions to create folders,
upload files, create spreadsheets, and append records.
Import and Testing
To test the workflow in another n8n instance:
1. Import the telegram-receipt-processor.json workflow file.
2. Configure the required credentials.
3. Connect the evaluator's own Telegram bot.
4. Verify the Google Drive and Google Sheets connections.
5. Send a sample receipt image through Telegram.
6. Execute the workflow and verify the extracted information.
7. Check the resulting Google Sheets record and Google Drive folder.
Portfolio Files
This repository contains:
• telegram-receipt-processor.json – Exported n8n workflow.
• screenshots/ – Workflow structure and sample execution screenshots.
• README.md – Project documentation.
Security Note
No API keys, passwords, Telegram bot tokens, or other private authentication secrets are
intentionally included in the portfolio files.
Users importing the workflow must configure their own credentials and connected
accounts.
Conclusion
This project demonstrates practical workflow automation using AI-powered image
analysis, JavaScript data processing, Telegram integration, and Google Workspace
services.
It focuses on automating receipt information extraction, structured transaction logging,
and organized cloud-based image storage.
