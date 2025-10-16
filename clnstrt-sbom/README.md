## Clnstrt-SBOM Tool

Clnstrt-SBOM tool is meant to generate Software Bill of Materials (SBOM) for container images. 

Key features: 
* Generate SBOM of any CleanStart image
* Generate SBOM of any another maintainer's image
* Compare SBOM of multiple images
* Curate package list of any CleanStart image
* Curate package list of any another maintainer's image
* Generate SBOM in SPDX and CYCLONEDX format


--- 
## Quick start

## Step 1: Installation

Install the Clnstrt tool on your Linux system:

```bash
curl -sSfL https://get.clnstrt.dev | sudo sh -s -- -b /usr/local/bin
```

**What this does:** Downloads and installs the `clnstrt-tool` command-line utility to your system.

---

## Step 2: Get Your API Key

Generate an API key by running this command (replace with your information):

```bash
curl -X POST "https://clnstrt-gw-api-3pvssbsuxa-uc.a.run.app/api/v1/admin/api-keys" \
  -H "Content-Type: application/json" \
  -d '{"email": "user@org.com", "name": "User", "organization": "Org"}'
```

**What this does:** Creates an API key for authenticating with the Clnstrt service. You'll receive an API key in the response.

---

## Step 3: Configure Authentication

Set your API key in the tool:

```bash
clnstrt-tool auth set <your-api-key>
```

**What this does:** Saves your API key so the tool can access Clnstrt services for enriched SBOM data.

---


#### Usage of this tool
# List Packages
# Display packages in terminal
clnstrt-tool pkg alpine:latest

Package Listing
📦 Package List for Docker Image: alpine:latest
================================================================================
Generated: 2025-08-19 12:06:15 UTC
Total Packages: 15

Package Name                        Version              License                  
--------------------------------------------------------------------------------
alpine-baselayout                   3.4.3-r2             GPL-2.0-only            
alpine-keys                         2.4-r1               MIT                     
busybox                             1.36.1-r15           GPL-2.0-only            
ca-certificates-bundle              20240226-r0          MPL-2.0 AND MIT        
libcrypto3                          3.1.4-r5             Apache-2.0              

📊 Package manager distribution:
  apk: 15 packages

# Generate SPDX SBOM (default)
clnstrt-tool sbom alpine:latest

# Generate CycloneDX SBOM
clnstrt-tool sbom --format cyclonedx alpine:latest

# Generate both formats
clnstrt-tool sbom --format both alpine:latest

# Pull image before scanning
clnstrt-tool sbom --pull alpine:latest

# Specify output filename
clnstrt-tool sbom --output my-alpine-sbom alpine:latest


# SBOM Schema - Complete Field Guide

## Document Structure Overview of SBOM

```json
{
  "spdxVersion": "SPDX-3.0",
  "dataLicense": "CC0-1.0",
  "SPDXID": "SPDXRef-DOCUMENT",
  "name": "SBOM for nginx:latest",
  "image-digest": "sha256:07ccdb7838758e758a4d52a9761636c385125a327355c0c94a6acff9babff938",
  "documentNamespace": "nginx:latest@sha256:07ccdb7838758e758a4d52a9761636c385125a327355c0c94a6acff9babff938",
  "creationInfo": {
    "created": "2025-10-16T09:39:19Z",
    "creators": [
      "Tool: Clnstrt-Enhanced-SBOM-generator-2.0"
    ],
    "licenseListVersion": "3.20"
  },
  "packages": [
    {
      "SPDXID": "SPDXRef-Package-apt-8b5f53dd348d9f35",
      "name": "apt",
      "versionInfo": "3.0.3",
      "filesAnalyzed": false,
      "maintainer": "APT Development Team <deity@lists.debian.org>",
      "license": "GPL-2+",
      "copyrightText": "NOASSERTION",
      "description": "commandline package manager",
      "URL": "NOASSERTION",
      "sourceInfo": "Package info acquired from dpkg db: /var/lib/dpkg/status",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "dpkg",
          "referenceLocator": "apt@3.0.3"
        },
        {
          "referenceCategory": "OTHER",
          "referenceType": "architecture",
          "referenceLocator": "amd64"
        }
      ],
      "properties": [
        {
          "name": "package_file_name",
          "value": "apt_3.0.3.deb"
        },
        {
          "name": "dependencies",
          "value": "base-passwd, (>=, 3.6.1), |, adduser, sqv, (>=, 1.3.0), libapt-pkg7.0, (>="
        },
        {
          "name": "component_type",
          "value": "os_package"
        }
      ]
    },
```
---

## 1. ROOT DOCUMENT FIELDS

### Required Fields
| Field | Example | Purpose | Security Use |
|-------|---------|---------|--------------|
| `spdxVersion` | `"SPDX-3.0"` | Format version | Tool compatibility |
| `dataLicense` | `"CC0-1.0"` | SBOM license | Legal compliance |
| `SPDXID` | `"SPDXRef-DOCUMENT"` | Document ID | Reference linking |
| `name` | `"SBOM for alpine:latest"` | Description | Human identification |
| `documentNamespace` | `"alpine:latest@sha256:abc..."` | Unique identifier | Global uniqueness |

### Container-Specific Fields
| Field | Example | Purpose | Security Use |
|-------|---------|---------|--------------|
| `image-digest` | `"sha256:792537642a6cb..."` | Image hash | Container verification |
| `image-build-id` | `"projects/291220049517/..."` | Build reference | Supply chain tracking |

### Creation Metadata
```json
"creationInfo": {
  "created": "2025-09-26T05:02:44Z",
  "creators": ["Tool: Clnstrt-Enhanced-SBOM-generator-2.0"],
  "licenseListVersion": "3.20"
}
```

---

## 2. PACKAGE FIELDS (packages array)

### Core Identity
| Field | Example | Required | Purpose |
|-------|---------|----------|---------|
| `SPDXID` | `"SPDXRef-Package-bash-8b19150a"` | ✅ | Unique package ID |
| `name` | `"bash"` | ✅ | Package name |
| `versionInfo` | `"5.2.26-r0"` | ✅ | Version for CVE matching |

### Legal & Compliance
| Field | Example | Purpose | CVE/Security Use |
|-------|---------|---------|------------------|
| `license` | `"GPL-3.0-or-later"` | Legal compliance | License risk assessment |
| `copyrightText` | `"NOASSERTION"` | Copyright info | Legal analysis |
| `maintainer` | `"Natanael Copa <email@domain>"` | Contact info | Supply chain trust |

### Technical Details
| Field | Example | Purpose | Security Use |
|-------|---------|---------|--------------|
| `description` | `"The GNU Bourne Again shell"` | Documentation | Component identification |
| `URL` | `"https://www.gnu.org/software/bash/"` | Homepage | Source verification |
| `filesAnalyzed` | `true` | Scan depth | Analysis completeness |
| `sourceInfo` | `"Package info acquired from apk db"` | Data source | Quality assessment |
| `builtDate` | `"2024-11-02T01:52:49Z"` | Build timestamp | Age-based risk |

---

## 3. EXTERNAL REFERENCES (Critical for CVE Scanning)

### Package Manager References
```json
"externalRefs": [
  {
    "referenceCategory": "PACKAGE-MANAGER",
    "referenceType": "apk",
    "referenceLocator": "bash@5.2.26-r0"
  }
]
```

### Architecture References
```json
{
  "referenceCategory": "OTHER", 
  "referenceType": "architecture",
  "referenceLocator": "x86_64"
}
```

### Package URL (PURL) - For Go Libraries
```json
{
  "referenceCategory": "PACKAGE-MANAGER",
  "referenceType": "purl", 
  "referenceLocator": "pkg:golang/github.com/prometheus/client_golang@v1.22.0"
}
```

**CVE Scanning Use**: These references are used to query vulnerability databases
- APK packages → Alpine SecDB, NVD
- PURLs → OSV Database, Go Vulnerability DB

---

## 4. CHECKSUMS (Integrity Verification)

```json
"checksums": [
  {
    "checksumValue": "Q1Hz5Oim6TlXIyfPU6P3LwtD/5Ytc="
  }
]
```

**Security Use**: Verify package hasn't been tampered with

---

## 5. PROPERTIES (Extended Metadata)

### File & Size Information
| Property Name | Example Value | Purpose |
|---------------|---------------|---------|
| `file_count` | `"46"` | Package complexity |
| `package_file_name` | `"bash-5.2.26-r0.apk"` | Original filename |
| `package_size` | `"447257"` | Archive size (bytes) |
| `installed_size` | `"1282851"` | Disk usage (bytes) |

### Dependencies
| Property Name | Example Value | Security Use |
|---------------|---------------|--------------|
| `dependencies` | `"/bin/sh, glibc, so:libreadline.so.8"` | Impact analysis |
| `provides` | `"cmd:bash=5.2.26-r0"` | Reverse dependency mapping |

### Source Code Tracking
| Property Name | Example Value | Security Use |
|---------------|---------------|--------------|
| `source_1` | `"https://ftp.gnu.org/gnu/bash/bash-5.2.26.tar.gz"` | Source verification |
| `commit_id` | `"de114558a5d8fa15350b1b3d440712fab6bae817"` | Exact source tracking |
| `repository` | `"https://gitlab.alpinelinux.org/alpine/apk-tools"` | Supply chain verification |

### Component Classification
| Property Name | Example Value | Purpose |
|---------------|---------------|---------|
| `component_type` | `"os_package"` or `"go_library"` | Categorization |
| `origin_package` | `"busybox"` | Sub-package relationship |

### Go-Specific Properties
| Property Name | Example Value | CVE Use |
|---------------|---------------|---------|
| `purl` | `"pkg:golang/github.com/aws/aws-sdk-go-v2@v1.36.3"` | Vulnerability lookup |
| `hash` | `"h1:mJoei2CxPutQVxaATCzDUjcZEjVRdpsiiXi2o38yqWM="` | Go module verification |

---

## 6. RELATIONSHIPS (Dependency Mapping)

### Relationship Types
```json
{
  "spdxElementId": "SPDXRef-Package-parent",
  "relatedSpdxElement": "SPDXRef-Package-dependency", 
  "relationshipType": "DEPENDS_ON"
}
```

| Relationship Type | Meaning | Security Impact |
|------------------|---------|-----------------|
| `DESCRIBES` | Document describes image | Documentation |
| `CONTAINS` | Image contains package | Inventory |
| `DEPENDS_ON` | Package depends on another | *Critical for vulnerability impact analysis* |

