# JS Analyzer

**JS Analyzer** is a comprehensive Burp Suite extension written in Python (Jython) that acts as a powerful passive scanner for JavaScript code. Heavily inspired by the industry-standard **JS Miner**, this tool goes deep into client-side code to extract sensitive data, map the application surface, and identify potential vulnerabilities.

It is designed to automate the tedious process of auditing JavaScript files, saving you hours of manual review by surfacing critical finds directly in your Burp issues.

## Key Capabilities

### 1. Advanced Secrets & Credential Harvesting
Automatically scans for high-entropy strings and known patterns to catch hardcoded secrets before they go to production.
*   **API Keys** (AWS, Google Maps, Stripe, Slack, etc.)
*   **Private Tokens** (JWTs, Bearer tokens)
*   **Password/Credential Pairs**

### 2. Dependency & Version Enumeration ("The Big One")
Identifies common JavaScript libraries and frameworks in use, extracting their specific versions to help you spot outdated or vulnerable components immediately.
*   **Extracts Library Names & Versions** (e.g., *jQuery 1.12.4*, *React 16.8.0*, *AngularJS 1.5*)
*   **Fingerprints Frameworks**
*   **Detects Vulnerable Outdated Dependencies** (similar to Retire.js logic)

### 3. Enumeration & Discovery
*   **Endpoint Extraction**: Uses regex to pull out full URLs, relative paths, and API endpoints hidden in the code.
*   **Subdomain Discovery**: Finds referenced subdomains (e.g., `dev.api.target.com`, `staging.target.com`) that might not be linked elsewhere.
*   **Cloud Storage Buckets**: Identifies S3 buckets, Azure blobs, and Google Cloud storage links.

### 4. Source Map & Debug Logic
*   **Source Map Detection**: Alerts if `.map` files are available, allowing you to reconstruct the original source code.
*   **Inline Source Code**: Flags inline scripts within HTML responses.

## Installation

**Important API Note**: Burp Suite is written in Java. To run Python extensions like this one, you **MUST** install and configure Jython (Java Python).

1.  **Download Jython**:
    *   Go to the [Jython Official Website](https://www.jython.org/download).
    *   Download the **Jython Standalone JAR** (e.g., `jython-standalone-2.7.3.jar`). This is required; the standard Python installed on your OS will not work with Burp Suite.

2.  **Configure Burp Suite**:
    *   Open Burp Suite.
    *   Navigate to **Extensions** > **Extensions Settings**.
    *   Locate the **Python Environment** section.
    *   Click **Select file** and browse to the location where you saved the `jython-standalone-*.jar` file.

3.  **Load the Extension**:
    *   Go to **Extensions** > **Installed**.
    *   Click **Add**.
    *   Set **Extension Type** to **Python**.
    *   Click **Select file** and choose `js_analyzer.py`.
    *   Click **Next**. The output window should show: `JS Analyzer loaded`.

## Usage

### Automatic Passive Scanning
Just browse your target application. JS Analyzer runs in the background. When it sees an HTTP response containing JavaScript (header `Content-Type: javascript` or file extension `.js`), it kicks in automatically.

### Manual Analysis
If you want to re-scan a specific request or analyze a file you suspect was missed:
1.  Right-click the request/response in **Proxy** or **Repeater**.
2.  Select **Extensions** > **JS Analyzer** > **Analyze Response**.

## Example Findings

When usage is detected, alerts usually appear in the **Issue Activity** dashboard or the **Extensions Output** tab.

**Example Log Output:**
```text
[ OFFICIAL JS Analyzer] [+] Analyzing: https://target.com/assets/app.js
[ OFFICIAL JS Analyzer] [!] FOUND API KEY: AKIAIOSFODNN7EXAMPLE (Line 405)
[ OFFICIAL JS Analyzer] [i] Library Identified: jQuery - Version 3.5.1
[ OFFICIAL JS Analyzer] [i] Endpoint Discovered: /api/v1/users/login
```

## Contributing
Found a bug? Want to add a new regex pattern?
1.  Fork the repo
2.  Create your feature branch (`git checkout -b feature/NewPattern`)
3.  Commit your changes
4.  Push to the branch
5.  Create a new Pull Request
