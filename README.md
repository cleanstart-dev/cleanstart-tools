# cleanstart-tools
This repository is to hold tools built by CleanStart.


### Currently Available tools
# Clnstrt-SBOM Tool
 Clnstrt-SBOM tool is meant to generate Software Bill of Materials (SBOM) for container images. 
 
 Key features: 
 * Generate SBOM of any CleanStart image
 * Generate SBOM of any another maintainer's image
 * Compare SBOM of multiple images
 * Curate package list of any CleanStart image
 * Curate package list of any another maintainer's image
 * Generate SBOM in SPDX and CYCLONEDX format


## Resources
- CleanStart Ogranization URL: https://www.cleanstart.com/ 


## Contact us
_Report any issue or feature request to: community-admin@cleanstart.com_


## About CleanStart Security
CleanStart is dedicated to reshaping the landscape of software supply chain security. With seamless integration, combined with continuous monitoring and vulnerability intelligence, CleanStart provides a platform that secures every step from development to delivery.
Our main goal is to make security easy for users while taking on the hard work of finding and fixing security issues. 
Here's how we do it:
Developer Harmony: We try to make security fit seamlessly into developers' work so they can keep moving fast without sacrificing safety.
Security Empowerment: With our tools, security teams can set up strong security rules and make sure they're followed, keeping the whole supply chain safe.
We are committed to enabling faster detection and response to threats, increasing trust, and empowering organizations to develop software with confidence by minimizing developer disruption and empowering security teams.

---

## SBOM Structure Overview

The generated SBOM contains three main sections:

### 1. Document Information
- SPDX version and data license
- Image digest and build ID
- Creation timestamp and tool information

### 2. Package Information
For each package, you'll find:
- **Basic info**: Package name, version, license, description
- **Source details**: Homepage URL, source repository, commit ID
- **Build info**: Build date, maintainer, architecture
- **File details**: File count, package size, installed size
- **Dependencies**: What other packages it depends on
- **Security**: Checksums for integrity verification


---

## Key Features

✅ **Multiple Formats**: Supports both SPDX and CycloneDX standards  
✅ **Complete Metadata**: Package versions, licenses, dependencies, and more  
✅ **Security Info**: Checksums and package integrity data  
✅ **Build Information**: Build dates, maintainers, and package origins  

---

## Quick Reference

| Command | Purpose |
|---------|---------|
| `clnstrt-tool sbom <image>` | Generate SPDX SBOM |
| `clnstrt-tool sbom --format cyclonedx <image>` | Generate CycloneDX SBOM |
| `clnstrt-tool sbom --format both <image>` | Generate both formats |
| `clnstrt-tool sbom --pull <image>` | Pull image first, then generate SBOM |
| `clnstrt-tool sbom --output <file> <image>` | Custom output filename |
| `clnstrt-tool pkg <image>` | List packages only |
| `clnstrt-tool pkg --output <file> <image>` | Save package list to file |

---

## Next Steps

Once you have your SBOM file:
1. Review the packages and their licenses
2. Check for security vulnerabilities using the package information
3. Verify source repositories and commit IDs
4. Use the SBOM for compliance and security auditing
