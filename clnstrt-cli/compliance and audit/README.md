## Compliance, Security & Audit Commands

- This section covers how to generate compliance reports, perform security audits, and analyze image changes using the clnstrt-cli.

### 1. Generate Compliance Report with SBOM
```bash
clnstrt report --format json --output compliance-report.json production-image:latest
# refer output at /build and push/build.json

clnstrt sbom --include-licenses --output compliance-sbom.json production-image:latest
```

- Generates a compliance report and an SBOM (Software Bill of Materials) for your production image.
- The compliance report (compliance-report.json) provides a summary of compliance checks.
- The SBOM (compliance-sbom.json) lists all components, including their licenses, ensuring open-source compliance.

### 2. Security Audit with Vulnerability Scan and SBOM
```bash
clnstrt scan --severity HIGH,CRITICAL --output security-scan.json production-image:latest
clnstrt sbom --include-vulns --output security-sbom.json production-image:latest
```

- Performs a vulnerability scan to detect high and critical severity issues in your image and generates an SBOM enriched with vulnerability data.
- The security-scan.json file lists all identified vulnerabilities.
- The security-sbom.json includes detailed package vulnerability mapping for audit tracking.

### 3. Generate Human-Readable Audit Report
```bash
clnstrt report --format html --output audit-report.html production-image:latest
```

- Creates a human-readable HTML report summarizing compliance, vulnerabilities, and scan results — ideal for sharing with stakeholders or auditors.

### 4. Compare Image Versions (SBOM Diff Analysis)
```bash
clnstrt sbomdiff --format txt --output changes-report.txt previous-version:latest production-image:latest
```

- Compares two image versions and highlights changes in dependencies, vulnerabilities, and licenses.
- The resulting changes-report.txt helps track what changed between builds and assess potential risk impact.


#### Outcome:

##### After running the above commands, you’ll have a complete set of artifacts:
- compliance-report.json – Compliance summary
- compliance-sbom.json – SBOM with license info
- security-scan.json – Vulnerability details
- security-sbom.json – SBOM with vulnerabilities
- audit-report.html – Human-readable report
- changes-report.txt – SBOM difference summary