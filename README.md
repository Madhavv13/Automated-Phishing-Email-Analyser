# Phishing Email Analyzer

An automated workflow for analyzing and reporting on potential phishing emails. This n8n workflow processes email headers and content to detect suspicious patterns, verify sender authenticity, and generate comprehensive security reports.

<img width="1097" height="374" alt="image" src="https://github.com/user-attachments/assets/4f6a8214-97e2-4f1b-b19e-171b8c4427a7" />


## Features

- **Header Analysis**: Examines email headers for SPF, DKIM, DMARC, and ARC authentication
- **URL Scanning**: Automatically extracts and scans URLs within emails using urlscan.io
- **File Analysis**: Checks attachments and embedded files for malicious content
- **Automated Reporting**: Generates detailed HTML reports with security findings
- **Email Notifications**: Sends analysis results to specified email addresses

## How It Works

1. **Input Processing**: Accepts email data including headers and content
   <img width="581" height="392" alt="image" src="https://github.com/user-attachments/assets/5391283f-962a-41d4-883e-642e72a46e8a" />

3. **Authentication Checks**:
   - SPF (Sender Policy Framework) verification
   - DKIM (DomainKeys Identified Mail) validation
   - DMARC (Domain-based Message Authentication) analysis
   - ARC (Authenticated Receive Chain) validation
4. **Content Analysis**:
   - Extracts and examines all URLs
   - Scans for known phishing indicators
   - Analyzes email structure for suspicious patterns
5. **Report Generation**: Creates a professional HTML report with:
   - Sender information and verification status
   - Authentication check results
   - URL analysis with safety ratings
   - File attachment analysis
   - Overall risk assessment

## Prerequisites

- n8n instance (self-hosted or cloud)
- API keys for:
  - virustotal.com (for File scanning)
  - urlscan.io (for URL scanning)
  - Google Gemini (for advanced analysis)
  - Email service (for sending reports)

## Installation

1. Clone this repository
2. Import the workflow into your n8n instance
3. Configure the required credentials:
   - virustotal API
   - urlscan.io API
   - Google Gemini API
   - Email service (SMTP or other)
5. Update the recipient email address in the workflow

## Usage

1. Send the email you want to analyze to the workflow's webhook URL
2. The workflow will automatically process the email
3. A detailed report will be generated and sent to the configured email address

## Report Contents

Each report includes:

- **Email Sender Information**
  - Sender domain
  - Return-Path
  - From header
  - Sender IP address


- **Email Authentication Checks**
  - SPF verification results
  - DKIM validation
  - DMARC compliance
  - ARC validation

- **URL Analysis**
  - List of all URLs found in the email
  - Safety status for each URL
  - Screenshots of landing pages
  - Link to full urlscan.io report

- **File Analysis** (if attachments present)
  - File hashes
  - Malware detection results
  - Threat intelligence data

## Customization

You can modify the workflow to:
- Add additional analysis steps
- Change the report format
- Integrate with other security tools
- Adjust notification settings

## Security Considerations

- Store API keys securely using n8n's credential system
- Limit access to the workflow's webhook URL
- Regularly update the workflow to include the latest threat intelligence



## Acknowledgements

- Built with [n8n](https://n8n.io/)
- URL scanning powered by [urlscan.io](https://urlscan.io/)
- File Scanning powered by[VirusTotal.com](https://www.virustotal.com/gui/home/upload)
- AI analysis powered by [Google Gemini](https://ai.google/)

---

