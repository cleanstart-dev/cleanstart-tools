## Prerequisites
Successful installation of clnstrt-sbom tool.
Successful image pull before generating sbom

## Generate SBOM

### Generate SBOM (Default - SPDX format)
```bash
clnstrt-tool sbom nginx:latest
```
This command will generate SPDX format sbom and display in terminal.

```bash
clnstrt-tool sbom --output < filename > nginx:latest
```
This command will generate SPDX format sbom and save it in json format in the given filename.


## Generate CycloneDX format
```bash
clnstrt-tool sbom --format cyclonedx nginx:latest
```
This command will generate CYCLONEDX format sbom and display in terminal.

```bash
clnstrt-tool sbom --format cyclonedx --output < filename > nginx:latest
```
This command will generate CYCLONEDX format sbom and save it in json format in the given filename.


## Generate both SPDX and CycloneDX formats
```bash
clnstrt-tool sbom --format both nginx:latest
```
This command will generate both SPDX and CYCLONEDX format sbom and display in terminal.

```bash
clnstrt-tool sbom --format both --output < filename > nginx:latest
```
This command will generate SPDX and CYCLONEDX format sbom and save them in json format in seperate files.


## Pull image and generate SBOM
```bash
clnstrt-tool sbom --pull nginx:latest
```
This command will pull the image, generate SPDX format sbom and save it in json format

```bash
clnstrt-tool sbom --output < filename > nginx:latest
```
This command will pull the image, generate SPDX format sbom and save it in json format in the given filename.


## Sample generated SBOM Output

```
✓ Generating SBOM for: alpine:latest
  Fetching commit details from BigQuery for 15 packages...
  SPDX SBOM saved to: given filename
  
  Includes 8 package commit IDs from BigQuery
  Includes source links for 12 packages from BigQuery
  Image SHA256: sha256:abc123...
  
  SBOM generation complete!
  Total packages found: 15
  Package manager distribution: apk: 15 packages
  Source Links: Found for 12 out of 15 packages from BigQuery
  Commit IDs: Found for 8 out of 15 packages from BigQuery
```