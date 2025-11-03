## Clnstrt CLI Tool Usage Guide

### Introduction to clnstrt-cli Tool:

Clnstrt is a powerful command-line tool designed for building minimal, secure container images in modern cloud-native environments. It focuses on creating optimized and secure-by-default containers, ideal for enterprise application development and deployment. The tool provides extensive commands to analyze, build, manage, and validate container images while emphasizing security and compliance. At the heart of clnstrt's workflow is the YAML configuration file, which serves as the central component for orchestrating various container operations and ensuring consistency across all environments.

### Importance:

In today's security-conscious development landscape, container image security and optimization are critical for successful application deployment. Clnstrt addresses supply chain security needs by providing integrated vulnerability scanning, image signing and comprehensive SBOM generation. The tool's ability to create minimal images reduces attack surface, improves performance and decreases storage costs. By consolidating multiple container security capabilities into a single unified tool, clnstrt significantly streamlines DevSecOps workflows and reduces operational complexity.

### Key Features:

- Build Minimal Images: Create lightweight, optimized container images with layer optimization, multi-stage builds, and configurable base images through the required from: field in configuration files
- Image Signing & Verification: Cosign-compatible container signing with key-based verification using public/private key pairs, policy enforcement for trusted images, and certificate chain validation for comprehensive security
- Vulnerability Scanning: Built-in Trivy integration for comprehensive vulnerability detection with severity filtering (CRITICAL, HIGH, MEDIUM, LOW), multiple output formats (JSON, plain text), and exit codes for CI/CD integration
- Comprehensive Analysis: Detailed layer inspection, metadata extraction, image comparison capabilities, and Software Bill of Materials (SBOM) generation in multiple formats (SPDX, CycloneDX) with license tracking and vulnerability inclusion
- Easy Management: Intuitive layer management, package tracking and export, Docker Compose integration for multi-service orchestration, and efficient cache management for faster builds.

### Conclusion:

Clnstrt-cli is a production-ready tool that addresses the complete lifecycle of secure container image management from build to deployment. By combining security scanning, signing, SBOM generation, and analysis into a unified platform, it streamlines workflows while maintaining enterprise-grade security. The configuration-driven approach ensures reproducibility, while extensive features provide flexibility for local development to enterprise CI/CD pipelines, making it essential for modern DevSecOps workflows.

### Quick Start:

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
      -w /work clnstrt-images.clnstrt.dev/clnstrt-cli-tool/clnstrt-cli:latest "$@"' | \
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
