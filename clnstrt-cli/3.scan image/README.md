## 🔍 Security & Scanning
### Vulnerability Scanning
- Clnstrt-CLI tool can scan images for known vulnerabilities and generate detailed reports.

```bash
# Basic scan
clnstrt scan image:tag
# Filter by severity
clnstrt scan --severity HIGH,CRITICAL image:tag
# Save results to file
clnstrt scan --output results.json image:tag
# Verbose scan
clnstrt scan image:tag -v
```

- Purpose: Scans the built image for known vulnerabilities. 
- How It Works: The clnstrt scan command checks the image against vulnerability databases and reports any issues found. The --output option saves the scan report to a file. 
- Outcome: A list of vulnerabilities, if any, is displayed or saved in scan-report.txt.