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
 
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Email Header Analysis Report</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            color: #333;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }

        .container {
            max-width: 900px;
            margin: 20px auto;
            background: #fff;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        h1, h2, h3 {
            color: #0056b3;
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
            margin-top: 30px;
        }

        h1 {
            text-align: center;
            color: #004085;
            border-bottom: 3px solid #004085;
            padding-bottom: 15px;
            margin-bottom: 40px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
            background-color: #fcfcfc;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 10px;
            text-align: left;
            vertical-align: top;
        }

        th {
            background-color: #e9f5ff;
            font-weight: bold;
        }

        .pass {
            color: green;
            font-weight: bold;
        }

        .fail {
            color: red;
            font-weight: bold;
        }

        .neutral {
            color: orange;
            font-weight: bold;
        }

        .info {
            background-color: #d9edf7;
            border-left: 5px solid #31708f;
            color: #31708f;
            padding: 15px;
            margin: 20px 0;
            border-radius: 4px;
        }

        .footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            font-size: 0.9em;
            color: #777;
        }

        code {
            background-color: #f8f8f8;
            padding: 2px 5px;
            border-radius: 4px;
            font-family: Consolas, monospace;
        }
    </style>
</head>

<body>
<div class="container">

    <h1>Email Header Analysis Report</h1>

    <h2>1. Email Sender Information</h2>
    <table>
        <thead>
            <tr>
                <th>Field</th>
                <th>Value</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Sender Domain (Mailfrom)</td>
                <td>thcultarfdes.co.uk</td>
            </tr>
            <tr>
                <td>From Header Domain</td>
                <td>access-accsecurity.com</td>
            </tr>
            <tr>
                <td>From Header</td>
                <td>Microsoft account team &lt;no-reply@access-accsecurity.com&gt;</td>
            </tr>
            <tr>
                <td>Recipient</td>
                <td>phishing@pot</td>
            </tr>
            <tr>
                <td>Sender IP</td>
                <td>89.144.44.2</td>
            </tr>
        </tbody>
    </table>

    <h2>2. Email Authentication Checks</h2>

    <h3>2.1 SPF (Sender Policy Framework)</h3>
    <p>
        SPF verifies whether the sending IP address is authorized by the domain
        owner to send emails on its behalf.
    </p>

    <table>
        <thead>
            <tr>
                <th>Parameter</th>
                <th>Detail</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Domain Checked</td>
                <td><code>thcultarfdes.co.uk</code></td>
                <td rowspan="4" class="fail">FAIL</td>
            </tr>
            <tr>
                <td>SPF Record</td>
                <td>
                    None – domain does not designate permitted sender hosts
                </td>
            </tr>
            <tr>
                <td>Sender IP</td>
                <td><code>89.144.44.2</code></td>
            </tr>
            <tr>
                <td>Result</td>
                <td>
                    SPF validation failed for the sending IP.
                </td>
            </tr>
        </tbody>
    </table>

    <p>
        <strong>Recommendation:</strong>
        SPF failed, indicating potential spoofing or misconfiguration.
    </p>

    <h3>2.2 DKIM (DomainKeys Identified Mail)</h3>
    <table>
        <thead>
            <tr>
                <th>Parameter</th>
                <th>Detail</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Domain Checked</td>
                <td><code>thcultarfdes.co.uk</code></td>
                <td rowspan="3" class="fail">FAIL</td>
            </tr>
            <tr>
                <td>DKIM Signature</td>
                <td>None</td>
            </tr>
            <tr>
                <td>Result</td>
                <td>Message not signed with DKIM.</td>
            </tr>
        </tbody>
    </table>

    <h3>2.3 DMARC</h3>
    <table>
        <thead>
            <tr>
                <th>Parameter</th>
                <th>Detail</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Domain Checked</td>
                <td><code>access-accsecurity.com</code></td>
                <td rowspan="5" class="fail">FAIL</td>
            </tr>
            <tr>
                <td>DMARC Record</td>
                <td>No valid DMARC record found</td>
            </tr>
            <tr>
                <td>Policy</td>
                <td>permerror</td>
            </tr>
            <tr>
                <td>SPF Alignment</td>
                <td>Failed</td>
            </tr>
            <tr>
                <td>DKIM Alignment</td>
                <td>Failed</td>
            </tr>
        </tbody>
    </table>

    <h2>3. IP Reputation Analysis</h2>

    <h3>Sender IP: 89.144.44.2</h3>
    <ul>
        <li><strong>ISP:</strong> Hostinger International Limited</li>
        <li><strong>Country:</strong> Lithuania</li>
        <li><strong>ASN:</strong> AS47583</li>
        <li><strong>Abuse Score:</strong> <span class="fail">75%</span></li>
    </ul>

    <h2>4. Final Verdict</h2>

    <div class="info">
        <strong>Conclusion:</strong>
        This email fails SPF, DKIM, and DMARC checks and originates from an IP
        with a poor reputation. It is highly likely to be a phishing attempt.
    </div>

    <ul>
        <li>Mark the email as phishing.</li>
        <li>Do not click links or open attachments.</li>
        <li>Block the sender domains and IP if possible.</li>
    </ul>

    <div class="footer">
        &copy; 2024 Automated Report Generator
    </div>

</div>
</body>
</html>

 

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

