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
2025/10/16 13:25:35 📄 Config file loaded: /home/user/.clnstrt.yaml
2025/10/16 13:25:35 🔑 Using API key from auth storage (overriding config file)
2025/10/16 13:25:35 🔑 Using API key: clnstrt_5ad49a9ed7d5****
2025/10/16 13:25:35 📦 Generating SBOM for: nginx:latest
2025/10/16 13:25:35 📥 Pulling image: nginx:latest
2025/10/16 13:25:38 ✅ Successfully pulled via API: nginx:latest
2025/10/16 13:30:06 ✅ SPDX SBOM saved to: sbom_comparison_20251016_132535/nginx_latest/cleanstart/nginx_latest_spdx_sbom.json
2025/10/16 13:30:06 📊 Component Summary:
2025/10/16 13:30:06    🗝️ Image SHA256: sha256:07ccdb7838758e758a4d52a9761636c385125a327355c0c94a6acff9babff938
2025/10/16 13:30:06    📋 Package Manager Distribution:
2025/10/16 13:30:06       dpkg: 150 packages
2025/10/16 13:30:06 🎉 SBOM generation complete!
2025/10/16 13:30:06 📄 Config file loaded: /home/user/.clnstrt.yaml
2025/10/16 13:30:06 🔑 Using API key from auth storage (overriding config file)
2025/10/16 13:30:06 🔑 Using API key: clnstrt_5ad49a9ed7d5****
2025/10/16 13:30:06 📦 Generating SBOM for: nginx:latest
2025/10/16 13:34:37 ✅ CycloneDX SBOM saved to: sbom_comparison_20251016_132535/nginx_latest/cleanstart/nginx_latest_cyclonedx_sbom.json
2025/10/16 13:34:37    Includes source links for 17 packages from Database
2025/10/16 13:34:37    License information found for 150 packages
2025/10/16 13:34:37 📊 SBOM generation complete!
2025/10/16 13:34:37    Total packages found: 150
2025/10/16 13:34:37    Package manager distribution:
2025/10/16 13:34:37      dpkg: 150 packages
2025/10/16 13:34:37    License Analysis:
2025/10/16 13:34:37      Packages with license information: 150
2025/10/16 13:34:37      Packages without license info: 0
2025/10/16 13:34:37    Source Links: Found for 17 out of 150 packages from Database
2025/10/16 13:34:37 📄 Config file loaded: /home/user/.clnstrt.yaml
2025/10/16 13:34:37 🔑 Using API key from auth storage (overriding config file)
2025/10/16 13:34:37 🔑 Using API key: clnstrt_5ad49a9ed7d5****
2025/10/16 13:34:47 ✅ Package list saved to: sbom_comparison_20251016_132535/nginx_latest/cleanstart/nginx_latest_packages.txt
2025/10/16 13:34:47 📊 Total packages found: 150
2025/10/16 13:34:47 📦 Package manager distribution:
2025/10/16 13:34:47    dpkg: 150 packages
2025/10/16 13:34:47 ✅ Package list saved to: sbom_comparison_20251016_132535/nginx_latest/cleanstart/nginx_latest_packages.txt
```