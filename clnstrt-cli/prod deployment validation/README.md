## Production Deployment & Validation

- This section help ensure that your production image is secure, verified, compliant, and well-documented before deployment.

### Note:
We are using python-test:latest, python:latest images here.
- python-test:latest - custom image build using python-test.yaml configuration, in /build and push/README.md 
- python:latest - public image of python

### 1. Full Security Scan
```bash
clnstrt scan --severity HIGH,CRITICAL,MEDIUM,LOW python:latest -v
# refer output at /prod deployment validation/severity.txt
```

- Performs a comprehensive vulnerability scan on the production image, detecting only high and critical severity issues.
- This ensures that only secure images are promoted to production environments.


### 2. Verify Signatures
```bash
 clnstrt verify -k public-key.pem python-test:latest -v
 # refer output at /list packages/verify.txt
```

- Verifies the digital signature of the production image using the provided public key (production.pub).
- This step ensures image authenticity, integrity, and trustworthiness before deployment.

### 3. Generate Deployment SBOM
```bash
clnstrt sbom python-test:latest -v
 # refer output at /list packages/sbom.json
```

- Creates a Software Bill of Materials (SBOM) for the deployed image, listing all included packages and dependencies.
- The generated deployment-sbom.json helps track open-source components and maintain visibility for ongoing security monitoring.

### Outcome:

#### After running these commands, you’ll have:

- Verified and vulnerability-free production image
- Verified digital signature for authenticity
- SBOM for monitoring and inventory tracking