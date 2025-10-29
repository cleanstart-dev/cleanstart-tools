## Clnstrt CLI Tool Usage Guide

## Introduction:
Clnstrt is a powerful tool for building minimal, secure container images. It focuses on creating optimized and secure-by-default containers, making it ideal for modern application development. The tool provides a comprehensive set of commands to analyze, build, manage, and validate container images while emphasizing security and efficiency.

The YAML configuration file is central to building images and running commands in this process.

## Key Features:
- Build minimal Images: 
  - Build lightweight container images tailored to your application's requirements.
- Image Signing & Verification: 
  - Cosign compatibility for container signing.
  - Key-based verification with public/private key pairs.
  - Use minimal base images to reduce attack surface.
- Vulnerability Scanning:
  - Built-in Trivy integration for comprehensive vulnerability detection.
  - Severity filtering (CRITICAL, HIGH, MEDIUM, LOW).
  - Multiple output formats (JSON, plain text).
- Comprehensive Analysis:
  - Provides detailed insights into image structure, vulnerabilities, and Software Bill of Materials (SBOM).
- Easy Management:
  - Manage image layers, packages, and multi-image compositions with ease.


## Quick Start:

### Follow these steps to set up the clnstrt-cli tool.

Contact sales@cleanstart.com 

Pull the clnstrt-cli image using the following command.

```bash
docker pull < location will be shared on demand >clnstrt-tool/< clnstrt cli image name >

```
replace < clnstrt cli image name > =>> clnstrt-cli:latest

### Tag the image

```bash
docker tag < image name > clnstrt
```

### Clnstrt Cli Tool Setup

```bash
echo -e '#!/bin/bash\ndocker \
      run --rm -v $(pwd):/work \
      -v /var/run/docker.sock:/var/run/docker.sock \
      -w /work clnstrt-cli:24.6.25 "$@"' | \
      sudo tee /usr/local/bin/clnstrt > /dev/null && \
      sudo chmod +x /usr/local/bin/clnstrt
```

### Basic Usage

```bash
# Get help
clnstrt --help
# Check version
clnstrt --version
# Analyze an image
clnstrt analyze cleanstart/go:latest
# Scan for vulnerabilities
clnstrt scan cleanstart/go:latest
```

## how to use guide:

- Build and Push Image : Configure your project, build container images, and push them securely to your preferred container registry using the clnstrt-cli.

- Scan Your Custom Image : Perform vulnerability and misconfiguration scans on your custom-built container images to ensure they meet security standards.

- Sign and Verify : Digitally sign your container images and verify their authenticity to maintain trust and compliance across deployments.

- List Packages : List and inspect all software packages and dependencies included within your container image for better visibility.

- SBOM Generation & Comparison : Generate a detailed Software Bill of Materials (SBOM), compare multiple SBOMs, and analyze differences for security and license compliance.

- Reports for Image : Access comprehensive reports containing scan results, vulnerabilities, and compliance summaries for your container images.

- Compliance and Audit : Ensure your images adhere to organizational or regulatory compliance standards and maintain audit-ready documentation.

- Prod Deployment & Validation : Deploy verified images to production and validate their integrity, ensuring only secure and compliant builds reach your environments.




## Troubleshooting

### Common Issues:

- #### Authentication Errors

```bash
docker login
# Error: Unauthenticated request
# Solution: Configure registry authentication
```

- #### Missing Key Files

```bash
clnstrt sign -k private.key image:tag
clnstrt verify -k public.key image:tag
# Error: required flag "key" not set
# Solution: Provide key file for sign/verify operations
```

- #### Package Scanning Issues

```bash
Error: no packages found in image
# This is normal for minimal/distroless images
# Not an error - indicates clean, minimal image
```
