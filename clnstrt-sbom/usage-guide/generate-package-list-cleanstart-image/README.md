## Prerequisites
Successful installation of clnstrt-sbom tool.
Successful image pull before generating sbom

## List Packages

### Display packages in terminal
```bash
clnstrt-tool pkg cleanstart/nginx:latest
```
This command will list packages of the Image in terminal.

### Save package list to a file
```bash
clnstrt-tool pkg --output < filename > cleanstart/nginx:latest
```
This command will list the packages and save it in given filename in txt file format.



### Sample generated Package List Output
```
Package List for Docker Image: nginx:latest
================================================================================
Generated: 2025-08-19 12:06:15 UTC
Total Packages: 15

Package Name              Version        License
--------------------------------------------------------------------------------
alpine-baselayout         3.4.3-r2       GPL-2.0-only
alpine-keys               2.4-r1         MIT
busybox                   1.36.1-r15     GPL-2.0-only
ca-certificates-bundle    20240226-r0    MPL-2.0 AND MIT
libcrypto3                3.1.4-r5       Apache-2.0
```