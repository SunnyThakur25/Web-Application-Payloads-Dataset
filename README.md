# Web-Application-Payloads-Dataset
A curated dataset of web application attack payloads for red teaming, ML model training, and secure testing — covering SQLi, XSS, command injection, and more.
Web Application Payloads Dataset


Comprehensive dataset for testing web application vulnerabilities

Overview

The Web Application Payloads Dataset (WEB_APPLICATION_PAYLOADS.jsonl) is a curated collection of 300 payloads designed for penetration testing and vulnerability assessment of web applications. It includes payloads for SQL Injection (SQLi), Cross-Site Scripting (XSS), Server-Side Request Forgery (SSRF), and Command Injection (CMDi), making it a valuable resource for cybersecurity professionals, penetration testers, and data scientists working on vulnerability detection models.

Each entry provides detailed metadata, including payload ID, description, context, type, severity, and example usage, enabling precise application in testing scenarios.

Dataset Details





Format: JSON Lines (.jsonl)



Size: 300 entries



Categories:





SQL Injection (SQLi): 100 payloads (tautology, union, blind-time, boolean-blind, error-based, stacked-queries)



Cross-Site Scripting (XSS): 100 payloads (reflected, stored)

Cross-Site Request Forgery(CSRF): 100 payloads

Server-Side Request Forgery (SSRF): 100 payloads (protocol chaining, IP obfuscation, header injection)



Command Injection (CMDi): 100 payloads (Linux/macOS, Windows, PowerShell, reverse shells)



Fields:





id: Unique identifier (e.g., sqli-001, xss-001)



description: Purpose of the payload



payload: The attack string



context: Where to apply the payload (e.g., URL parameter, user input)



type: Attack type (e.g., tautology, reflected)



severity: Impact level (low, medium, high, critical)



example_query or example_usage: Example of payload application



Severity Distribution:





Critical: ~20% (e.g., stacked-queries, reverse shells)



High: ~60% (e.g., tautology, union, reflected XSS)



Medium: ~15% (e.g., blind-time, boolean-blind)



Low: ~5% (e.g., certain SSRF payloads)

Use Cases





Penetration Testing: Test web applications for vulnerabilities using real-world payloads.



Security Tool Development: Build automated scanners or fuzzers for SQLi, XSS, SSRF, and CMDi detection.



Machine Learning: Train models for vulnerability classification, WAF bypass detection, or anomaly detection.



Education: Learn about web application vulnerabilities and attack techniques.



WAF Testing: Evaluate Web Application Firewalls against encoded and obfuscated payloads.

Sample Payloads







ID



Type



Payload



Context



Severity





sqli-001



Tautology



' OR '1'='1



Login username



High





xss-001



Reflected XSS



<script>alert('XSS1')</script>



URL parameter



High





ssrf-001



SSRF



http://127.0.0.1/



URL parameter



High





cmdinj-001



Command Injection



; ls -la



User input



High

Usage Instructions





Download: Clone the repository or download WEB_APPLICATION_PAYLOADS.jsonl.



Parse: Use a JSON Lines parser (e.g., Python’s json module) to read the dataset.

import json
with open('WEB_APPLICATION_PAYLOADS.jsonl', 'r') as f:
    payloads = [json.loads(line) for line in f]



Test: Apply payloads to target applications in a controlled environment with explicit permission.



Analyze: Check responses for vulnerability indicators (e.g., SQL errors, reflected scripts).



⚠️ Ethical Use: Only use this dataset on systems you have explicit permission to test. Unauthorized testing is illegal and unethical.

Example Testing Script

Below is a Python script to test SQLi and XSS payloads against a target URL:

import requests
import json
from urllib.parse import urlencode

def test_payload(url, param, payload, attack_type):
    test_url = f"{url}?{param}={urlencode({'': payload})}"
    response = requests.get(test_url, timeout=5)
    if attack_type == "sqli" and any(err in response.text.lower() for err in ["sql syntax", "mysql_fetch"]):
        return True, f"SQLi detected: {payload}"
    if attack_type == "xss" and payload in response.text:
        return True, f"XSS detected: {payload}"
    return False, ""

with open('WEB_APPLICATION_PAYLOADS.jsonl', 'r') as f:
    for line in f:
        entry = json.loads(line.strip())
        success, message = test_payload("http://example.com/search", "q", entry['payload'], entry['type'].lower())
        print(f"[{entry['id']}] {message if success else 'No vulnerability'}")

Contributing

Contributions are welcome! To contribute:





Fork the repository.



Add new payloads or improve documentation.



Submit a pull request with a clear description of changes.

Please ensure payloads are unique, well-documented, and follow the existing JSON structure.

License

This dataset is licensed under the MIT License. You are free to use, modify, and distribute it, provided you adhere to ethical and legal guidelines.

Citation

If you use this dataset in your research or projects, please cite:

Web Application Payloads Dataset (2025). Available at [Hugging Face/Kaggle/GitHub ].

Contact

For questions or suggestions, open an issue on GitHub or contact sunny48445@gmail.com.



Built for security researchers by security researchers. Stay safe, test responsibly!
