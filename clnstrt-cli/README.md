##Clnstrt CLI Tool Usage Guide

##Introduction:
Clnstrt is a powerful tool for building minimal, secure container images. It focuses on creating optimized and secure-by-default containers, making it ideal for modern application development. The tool provides a comprehensive set of commands to analyze, build, manage, and validate container images while emphasizing security and efficiency.
The YAML configuration file is central to building images and running commands in this process.

##Key Features:
##Minimal Images: Build lightweight container images tailored to your application's requirements.
##Security-First: Includes tools for scanning, signing, and verifying container images to ensure secure deployment.
##Comprehensive Analysis: Provides detailed insights into image structure, vulnerabilities, and Software Bill of Materials (SBOM).
##Easy Management: Manage image layers, packages, and multi-image compositions with ease.


## Troubleshooting

### Common Issues

#### Authentication Errors

```bash
# Error: Unauthenticated request
# Solution: Configure registry authentication
docker login
```

#### Missing Key Files

```bash
# Error: required flag "key" not set
# Solution: Provide key file for sign/verify operations
clnstrt sign -k private.key image:tag
clnstrt verify -k public.key image:tag
```

#### Package Scanning Issues

```bash
Error: no packages found in image
# This is normal for minimal/distroless images
# Not an error - indicates clean, minimal image
```

## Security Features

### Vulnerability Scanning

- Built-in Trivy integration for comprehensive vulnerability detection
- Severity filtering (CRITICAL, HIGH, MEDIUM, LOW)
- Multiple output formats (JSON, plain text)

### Image Signing & Verification

- Cosign compatibility for container signing
- Key-based verification with public/private key pairs
- Policy enforcement for trusted images
- Certificate chain validation

### Security Best Practices

- Always scan images before deployment
- Sign critical images for integrity verification
- Use minimal base images to reduce attack surface
- Regular vulnerability updates with latest scan databases
- Implement security policies in CI/CD pipelines


### Key Files Required

- `config.yaml` - Build configuration with from: field
- `private.key/public.key` - For signing and verification

## Best Practices

### Image Security

- Scan early and often - integrate scanning into build pipelines
- Use specific tags - avoid latest in production
- Minimal base images - prefer distroless or scratch when possible
- Regular updates - keep base images and dependencies current
- Sign critical images - implement signing for production deployments

### Configuration Management

- Version control configs - track configuration changes
- Environment-specific configs - separate dev/staging/prod configurations
- Validate before build - always validate configs before building
- Document dependencies - maintain clear dependency documentation

### Performance Optimization

- Use build cache - enable caching for faster builds
- Layer optimization - minimize layer count and size
- Multi-stage builds - separate build and runtime environments
- Regular cleanup - clear caches and unused images


how to use guide:

Quick start: how to quick start
Build and Push image: Configure, Build and Push image using clnstrt-cli
Scan you custom Image: Scan image
Sign and Verify: sign and verify images for compliance
Packages: list all the packages
SBOM generation & comparison: Generate SBOM, Compare and Analyze
Reports for Image: get Image reports
Compliance and Audit: 
Prod Deployment & Validation: 