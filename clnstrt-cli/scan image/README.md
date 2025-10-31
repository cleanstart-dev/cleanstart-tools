## 🔍 Security & Scanning
### Vulnerability Scanning
- Clnstrt-CLI tool can scan images for known vulnerabilities and generate detailed reports.

```bash
# Basic scan
clnstrt scan python-test:latest -v
# refer output at /scan image/scan.txt

# Filter by severity
clnstrt scan --severity HIGH,CRITICAL,MEDIUM,LOW python:latest -v
# refer output at /scan image/severity.txt

# Save results to file
clnstrt scan --output results.json python-test:latest -v
# Outout will be similar to this:
# Starting Trivy scan for image: python-test:latest
# Vulnerability counts - Critical: 0, High: 0, Medium: 0, Low: 0 (Unknown: 0)
# Scan completed. Found 0 vulnerabilities

# Trivy Scan Results for python-test:latest
# Scan Time: 2025-10-29T12:14:25Z

# Vulnerability Summary:
#   Critical: 0
#   High:     0
#   Medium:   0
#   Low:      0
#   Total:    0

# Detailed results saved to: results.json
# refer output at /scan image/results.json
```

- Purpose: Scans the built image for known vulnerabilities. 
- How It Works: The clnstrt scan command checks the image against vulnerability databases and reports any issues found. The --output option saves the scan report to a file. 
- Outcome: A list of vulnerabilities, if any, is displayed or saved in scan-report.txt.