## Prerequisites
Successful installation of clnstrt-sbom tool.
Successful image pull before generating sbom

## Generate SBOM

### Generate SBOM (Default - SPDX format)
```bash
clnstrt-tool sbom cleanstart/nginx:latest
```
This command will generate SPDX format sbom and display in terminal.

```bash
clnstrt-tool sbom --output < filename > cleanstart/nginx:latest
```
This command will generate SPDX format sbom and save it in json format in the given filename.


## Generate CycloneDX format
```bash
clnstrt-tool sbom --format cyclonedx cleanstart/nginx:latest
```
This command will generate CYCLONEDX format sbom and display in terminal.

```bash
clnstrt-tool sbom --format cyclonedx --output < filename > cleanstart/nginx:latest
```
This command will generate CYCLONEDX format sbom and save it in json format in the given filename.


## Generate both SPDX and CycloneDX formats
```bash
clnstrt-tool sbom --format both cleanstart/nginx:latest
```
This command will generate both SPDX and CYCLONEDX format sbom and display in terminal.

```bash
clnstrt-tool sbom --format both --output < filename > cleanstart/nginx:latest
```
This command will generate SPDX and CYCLONEDX format sbom and save them in json format in seperate files.


## Pull image and generate SBOM
```bash
clnstrt-tool sbom --pull cleanstart/nginx:latest
```
This command will pull the image, generate SPDX format sbom and save it in json format

```bash
clnstrt-tool sbom --output < filename > cleanstart/nginx:latest
```
This command will pull the image, generate SPDX format sbom and save it in json format in the given filename.


## Sample generated SBOM Output

```
2025/10/16 12:54:36 📄 Config file loaded: /home/user/.clnstrt.yaml
2025/10/16 12:54:36 🔑 Using API key from auth storage (overriding config file)
2025/10/16 12:54:36 🔑 Using API key: clnstrt_3f03070846b0****
2025/10/16 12:54:36 📦 Generating SBOM for: cleanstart/nginx:latest
2025/10/16 12:54:36 📥 Pulling image: cleanstart/nginx:latest
2025/10/16 12:54:40 ✅ Successfully pulled via API: cleanstart/nginx:latest
2025/10/16 12:56:06 ⚠️ API enrichment failed, falling back to Database: API connection test failed: API test failed: Invalid or inactive API key
2025/10/16 12:56:06 🏷️ Detected clnstrt-os from scanner info: clnstrt
2025/10/16 12:56:06 ✅ SPDX SBOM saved to: sbom_comparison_20251016_125435/cleanstart_nginx_latest/cleanstart/cleanstart_nginx_latest_spdx_sbom.json
2025/10/16 12:56:06 📊 Component Summary:
2025/10/16 12:56:06    🗝️ Image SHA256: sha256:8a71058998f50f0c8d26441b83da1e8eec2323ac12b57ea82c157d8fa0bd8da1
2025/10/16 12:56:06    📋 Package Manager Distribution:
2025/10/16 12:56:06       apk: 26 packages
2025/10/16 12:56:06 🎉 SBOM generation complete!
2025/10/16 12:56:06 📄 Config file loaded: /home/user/.clnstrt.yaml
2025/10/16 12:56:06 🔑 Using API key from auth storage (overriding config file)
2025/10/16 12:56:06 🔑 Using API key: clnstrt_3f03070846b0****
2025/10/16 12:56:06 📦 Generating SBOM for: cleanstart/nginx:latest
2025/10/16 12:57:13 ⚠️ API enrichment failed, falling back to Database: API connection test failed: API test failed: Invalid or inactive API key
2025/10/16 12:57:13 🏷️ Detected clnstrt-os from scanner info: clnstrt
2025/10/16 12:57:13 ✅ CycloneDX SBOM saved to: sbom_comparison_20251016_125435/cleanstart_nginx_latest/cleanstart/cleanstart_nginx_latest_cyclonedx_sbom.json
2025/10/16 12:57:13    License information found for 26 packages
2025/10/16 12:57:13 📊 SBOM generation complete!
2025/10/16 12:57:13    Total packages found: 26
2025/10/16 12:57:13    Package manager distribution:
2025/10/16 12:57:13      apk: 26 packages
2025/10/16 12:57:13    License Analysis:
2025/10/16 12:57:13      Packages with license information: 26
2025/10/16 12:57:13      Packages without license info: 0
2025/10/16 12:57:13 📄 Config file loaded: /home/user/.clnstrt.yaml
2025/10/16 12:57:13 🔑 Using API key from auth storage (overriding config file)
2025/10/16 12:57:13 🔑 Using API key: clnstrt_3f03070846b0****
2025/10/16 12:58:27 ✅ Package list saved to: sbom_comparison_20251016_125435/cleanstart_nginx_latest/cleanstart/cleanstart_nginx_latest_packages.txt
2025/10/16 12:58:27 📊 Total packages found: 26
2025/10/16 12:58:27 📦 Package manager distribution:
2025/10/16 12:58:27    apk: 26 packages
2025/10/16 12:58:27 ✅ Package list saved to: sbom_comparison_20251016_125435/cleanstart_nginx_latest/cleanstart/cleanstart_nginx_latest_packages.txt
```