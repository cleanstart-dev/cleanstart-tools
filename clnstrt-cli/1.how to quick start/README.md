### follow these steps to set up the clnstrt-cli tool.

Contact sales@cleanstart.com 

Pull the clnstrt-cli image using the following command.

```bash
docker pull < location will be shared on demand >clnstrt-tool/< clnstrt cli image name >

```
- replace < clnstrt cli image name > =>> clnstrt-cli:latest

###Tag the image

```bash
docker tag < image name > clnstrt
```

Set user/bin

```bash
echo -e '#!/bin/bash\ndocker \
      run --rm -v $(pwd):/work \
      -v /var/run/docker.sock:/var/run/docker.sock \
      -w /work clnstrt-cli:24.6.25 "$@"' | \
      sudo tee /usr/local/bin/clnstrt > /dev/null && \
      sudo chmod +x /usr/local/bin/clnstrt
```

### Basic Usage

```bash
# Get help
clnstrt --help
# Check version
clnstrt --version
# Analyze an image
clnstrt analyze cleanstart/go:latest
# Scan for vulnerabilities
clnstrt scan cleanstart/go:latest
```

