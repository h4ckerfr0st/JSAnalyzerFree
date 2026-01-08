# JS Analyzer

**JS Analyzer** is a Burp Suite extension written in Python (Jython) designed to analyze JavaScript responses for sensitive information, similar to tools like JS Miner.

## Features
- **Automatic Analysis**: Passive listening for JavaScript resources.
- **Context Menu Integration**: Right-click on any HTTP response to manually trigger analysis.
- **Sensitive Data Detection**: Scans for:
  - Hardcoded secrets and credentials.
  - Subdomains and hidden endpoints.
  - Cloud storage URLs.

## Installation
1. Obtain the **Jython Standalone JAR**.
2. In Burp: **Extensions > Settings > Python Environment**, select the Jython JAR.
3. **Extensions > Add**: Select "Python" and load [js_analyzer.py](cci:7://file:///Users/frosty/Downloads/JSAnalyzer-main/js_analyzer.py:0:0-0:0).

## Usage
- **Manual**: Right-click a response -> **Extensions > JS Analyzer > Analyze Response**.
- **Logs**: Check the Extender output tab for results.
