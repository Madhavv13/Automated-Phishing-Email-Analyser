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
 
  <h1 align="center">Email & Phishing Analysis Report</h1>

<hr>

<h2>1. Email Sender Information</h2>

<table>
  <tr><th align="left">Field</th><th align="left">Value</th></tr>
  <tr><td>Sender Domain (Mailfrom)</td><td>thcultarfdes.co.uk</td></tr>
  <tr><td>From Header Domain</td><td>access-accsecurity.com</td></tr>
  <tr>
    <td>From Header</td>
    <td>Microsoft account team &lt;no-reply@access-accsecurity.com&gt;</td>
  </tr>
  <tr><td>Recipient</td><td>phishing@pot</td></tr>
  <tr><td>Sender IP</td><td>89.144.44.2</td></tr>
</table>

<hr>

<h2>2. Email Authentication Checks</h2>

<h3>2.1 SPF (Sender Policy Framework)</h3>

<p>
SPF verifies whether the sending IP address is authorized to send email on
behalf of the MAIL FROM domain.
</p>

<table>
  <tr>
    <th align="left">Parameter</th>
    <th align="left">Detail</th>
    <th align="left">Status</th>
  </tr>
  <tr>
    <td>Domain Checked</td>
    <td><code>thcultarfdes.co.uk</code></td>
    <td rowspan="4" style="color:red;"><b>FAIL</b></td>
  </tr>
  <tr>
    <td>SPF Record</td>
    <td colspan="2">
      None – domain does not designate permitted sender hosts
    </td>
  </tr>
  <tr>
    <td>Sender IP</td>
    <td colspan="2"><code>89.144.44.2</code></td>
  </tr>
  <tr>
    <td>Result</td>
    <td colspan="2">
      IP not authorized to send email
    </td>
  </tr>
</table>

<p>
<b>Recommendation:</b>
SPF failure strongly indicates spoofing or sender misconfiguration.
</p>

<hr>

<h3>2.2 DKIM (DomainKeys Identified Mail)</h3>

<p>
DKIM verifies message integrity and authenticates the sending domain using
cryptographic signatures.
</p>

<table>
  <tr>
    <th align="left">Parameter</th>
    <th align="left">Detail</th>
    <th align="left">Status</th>
  </tr>
  <tr>
    <td>Domain Checked</td>
    <td><code>thcultarfdes.co.uk</code></td>
    <td rowspan="3" style="color:red;"><b>FAIL</b></td>
  </tr>
  <tr>
    <td>DKIM Signature</td>
    <td colspan="2">None (message not signed)</td>
  </tr>
  <tr>
    <td>Overall Result</td>
    <td colspan="2">DKIM authentication failed</td>
  </tr>
</table>

<p>
<b>Recommendation:</b>
Missing DKIM further reduces email trustworthiness.
</p>

<hr>

<h3>2.3 DMARC (Domain-based Message Authentication)</h3>

<p>
DMARC builds on SPF and DKIM to enforce authentication alignment and define
handling policies for failed messages.
</p>

<table>
  <tr>
    <th align="left">Parameter</th>
    <th align="left">Detail</th>
    <th align="left">Status</th>
  </tr>
  <tr>
    <td>Domain Checked</td>
    <td><code>access-accsecurity.com</code></td>
    <td rowspan="6" style="color:red;"><b>FAIL</b></td>
  </tr>
  <tr>
    <td>DMARC Record</td>
    <td colspan="2">Missing or malformed (permerror)</td>
  </tr>
  <tr>
    <td>Policy</td>
    <td colspan="2">None</td>
  </tr>
  <tr>
    <td>SPF Alignment</td>
    <td colspan="2">Failed</td>
  </tr>
  <tr>
    <td>DKIM Alignment</td>
    <td colspan="2">Failed</td>
  </tr>
  <tr>
    <td>Overall Result</td>
    <td colspan="2">
      No DMARC enforcement possible
    </td>
  </tr>
</table>

<p>
<b>Recommendation:</b>
Absence of DMARC combined with SPF and DKIM failures significantly increases
the risk of phishing and spoofing.
</p>

<hr>

<h2>3. IP Reputation Analysis</h2>

<h3>3.1 Whois Information</h3>

<table>
  <tr><td><b>IP Address</b></td><td><code>89.144.44.2</code></td></tr>
  <tr><td><b>Organization</b></td><td>Hostinger International Limited</td></tr>
  <tr><td><b>Country</b></td><td>Lithuania (LT)</td></tr>
  <tr><td><b>ASN</b></td><td>AS47583</td></tr>
  <tr><td><b>Abuse Contact</b></td><td>abuse@hostinger.com</td></tr>
</table>

<p>
<b>Analysis:</b>
The sender IP belongs to a commercial hosting provider, which is frequently
abused for malicious email campaigns.
</p>

<h3>3.2 AbuseIPDB Reputation</h3>

<table>
  <tr><td><b>Abuse Score</b></td><td style="color:red;"><b>75% (High)</b></td></tr>
  <tr><td><b>Total Reports</b></td><td>58</td></tr>
  <tr><td><b>Last Reported</b></td><td>2024-07-20</td></tr>
  <tr><td><b>Confidence of Abuse</b></td><td>80%</td></tr>
  <tr><td><b>Usage Type</b></td><td>Web Hosting / ISP</td></tr>
</table>

<p>
<b>Analysis:</b>
The IP has a high abuse score and is frequently reported for phishing and
spam-related activity.
</p>

<hr>

<h2>4. Phishing Analysis</h2>

<h3>4.1 URL Analysis</h3>

<table>
  <tr><td><b>URL</b></td><td>null</td></tr>
  <tr><td><b>Name</b></td><td>null</td></tr>
  <tr><td><b>Screenshot</b></td><td>Not available</td></tr>
  <tr><td><b>Verdict</b></td><td style="color:orange;"><b>Unknown</b></td></tr>
  <tr>
    <td><b>Validator</b></td>
    <td>urlscan.io (Full report unavailable)</td>
  </tr>
</table>

<h3>4.2 File Analysis</h3>

<p>
No file attachments were detected or analyzed for this email.
</p>

<hr>

<h2>5. Final Verdict & Recommendations</h2>

<div style="border-left:4px solid red; padding:10px;">
  <b>High-Risk Phishing Email</b><br><br>
  ❌ SPF failed<br>
  ❌ DKIM failed<br>
  ❌ DMARC failed<br>
  🔴 Poor IP reputation<br>
  ⚠️ No trusted URL validation
</div>

<h3>Recommended Actions</h3>

<ul>
  <li>Mark the email as phishing or spam</li>
  <li>Do not click any links or open attachments</li>
  <li>Do not reply or share personal information</li>
  <li>Block sender domains and IP address</li>
</ul>

<hr>

<p align="center">
<b>Automated Email & Phishing Analysis Report</b><br>
Generated via n8n automation<br>
© 2024
</p>


 

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

