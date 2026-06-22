# Bank Statement Analyzer
A Python tool that turns a raw bank statement into a clean, categorized financial report automatically. It reads transactions from an Excel file, classifies each one into an income or expense category, and generates a formatted, two-sheet report with a profit and loss summary.

The problem:
Bank statements are messy. Transaction descriptions are full of cryptic merchant codes (SQ *BLUEBOTTLE 4412, TST* THE DAILY GRIND, AMZN MKTP US*2A4TY8) that make manual bookkeeping slow and error-prone. This tool automates the categorization and reporting, turning a statement full of raw rows into an organized P&L in seconds.

How it works:
The classifier uses a hybrid, two-layer approach:
Rule-based layer — A keyword dictionary maps common merchants and terms to categories (for example, "aws" and "github" map to Software & SaaS). This layer is fast, free, deterministic, and fully transparent, and it handles the majority of transactions.
AI layer - Only the transactions the rules cannot match are sent to the OpenAI API (gpt-4o-mini), which reads the context the way a person would and assigns the remaining ambiguous descriptions.

This design keeps cost minimal, the AI only touches the hard cases, while keeping results explainable. It mirrors the pattern used in production classification systems: cheap, transparent logic for the bulk of the work, and a model reserved for the difficult edge cases.

Output:
The tool generates a formatted Excel report with two sheets:
Transactions — every transaction with its assigned category
P&L Summary — totals by category, with a calculated net income

Tech stack:
Python
pandas — data processing
openpyxl — Excel reading, writing, and formatting
OpenAI API — AI-assisted classification
Jupyter Notebook — development and exploration

Usage:

Install dependencies: pip install pandas openpyxl openai

Place your bank statement (an Excel file with Date, Description, and Amount columns) in the project folder.
Run the notebook. You will be prompted for your OpenAI API key, entered securely via getpass — it is never stored in the file. The tool outputs output_report.xlsx.

Note on data
The included bank_statement.xlsx is synthetic sample data, created for demonstration. No real financial data is used in this repository.


Built by Naumenko Analytics — applied data and analytics solutions.