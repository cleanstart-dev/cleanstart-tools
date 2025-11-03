## Compliance, Security & Audit Commands

- This section covers how to generate compliance reports, perform security audits, and analyze image changes using the clnstrt-cli.

### Note:
We are using python-test:latest, python:latest images here.
- python-test:latest - custom image build using python-test.yaml configuration, in /build and push/README.md 
- python:latest - public image of python

### 1. Generate Compliance Report with Image
```bash
clnstrt report --format json python-test:latest -v
# refer output at /compliance and audit/e32c6d95-c163-4b1f-b6f9-b51a1288a4d4.json
```

- Generates a compliance report and an SBOM (Software Bill of Materials) for your production image.
- The compliance report (compliance-report.json) provides a summary of compliance checks.
- The SBOM (compliance-sbom.json) lists all components, including their licenses, ensuring open-source compliance.

### 2. Security Audit with Vulnerability Scan
```bash
clnstrt scan --severity HIGH,CRITICAL,MEDIUM,LOW --output security-scan.json python:latest -v
# Starting Trivy scan for image: python:latest with severity filter: [HIGH CRITICAL MEDIUM LOW]
# Vulnerability counts - Critical: 0, High: 82, Medium: 211, Low: 211 (Unknown: 0)

# Trivy Scan Results for python:latest
# Scan Time: 2025-10-31T13:52:13Z

# Vulnerability Summary:
#   Critical: 0
#   High:     82
#   Medium:   211
#   Low:      211
#   Total:    504

# Detailed results saved to: security-scan.json
```

- Performs a vulnerability scan to detect high and critical severity issues in your image and generates an SBOM enriched with vulnerability data.
- The security-scan.json file lists all identified vulnerabilities.
- The security-sbom.json includes detailed package vulnerability mapping for audit tracking.

### 3. Generate Human-Readable Audit Report
```bash
clnstrt report --format html --output audit-report.html python-test:latest -v
# Outout will be similar to this:
# Report generated successfully: c1b953e4-e790-40a2-98e9-44da134f25e3.html
# refer output at /compliance and audit/c1b953e4-e790-40a2-98e9-44da134f25e3.html
```

- Creates a human-readable HTML report summarizing compliance, vulnerabilities, and scan results — ideal for sharing with stakeholders or auditors.
