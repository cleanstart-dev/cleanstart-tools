### Production Deployment

```bash
# Full security scan
clnstrt scan --severity HIGH,CRITICAL production-image:latest
# Generate compliance report
clnstrt report --format pdf --dir ./compliance production-image:latest
# Verify signatures
clnstrt verify -k production.pub production-image:latest
# Generate deployment SBOM
clnstrt sbom production-image:latest > deployment-sbom.json
```