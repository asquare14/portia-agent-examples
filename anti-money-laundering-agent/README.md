# Anti Money Laundering Agent


### Glossary

- **AML (Anti-Money Laundering)**: A set of laws, regulations, and procedures designed to prevent criminals from disguising illegally obtained funds as legitimate income. AML processes include transaction monitoring, customer due diligence (CDD), and reporting suspicious activity.

- **Open Banking**: A financial services framework that allows banks to securely share customer data (with consent) through APIs. It enables third-party providers to offer innovative financial services, such as budgeting tools, payment initiation, and account aggregation.

- **EnableBanking**: A platform that provides a unified API for accessing financial data and initiating payments across multiple banks through open banking protocols. Often used by fintechs and compliance systems to streamline connectivity with multiple banks.

- **SAR (Suspicious Activity Report)**: A document filed by financial institutions to report suspicious transactions that may indicate money laundering, terrorist financing, or other criminal activities.

- **MCP (Model Context Protocol)**: A standardized way for applications to provide context and tools to Large Language Models, enabling AI agents to interact with external systems and data sources.


## Overview

An intelligent AI agent that automates Anti-Money Laundering (AML) compliance by analyzing Open Banking transaction data and generating Suspicious Activity Reports (SARs) for regulatory compliance.

## 🎯 Project Goals

### Primary Objectives
- **Automate AML Monitoring**: Continuously analyze transaction patterns for suspicious activity
- **Regulatory Compliance**: Generate UK-compliant SAR reports for the National Crime Agency (NCA)
- **Real-time Detection**: Identify money laundering risks as they occur
- **Reduce Manual Work**: Eliminate the need for manual transaction review

### Business Value
- **Cost Reduction**: Automate expensive manual compliance processes
- **Risk Mitigation**: Catch suspicious activity faster than manual review
- **Regulatory Adherence**: Ensure compliance with UK AML regulations
- **Scalability**: Handle large volumes of transactions efficiently

## 🏗️ Architecture

### Core Components
1. **Financial Data Agent**: AI agent that gets the banking transactions.
2. **Open Banking MCP Server**: — MCP service layering on a custom EnableBanking client to provide AI-accessible tools for financial data access and payments.
Tools: fetch_accounts, fetch_transactions, complete_authorization
3. **AML Analysis Engine**: AI agent that flags transactions as AML.
4. **SAR Report Generator**: AI agent that generates automated regulatory report creation.

### Data Flow

1. **Financial Agent asked to get transaction** – User or system triggers a fetch request for recent banking transactions.
2. **MCP Layer** – MCP server handles the API request to the connected bank via Open Banking APIs.
3. **OAuth Consent** – MCP initiates secure OAuth flow for account access.
4. **User Interaction** – User is prompted to authorize and paste the **access token** back into the system.
5. **Resume Process** – MCP validates the token and securely retrieves the requested transaction data.
6. **Transaction Formatting** – Normalize and clean transaction data into a consistent internal schema.
7. **Compliance Agent** – Analyze transactions for AML risks and generate flagged vs. clean transaction sets.
8. **SAR Generator Agent** – Convert flagged transactions into a structured SAR payload and human-readable narrative.
9. **Email Notification** – Automatically email the SAR report to compliance officers or a secure mailbox.

## How you can use it


### Prerequisites
- Python 3.8+
- Portia API key
- OpenAI API key
- Open Banking credentials (EnableBanking)
- Private key file from Enable Banking (.pem)

### Setup enable banking

1. Go to https://enablebanking.com/cp/applications and create an application.
2. Add http://127.0.0.1:8765/callback in allowed redirect uris.
3. Once your app is created, download a pem file and the app-id and keep it handy for running the application.
4. Add these to openbanking_config.py along with email that you want SAR report to go to.
5. Next go to https://enablebanking.com/cp/mock-aspsp
6. Create a mock account and mock transactions.
7. You can use chatgpt to generate mock shady transactions.

## 🐬 Running locally using docker


### Running locally
```bash
# Install dependencies
uv sync

# Start OAuth callback server in terminal 1
uv run oauth_callback_server.py

# Run MCP server in terminal 2
uv run mcp run openbanking_mcp/openbanking_mcp_server.py

# Execute main agent in terminal 3
uv run main.py
```

## 📁 Project Structure

```
anti-money-laundering-agent/
├── main.py                          # Main agent execution
├── oauth_callback_server.py         # OAuth authorization handler
├── openbanking-mcp/                 # Open Banking MCP server
│   ├── openbanking_mcp_server.py   # MCP server implementation
│   ├── openbanking_mcp_tool.py     # Open Banking API tools
│   └── openbanking_client.py       # EnableBanking client
├── aml_suspicious_activity_report_agent.py  # SAR generation logic
├── aml_financial_data_agent.py     # Gets transactions from open banking
├── aml_compliance_agent.py         # Checks for compliance
├── pydantic_base_models.py 
├── pyproject.toml                   # Project dependencies
└── README.md                        # This file
```

## 🔧 Configuration

### Environment Variables
```bash
PORTIA_API_KEY=your_portia_key
OPENAI_API_KEY=your_openai_key
OPENBANKING_APP_ID=your_enablebanking_app_id
```

### Private Key
Store your `.pem` file securely and reference it in your configuration.

## 📈 Future Enhancements

* **Real-Time Intelligence** – Instant detection and alerts for suspicious transactions, empowering teams to act the moment risk is identified.
* **Global Compliance Ready** – Seamlessly adapts to international regulations, from FCA and FinCEN to FATF frameworks, ensuring worry-free scalability.
* **Plug-and-Play Integration** – Easily connects to any financial platform, core banking system, or payment processor with minimal setup.
* **Next-Gen Dashboard** – A sleek, interactive interface delivering real-time analytics, risk scoring, and one-click SAR generation.

## 🤝 Contributing

This project follows standard open-source contribution guidelines. Please ensure all code changes maintain security and compliance standards.