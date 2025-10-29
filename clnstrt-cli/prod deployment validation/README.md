## Production Deployment & Validation

- This section help ensure that your production image is secure, verified, compliant, and well-documented before deployment.

### 1. Full Security Scan
```bash
clnstrt scan --severity HIGH,CRITICAL production-image:latest
```

- Performs a comprehensive vulnerability scan on the production image, detecting only high and critical severity issues.
- This ensures that only secure images are promoted to production environments.

### 2. Generate Compliance Report
```bash
clnstrt report --format pdf --dir ./compliance production-image:latest
```

- Generates a compliance report in PDF format and stores it in the ./compliance directory.
- The report includes license compliance, security posture, and verification status — useful for audits and internal reviews.

### 3. Verify Signatures
```bash
clnstrt verify -k production.pub production-image:latest
```

- Verifies the digital signature of the production image using the provided public key (production.pub).
- This step ensures image authenticity, integrity, and trustworthiness before deployment.

### 4. Generate Deployment SBOM
```bash
clnstrt sbom production-image:latest > deployment-sbom.json
```

- Creates a Software Bill of Materials (SBOM) for the deployed image, listing all included packages and dependencies.
- The generated deployment-sbom.json helps track open-source components and maintain visibility for ongoing security monitoring.

### Outcome:

#### After running these commands, you’ll have:

- Verified and vulnerability-free production image
- PDF compliance report for auditing
- Verified digital signature for authenticity
- SBOM for monitoring and inventory tracking