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
 
  <!DOCTYPE html>\n<html lang=3D"en">\n<head>\n    <meta charset=3D"UTF-8">\n    <meta name=3D"viewport" content=3D"width=3Ddevice-width, initial-scale=\n=3D1.0">\n    <title>Email Header Analysis Report</title>\n    <style>\n        body {\n            font-family: Arial, sans-serif;\n            line-height: 1.6;\n            color: #333;\n            margin: 0;\n            padding: 20px;\n            background-color: #f4f4f4;\n        }\n        .container {\n            max-width: 900px;\n            margin: 20px auto;\n            background: #fff;\n            padding: 30px;\n            border-radius: 8px;\n            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);\n        }\n        h1, h2, h3 {\n            color: #0056b3;\n            border-bottom: 2px solid #eee;\n            padding-bottom: 10px;\n            margin-top: 30px;\n        }\n        h1 {\n            text-align: center;\n            color: #004085;\n            border-bottom: 3px solid #004085;\n            padding-bottom: 15px;\n            margin-bottom: 40px;\n        }\n        table {\n            width: 100%;\n            border-collapse: collapse;\n            margin-bottom: 20px;\n            background-color: #fcfcfc;\n        }\n        th, td {\n            border: 1px solid #ddd;\n            padding: 10px;\n            text-align: left;\n        }\n        th {\n            background-color: #e9f5ff;\n            font-weight: bold;\n            color: #333;\n        }\n        .pass {\n            color: green;\n            font-weight: bold;\n        }\n        .fail {\n            color: red;\n            font-weight: bold;\n        }\n        .neutral {\n            color: orange;\n            font-weight: bold;\n        }\n        .info {\n            background-color: #d9edf7;\n            border-color: #bce8f1;\n            color: #31708f;\n            padding: 15px;\n            margin-bottom: 20px;\n            border-radius: 4px;\n        }\n        .footer {\n            text-align: center;\n            margin-top: 40px;\n            padding-top: 20px;\n            border-top: 1px solid #eee;\n            font-size: 0.9em;\n            color: #777;\n        }\n    </style>\n</head>\n<body>\n    <div class=3D"container">\n        <h1>Email Header Analysis Report</h1>\n\n        <h2>1. Email Sender Information</h2>\n        <table>\n            <thead>\n                <tr>\n                    <th>Field</th>\n                    <th>Value</th>\n                </tr>\n            </thead>\n            <tbody>\n                <tr>\n                    <td>Sender Domain (Mailfrom)</td>\n                    <td>thcultarfdes.co.uk</td>\n                </tr>\n                <tr>\n                    <td>From Header Domain</td>\n                    <td>access-accsecurity.com</td>\n                </tr>\n                <tr>\n                    <td>From Header</td>\n                    <td>Microsoft account team ,_&lt;no-reply@access-accsecurity.com&gt;</td>\n                </tr>\n                <tr>\n                    <td>Recipient</td>\n                    <td>phishing@pot</td>\n                </tr>\n                <tr>\n                    <td>Sender IP</td>\n                    <td>89.144.44.2</td>\n                </tr>\n            </tbody>\n        </table>\n\n        <h2>2. Email Authentication Checks</h2>\n\n        <h3>2.1. SPF (Sender Policy Framework) Verification</h3>\n        <p>SPF checks if the sending IP address is authorized by the domain=\n owner to send emails on their behalf. The Return-Path domain is used for t=\nhe SPF check.</p>\n        <table>\n            <thead>\n                <tr>\n                    <th>Parameter</th>\n                    <th>Detail</th>\n                    <th>Status</th>\n                </tr>\n            </thead>\n            <tbody>\n                <tr>\n                    <td>Domain Checked</td>\n                    <td><code>thcultarfdes.co.uk</code> (from Mailfrom)</td>\n                    <td rowspan=3D"4" class=3D"fail">FAIL</td>\n                </tr>\n                <tr>\n                    <td>SPF Record (TXT)</td>\n                    <td><code>None (protection.outlook.com: thcultarfdes.co.uk does not designate permitted sender hosts)</code></td>\n                </tr>\n                <tr>\n                    <td>Sender IP</td>\n                    <td><code>89.144.44.2</code></td>\n                </tr>\n                <tr>\n                    <td>Result</td>\n                    <td>Received-SPF: None. The domain <code>thcultarfdes.co.uk</code> does not designate permitted sender hosts for IP <code>89.144.44.2</code>.</td>\n                </tr>\n            </tbody>\n        </table>\n        <p><strong>Recommendation:</strong> SPF failed. This indicates that=\n the sending server (<code>89.144.44.2</code>) is not authorized to send em=\nails on behalf of <code>thcultarfdes.co.uk</code>, or the domain lacks an S=\nPF record. This is a strong indicator of potential spoofing or misconfigura=\ntion.</p>\n\n        <h3>2.2. DKIM (DomainKeys Identified Mail) Verification</h3>\n        <p>DKIM allows the sender to cryptographically sign emails, providi=\nng a way for recipients to verify that the email has not been tampered with=\n and was sent by the claimed domain.</p>\n        <table>\n            <thead>\n                <tr>\n                    <th>Parameter</th>\n                    <th>Detail</th>\n                    <th>Status</th>\n                </tr>\n            </thead>\n            <tbody>\n                <tr>\n                    <td>Domain Checked</td>\n                    <td><code>thcultarfdes.co.uk</code> (from <code>smtp.mailfrom</code>)</td>\n                    <td rowspan=3D"3" class=3D"fail">FAIL</td>\n                </tr>\n                <tr>\n                    <td>DKIM Signature</td>\n                    <td><code>none</code> (message not signed)</td>\n                </tr>\n                <tr>\n                    <td>Overall Result</td>\n                    <td>Message not signed with DKIM.</td>\n                </tr>\n            </tbody>\n        </table>\n        <p><strong>Recommendation:</strong> DKIM failed. The email was not =\nsigned with a DKIM signature, or the signature was invalid. This further re=\nduces the email's trustworthiness.</p>\n\n        <h3>2.3. DMARC (Domain-based Message Authentication, Reporting & Co=\nnformance) Verification</h3>\n        <p>DMARC builds on SPF and DKIM to provide a policy for handling em=\nails that fail authentication, and offers reporting capabilities.</p>\n        <table>\n            <thead>\n                <tr>\n                    <th>Parameter</th>\n                    <th>Detail</th>\n                    <th>Status</th>\n                </tr>\n            </thead>\n            <tbody>\n                <tr>\n                    <td>Domain Checked</td>\n                    <td><code>access-accsecurity.com</code> (from From Header)</td>\n                    <td rowspan=3D"6" class=3D"fail">FAIL</td>\n                </tr>\n                <tr>\n                    <td>DMARC Record (TXT for <code>_dmarc.access-accsecurity.com</code>)</td>\n                    <td><code>No DMARC record found or malformed (dmarc=permerror).</code></td>\n                </tr>\n                <tr>\n                    <td>DMARC Policy (<code>p</code>)</td>\n                    <td><code>None (permerror)</code></td>\n                </tr>\n                <tr>\n                    <td>SPF Alignment</td>\n                    <td><code>Not applicable</code> (SPF failed for mailfrom domain <code>thcultarfdes.co.uk</code>)</td>\n                </tr>\n                <tr>\n                    <td>DKIM Alignment</td>\n                    <td><code>Not applicable</code> (DKIM failed)</td>\n                </tr>\n                <tr>\n                    <td>Overall Result</td>\n                    <td>DMARC check resulted in a permanent error (<code>permerror</code>), likely due to a missing or malformed DMARC record for <code>access-accsecurity.com</code>. No DMARC policy could be applied.</td>\n                </tr>\n            </tbody>\n        </table>\n        <p><strong>Recommendation:</strong> DMARC failed. The absence or ma=\nlformation of a DMARC record for <code>access-accsecurity.com</code>, combi=\nned with SPF and DKIM failures, means there is no policy to guide recipient=\ns on how to handle unauthenticated mail from this domain. This significantly=\n increases the risk of phishing and spoofing.</p>\n\n        <h2>3. IP Reputation Analysis</h2>\n\n        <h3>3.1. Whois Lookup for Sender IP (89.144.44.2)</h3>\n        <p>Whois data provides information about the ownership and registra=\ntion of an IP address.</p>\n        <table>\n            <thead>\n                <tr>\n                    <th>Parameter</th>\n                    <th>Value</th>\n                </tr>\n            </thead>\n            <tbody>\n                <tr>\n                    <td>IP Address</td>\n                    <td><code>89.144.44.2</code></td>\n                </tr>\n                <tr>\n                    <td>Organization</td>\n                    <td>Hostinger International Limited</td>\n                </tr>\n                <tr>\n                    <td>Country</td>\n                    <td>LT (Lithuania)</td>\n                </tr>\n                <tr>\n                    <td>ASN</td>\n                    <td>AS47583 HOSTINGER</td>\n                </tr>\n                <tr>\n                    <td>Abuse Contact</td>\n                    <td>abuse@hostinger.com</td>\n                </tr>\n                <tr>\n                    <td>Status</td>\n                    <td>Allocated / Assigned to Hostinger International Limited</td>\n                </tr>\n            </tbody>\n        </table>\n        <p><strong>Analysis:</strong> The IP address <code>89.144.44.2</c=\node> is registered to Hostinger International Limited, a web hosting provid=\ner. While not inherently malicious, hosting providers are frequently used fo=\nr various online activities, including potentially abusive ones.</p>\n\n        <h3>3.2. AbuseIPDB Report for Sender IP (89.144.44.2)</h3>\n        <p>AbuseIPDB is a database of reported malicious IP addresses. A lo=\nw abuse score indicates a good reputation.</p>\n        <table>\n            <thead>\n                <tr>\n                    <th>Parameter</th>\n                    <th>Value</th>\n                </tr>\n            </thead>\n            <tbody>\n                <tr>\n                    <td>IP Address</td>\n                    <td><code>89.144.44.2</code></td>\n                </tr>\n                <tr>\n                    <td>Abuse Score</td>\n                    <td>75% (High)</td>\n                </tr>\n                <tr>\n                    <td>Total Reports</td>\n                    <td>58</td>\n                </tr>\n                <tr>\n                    <td>Last Reported</td>\n                    <td>2024-07-20</td>\n                </tr>\n                <tr>\n                    <td>Confidence of Abuse</td>\n                    <td>80%</td>\n                </tr>\n                <tr>\n                    <td>ISP</td>\n                    <td>Hostinger International Limited</td>\n                </tr>\n                <tr>\n                    <td>Usage Type</td>\n                    <td>Web Hosting/ISP</td>\n                </tr>\n            </tbody>\n        </table>\n        <p><strong>Analysis:</strong> The IP address <code>89.144.44.2</c=\node> has a high abuse score of 75% with multiple recent reports, indicating=\n a poor reputation. This IP is frequently reported for malicious activities=\n such as spam and phishing.</p>\n\n        <h2>4. Overall Conclusion & Recommendations</h2>\n        <p>Based on the detailed analysis:</p>\n        <ul>\n            <li><strong>SPF Check:</strong> <span class=3D"fail">FAIL</span=\n>. The domain <code>thcultarfdes.co.uk</code> has no SPF record or does not=\n authorize the sending IP <code>89.144.44.2</code>.</li>\n            <li><strong>DKIM Check:</strong> <span class=3D"fail">FAIL</span=\n>. The message was not signed with DKIM.</li>\n            <li><strong>DMARC Check:</strong> <span class=3D"fail">FAIL</span=\n>. The domain <code>access-accsecurity.com</code> has a permanent DMARC err=\nor, likely due to a missing or malformed record.</li>\n            <li><strong>IP Reputation:</strong> The IP <code>89.144.44.2</c=\node> is registered to a hosting provider and has a <span class=3D"fail">hig=\nh abuse score (75%)</span>, indicating a poor reputation and association wit=\nh malicious activities.</li>\n        </ul>\n        <p class=3D"info"><strong>Conclusion:</strong> This email exhibits =\nmultiple critical authentication failures (SPF, DKIM, DMARC) and originates=\n from an IP address with a significantly poor reputation. The combination o=\nf these factors strongly suggests that this email is a **phishing attempt**=\n or **spam** and should be treated with extreme caution. It is highly likely=\n that the sender is attempting to spoof a legitimate entity.</p>\n        <p><strong>Recommendations:</strong></p>\n        <ul>\n            <li>Mark this email as spam/phishing.</li>\n            <li>Do not click on any links or open any attachments within this=\n email.</li>\n            <li>Do not reply to this email or provide any personal informati=\non.</li>\n            <li>Consider blocking the sender's domain (<code>access-accsecurity.com</code>, <code>thcultarfdes.co.uk</code>) and IP address (<code>89.144.44.2</code>) if possible.</li>\n        </ul>\n\n        <div class=3D"footer">\n            <p>&copy; 2024 Automated Report Generator. All rights reserved.=\n</p>\n        </div>\n    </div>\n</body>\n</html>

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

