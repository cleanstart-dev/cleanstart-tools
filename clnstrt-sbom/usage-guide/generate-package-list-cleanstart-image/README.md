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
📦 Package List for Docker Image: cleanstart/nginx:latest
================================================================================
Generated: 2025-10-16 12:58:27 UTC
Total Packages: 26

Package Name                             Version              License             
--------------------------------------------------------------------------------
busybox                                  1.37.0-r30           GPL-2.0-only        
busybox-binsh                            1.37.0-r30           GPL-2.0-only        
busybox-ifupdown                         1.37.0-r30           GPL-2.0-only        
busybox-mdev-openrc                      1.37.0-r30           GPL-2.0-only        
busybox-openrc                           1.37.0-r30           GPL-2.0-only        
busybox-suid                             1.37.0-r30           GPL-2.0-only        
clnstrt-baselayout                       3.6.5-r0             GPL-2.0-only        
clnstrt-baselayout-data                  3.6.5-r0             GPL-2.0-only        
clnstrt-conf                             3.18.1-r0            MIT                 
clnstrt-release                          3.20.3-r0            MIT                 
glibc-clnstrt                            2.41-r0              GNU LGPL            
libcap2                                  2.70-r1              BSD-3-Clause OR GPL 
libcrypto3                               3.5.2-r0             Apache-2.0          
libgcc                                   15.1.0_git20250607-  GPL-2.0-or-later AN 
libssl3                                  3.5.2-r0             Apache-2.0          
libxcrypt                                4.4.36-r0            LGPL-2.1 license    
mdev-conf                                4.7-r0               MIT                 
nginx                                    1.29.0-r0            BSD-2-Clause        
nginx-openrc                             1.29.0-r0            BSD-2-Clause        
openrc                                   0.54-r1              BSD-2-Clause        
openssl                                  3.5.2-r0             Apache-2.0          
pcre                                     8.45-r3              BSD-3-Clause        
scanelf                                  1.3.8-r2             GPL-2.0-only        
skalibs-libs                             2.14.3.0-r0          ISC                 
ssl_client                               1.37.0-r30           GPL-2.0-only        
zlib                                     1.3.1-r3             Zlib                

📊 Package manager distribution:
  apk: 26 packages
```