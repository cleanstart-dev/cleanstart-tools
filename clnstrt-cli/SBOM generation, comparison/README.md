## SBOM (Software Bill of Materials)

Generates an SBOM and also generate clnstrt diff(v1/v2) and clnstrt sbomdiff(sbom1/sbom2) using the Clnstrt CLI tool and are used to compare container images and their respective Software Bills of Materials (SBOMs). These commands help you identify differences in the images, such as layer structure, installed packages, and vulnerabilities, allowing for better image management, security auditing, and compliance checks.

### Generate SBOM

```bash
# Generate SBOM (default output to console)
clnstrt sbom python-test:latest -v
# Outout will be similar to this:
# Generating SBOM for image: python-test:latest
# Running syft command: syft packages python-test:latest -o cyclonedx-json --file sbom_python-test:latest.json -v
# Successfully generated SBOM at: sbom_python-test:latest.json using format: cyclonedx-json
# refer output at /SBOM generation, comparison/sbom_python-test-latest.json

# Save SBOM to JSON file
clnstrt sbom --output sbom.json python-test:latest -v
# Outout will be similar to this:
# Generating SBOM for image: python-test:latest
# Running syft command: syft packages python-test:latest -o cyclonedx-json --file sbom.json -v
# Successfully generated SBOM at: sbom.json using format: cyclonedx-json
# refer output at /SBOM generation, comparison/sbom.json

# Generate with specific format and save
clnstrt sbom --format spdx --output spdx-sbom.json python-test:latest -v
# Outout will be similar to this:
# Generating SBOM for image: python-test:latest
# Running syft command: syft packages python-test:latest -o spdx-json --file spdx-sbom.json -v
# Successfully generated SBOM at: spdx-sbom.json using format: spdx-json
# refer output at /SBOM generation, comparison/spdx-sbom.json

# Generate CycloneDX format SBOM
clnstrt sbom --format cyclonedx --output cyclonedx-sbom.json python-test:latest -v
# Outout will be similar to this:
# Generating SBOM for image: python-test:latest
# Running syft command: syft packages python-test:latest -o cyclonedx-json --file cyclonedx-sbom.json -v
# Successfully generated SBOM at: cyclonedx-sbom.json using format: cyclonedx
# refer output at /SBOM generation, comparison/cyclonedx-sbom.json

# With config file and output
clnstrt sbom -c sbom-config.yaml --output configured-sbom.json python-test:latest -v
# sbom-config.yaml used python-test.yaml
# Outout will be similar to this:
# Generating SBOM for image: python-test:latest
# Running syft command: syft packages python-test:latest -o cyclonedx-json --file configured-sbom.json -v
# Successfully generated SBOM at: configured-sbom.json using format: cyclonedx-json
# refer output at /SBOM generation, comparison/configured-sbom.json
```

- Purpose: Generates an SBOM for the specified image in different formats. 
- How It Works: The clnstrt sbom command analyzes the image, extracts package and dependency information, and saves it in the specified file format (default, CycloneDX, or SPDX). 
- Outcome: SBOMs are generated and saved as sbom.json, cyclonedx-sbom.json, and spdx-sbom.json.

### Output Files Generated:

- `sbom.json` - Standard SBOM in JSON format
- `spdx-sbom.json` - SPDX format SBOM
- `cyclonedx-sbom.json` - CycloneDX format SBOM

### sbomdiff - Compare SBOMs Between Images

Compares two images SBOM to show added, removed, and changed components.

```bash
# Compare SBOMs (output to console)
clnstrt sbomdiff python-test:latest python:latest -v
# Outout will be similar to this:
# Comparing SBOMs for images:
#   1: python-test:latest
#   2: python:latest
# Generating SBOM for image: python-test:latest
# Running: syft python-test:latest --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom1_1761810935557154813.json
# Generating SBOM for image: python:latest
# Running: syft python:latest --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom2_1761810935557161065.json
# SBOM comparison written to: sbom_diff_20251030_075535.csv
# refer output at /SBOM generation, comparison/sbom_diff_20251030_075535.csv

# Save comparison to JSON file
clnstrt sbomdiff --output sbom-diff.json python-test:latest python:latest -v
# Outout will be similar to this:
# Comparing SBOMs for images:
#   1: python-test:latest
#   2: python:latest
# Generating SBOM for image: python-test:latest
# Running: syft python-test:latest --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom1_1761811359078755427.json
# Generating SBOM for image: python:latest
# Running: syft python:latest --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom2_1761811359078762565.json
# SBOM comparison written to: sbom-diff.json
# refer output at /SBOM generation, comparison/sbom-diff.json

# Compare same image (should show no differences)
clnstrt sbomdiff --output no-diff.json python-test:latest python-test:latest -v
# Outout will be similar to this:
# Comparing SBOMs for images:
#   1: python-test:latest
#   2: python-test:latest
# Generating SBOM for image: python-test:latest
# Running: syft python-test:latest --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom1_1761811919651643705.json
# Generating SBOM for image: python-test:latest
# Running: syft python-test:latest --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom2_1761811919651651178.json
# SBOM comparison written to: no-diff.json
# refer output at /SBOM generation, comparison/no-diff.json

```

### Output Files Generated:

- `sbom-diff.json` - Differences in JSON format
- `no-diff.json` - Empty diff file (same images)


### sbomdiff json files - Compare Local SBOM Files

Compares two local SBOM files and exports differences in multiple formats.

```bash
# Compare two SBOM files (output to console)
clnstrt sbomdifffiles sbom1.json sbom2.json
# sbom1.json consist of python-test:latest sbom
# sbom2.json consist of python:latest sbom
# Outout will be similar to this:
# Comparing SBOM files:
#   1: sbom1.json
#   2: sbom2.json

# Comparison Summary:
#   Added Packages: 21878
#   Removed Packages: 3329
#   Modified Packages: 4
#   Total Changes: 25211
# SBOM comparison written to: sbom_diff_20251030_085543.csv
# refer output at /SBOM generation, comparison/sbom_diff_20251030_085543.csv
```
### Output Files Generated:

- `sbom_diff_20251030_085543.csv` - File comparison in CSV format


### SBOM Analysis Workflow

```bash
# 1. Generate SBOM for comparison baseline
clnstrt sbom --output baseline-sbom.json my-app:v1.0 -v
# Build my-app:v1.0 using this command
# Please find python-test-v1.yaml under SBOM generation, comparison folder
# clnstrt build python-test-v1.yaml my-app:v1.0 -v
# Outout will be similar to this:
# Generating SBOM for image: my-app:v1.0
# Running syft command: syft packages my-app:v1.0 -o cyclonedx-json --file baseline-sbom.json -v
# Successfully generated SBOM at: baseline-sbom.json using format: cyclonedx-json
# refer output at /SBOM generation, comparison/baseline-sbom.json

# 2. Generate SBOM for new version
clnstrt sbom --output current-sbom.json my-app:v2.0 -v
# Build my-app:v2.0 using this command
# Please find python-test-v2.yaml under SBOM generation, comparison folder
# clnstrt build python-test-v2.yaml my-app:v1.0 -v
# Outout will be similar to this:
# Generating SBOM for image: my-app:v2.0
# Running syft command: syft packages my-app:v2.0 -o cyclonedx-json --file current-sbom.json -v
# Successfully generated SBOM at: current-sbom.json using format: cyclonedx-json
# refer output at /SBOM generation, comparison/current-sbom.json

# 3. Compare versions and save differences
clnstrt sbomdiff --output version-diff.json my-app:v1.0 my-app:v2.0 -v
# Outout will be similar to this:
# Comparing SBOMs for images:
#   1: my-app:v1.0
#   2: my-app:v2.0
# Generating SBOM for image: my-app:v1.0
# Running: syft my-app:v1.0 --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom1_1761817346910504263.json
# Generating SBOM for image: my-app:v2.0
# Running: syft my-app:v2.0 --scope all-layers -o json
# SBOM generated successfully: /tmp/sbom2_1761817346910510955.json
# SBOM comparison written to: version-diff.json
# refer output at /SBOM generation, comparison/version-diff.json

# 4. Compare local SBOM files
clnstrt sbomdifffiles --output file-comparison.json baseline-sbom.json current-sbom.json -v
# Outout will be similar to this:
# Comparing SBOM files:
#   1: baseline-sbom.json
#   2: current-sbom.json

# Comparison Summary:
#   Added Packages: 62
#   Removed Packages: 0
#   Modified Packages: 0
#   Total Changes: 62
# SBOM comparison written to: file-comparison.json
# refer output at /SBOM generation, comparison/file-comparison.json
```

### Output Files Generated:

- `baseline-sbom.json` - sbom for v1
- `current-sbom.json` - sbom for v2
- `version-diff.json` - difference between v1, v2 packages
- `file-comparison.json` - packages comparison between v1, v2

- Purpose: These commands facilitate the comparison of container images and their Software Bill of Materials (SBOM) to identify differences in layers, packages, configurations, and software components across two images.
- How It Works: The clnstrt diff command compares two container images, highlighting differences in their layers, packages, and configurations, with the option to output the comparison in a CSV format. This can be done for both local and remote images. The clnstrt sbomdiff command compares the SBOMs of two container images, displaying differences in the software components included, with support for different SBOM formats like CycloneDX or SPDX. It outputs the results in CSV format as well. 
- Outcome: These commands enable users to efficiently identify and track changes between container images or their SBOMs, helping with version control, security audits, and compliance monitoring. They ensure that users can compare images in terms of both their content and underlying software composition across different versions or architectures.