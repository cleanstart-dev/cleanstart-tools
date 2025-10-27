## clnstrt-SBOM Tool

Clnstrt-SBOM tool is meant to generate Software Bill of Materials (SBOM) for container images. 


## What is the clnstrt-SBOM Generation Tool?

Our SBOM (Software Bill of Materials) Generation Tool is a comprehensive container scanning solution that creates detailed software inventories for Docker images. The tool analyzes container images to identify all software components, libraries, and dependencies, producing standardized SBOM documents that help organizations understand their software.


## Importance of SBOM

SBOMs are now a compliance baseline. Incomplete SBOMs create blind spots and operational
risks. CleanStart SBOM delivers compliance-ready, complete, and actionable intelligence at scale,
giving security leaders the confidence to meet regulatory requirements and strengthen supply
chain resilience.


## Key features: 

* Generate SBOM of any CleanStart image
* Generate SBOM of any another maintainer's image
* Compare SBOM of multiple images
* Curate package list of any CleanStart image
* Curate package list of any another maintainer's image
* Generate SBOM in SPDX and CYCLONEDX format


## clnstrt - SBOM - Whitepaper 
https://www.cleanstart.com/resources/software-bill-of-materials

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
