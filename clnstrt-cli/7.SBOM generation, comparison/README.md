## SBOM (Software Bill of Materials)

Generates an SBOM and also generate clnstrt diff(v1/v2) and clnstrt sbomdiff(sbom1/sbom2) using the Clnstrt CLI tool and are used to compare container images and their respective Software Bills of Materials (SBOMs). These commands help you identify differences in the images, such as layer structure, installed packages, and vulnerabilities, allowing for better image management, security auditing, and compliance checks.

### Generate SBOM

```bash
# Generate SBOM (default output to console)
clnstrt sbom image:tag
# Save SBOM to JSON file
clnstrt sbom --output sbom.json image:tag
# Generate with specific format and save
clnstrt sbom --format spdx-json --output my-sbom.json image:tag
# Generate CycloneDX format SBOM
clnstrt sbom --format cyclonedx --output cyclone-sbom.json image:tag
# With config file and output
clnstrt sbom -c sbom-config.yaml --output configured-sbom.json image:tag
# Include licenses in SBOM
clnstrt sbom --include-licenses --output sbom-with-licenses.json image:tag
# Include vulnerabilities in SBOM
clnstrt sbom --include-vulns --output sbom-with-vulns.json image:tag
```

- Purpose: Generates an SBOM for the specified image in different formats. 
- How It Works: The clnstrt sbom command analyzes the image, extracts package and dependency information, and saves it in the specified file format (default, CycloneDX, or SPDX). 
- Outcome: SBOMs are generated and saved as sbom.json, sbom-cyclonedx.json, and sbom-spdx.json.

### Output Files Generated:

- `sbom.json` - Standard SBOM in JSON format
- `my-sbom.json` - SPDX format SBOM
- `cyclone-sbom.json` - CycloneDX format SBOM
- `sbom-with-licenses.json` - SBOM including license information
- `sbom-with-vulns.json` - SBOM with vulnerability data

### sbomdiff - Compare SBOMs Between Images

Compares two images SBOM to show added, removed, and changed components.

```bash
# Compare SBOMs (output to console)
clnstrt sbomdiff image1:tag image2:tag
# Save comparison to JSON file
clnstrt sbomdiff --output sbom-diff.json image1:tag image2:tag
# Save comparison to CSV file
clnstrt sbomdiff --output sbom-diff.csv --format csv image1:tag image2:tag
# Save comparison to TXT file
clnstrt sbomdiff --output sbom-diff.txt --format txt image1:tag image2:tag
# Detailed comparison with output file
clnstrt sbomdiff --detailed --output detailed-diff.json image1:tag image2:tag
# Compare same image (should show no differences)
clnstrt sbomdiff --output no-diff.json image:tag image:tag
```

### Output Files Generated:

- `sbom-diff.json` - Differences in JSON format
- `sbom-diff.csv` - Differences in CSV format for spreadsheet analysis
- `sbom-diff.txt` - Human-readable text format differences
- `detailed-diff.json` - Detailed component-level differences
- `no-diff.json` - Empty diff file (same images)




### sbomdiff json files - Compare Local SBOM Files

Compares two local SBOM files and exports differences in multiple formats.

```bash
# Compare two SBOM files (output to console)
clnstrt sbomdifffiles sbom1.json sbom2.json
# Save file comparison to JSON
clnstrt sbomdifffiles --output file-diff.json sbom1.json sbom2.json
# Save file comparison to CSV
clnstrt sbomdifffiles --format csv --output file-diff.csv sbom1.json sbom2.json
# Save file comparison to TXT
clnstrt sbomdifffiles --format txt --output file-diff.txt sbom1.json sbom2.json
# Compare with table format output
clnstrt sbomdifffiles --format table --output table-diff.txt sbom1.json sbom2.json
# Detailed file comparison
clnstrt sbomdifffiles --detailed --output detailed-file-diff.json sbom1.json sbom2.json
```

### Output Files Generated:

- `file-diff.json` - File comparison in JSON format
- `file-diff.csv` - Spreadsheet-compatible CSV comparison
- `file-diff.txt` - Text format file differences
- `table-diff.txt` - Tabular format comparison
- `detailed-file-diff.json` - Comprehensive file analysis


### SBOM Analysis Workflow

```bash
# 1. Generate comprehensive SBOM with all data
clnstrt sbom --include-licenses --include-vulns --output complete-sbom.json my-app:latest
# 2. Generate SBOM for comparison baseline
clnstrt sbom --output baseline-sbom.json my-app:v1.0
# 3. Generate SBOM for new version
clnstrt sbom --output current-sbom.json my-app:v2.0
# 4. Compare versions and save differences
clnstrt sbomdiff --output version-diff.json my-app:v1.0 my-app:v2.0
# 5. Generate CSV for spreadsheet analysis
clnstrt sbomdiff --format csv --output version-diff.csv my-app:v1.0 my-app:v2.0
# 6. Compare local SBOM files
clnstrt sbomdifffiles --output file-comparison.json baseline-sbom.json complete-sbom.json
```

- Purpose: These commands facilitate the comparison of container images and their Software Bill of Materials (SBOM) to identify differences in layers, packages, configurations, and software components across two images.
- How It Works: The clnstrt diff command compares two container images, highlighting differences in their layers, packages, and configurations, with the option to output the comparison in a CSV format. This can be done for both local and remote images. The clnstrt sbomdiff command compares the SBOMs of two container images, displaying differences in the software components included, with support for different SBOM formats like CycloneDX or SPDX. It outputs the results in CSV format as well. 
- Outcome: These commands enable users to efficiently identify and track changes between container images or their SBOMs, helping with version control, security audits, and compliance monitoring. They ensure that users can compare images in terms of both their content and underlying software composition across different versions or architectures.