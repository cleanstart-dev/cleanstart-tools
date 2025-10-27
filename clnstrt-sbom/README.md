## Software Bill of Materials - SBOM

## What is SBOM?

An SBOM is a comprehensive inventory that lists all software components, libraries, and dependencies within an application or system. It functions like an ingredient list for software, documenting open-source and proprietary components, their versions, licenses, and relationships. SBOMs are typically formatted using industry standards like SPDX or CycloneDX for machine-readable documentation. They capture the complete software supply chain hierarchy, from top-level applications down to nested dependencies. Modern SBOMs include metadata about component origins, maintainers, and known vulnerabilities at the time of creation.

##  Importance of SBOM

SBOMs help organizations quickly find and fix security vulnerabilities by showing exactly which software components they're using. They ensure legal compliance by tracking all software licenses and meeting requirements for software transparency. When critical vulnerabilities are discovered, organization can instantly check if they're affected instead of scrambling to audit their systems. They reduce supply chain risks by revealing hidden dependencies before problems arise, preventing costly breaches and downtime. SBOMs save time and money by automating inventory tracking that would otherwise require manual documentation across complex software systems.


## clnstrt-SBOM Generation Tool

CleanStart SBOM Generation Tool is a comprehensive container scanning solution that creates detailed software inventories for Docker images. The tool analyzes container images to identify all software components, libraries, and dependencies, producing standardized SBOM documents that help organizations understand their software.


## Key features: 

* Generate SBOM of any CleanStart image
* Generate SBOM of any another maintainer's image
* Compare SBOM of multiple images
* Curate package list of any CleanStart image
* Curate package list of any another maintainer's image
* Generate SBOM in SPDX and CYCLONEDX format


## Conclusion

SBOMs are now a compliance baseline. Incomplete SBOMs create blind spots and operational
risks. CleanStart SBOM delivers compliance-ready, complete, and actionable intelligence at scale,
giving security leaders the confidence to meet regulatory requirements and strengthen supply
chain resilience.


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

