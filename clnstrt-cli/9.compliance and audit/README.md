```bash
# Generate compliance report with SBOM
clnstrt report --format json --output compliance-report.json production-image:latest
clnstrt sbom --include-licenses --output compliance-sbom.json production-image:latest
# Security audit with vulnerability scan and SBOM
clnstrt scan --severity HIGH,CRITICAL --output security-scan.json production-image:latest
clnstrt sbom --include-vulns --output security-sbom.json production-image:latest
# Generate human-readable audit report
clnstrt report --format html --output audit-report.html production-image:latest
clnstrt sbomdiff --format txt --output changes-report.txt previous-version:latest production-image:latest
```