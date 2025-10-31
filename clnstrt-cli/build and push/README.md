Create python-test.yaml using "nano python-test.yaml" and paste below config file.

### Build a Minimal Docker Image

```yaml
from: alpine:latest
packages:
      - ca-certificates
      - curl
      - python3
      - py3-pip
env:
    PATH: "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    PYTHONUNBUFFERED: "1"
    APP_ENV: "production"
workdir: /app
user: nobody
cmd:
     - "python3"
     - "-c"
     - "print('Hello from Python Alpine!')"
labels:
        org.opencontainers.image.source: "clnstrt"
        org.opencontainers.image.version: "1.0.0"
        org.opencontainers.image.description: "Python application with SBOM"
```



#### Purpose of the YAML Configuration:

- Base Image: Specifies the base image (alpine:latest) from which the build will start.
- Packages: Lists additional packages to be installed in the container (e.g., curl, python3).
- Environment Variables: Defines the environment variables for the container.
- Work Directory: Sets the working directory for executing commands (/app).
- User: Specifies the user under which commands will run (nobody).
- Command: Default command to execute when the container runs.
- Labels: Metadata labels for the image.

### Build Container Images

Builds a new container image from a declarative config with options for caching and squashing.

```bash
# Basic build
clnstrt build python-test.yaml python-test:latest -v
# refer output at /build and push/build.json

# Build with squashed layers
clnstrt build --squash python-test.yaml python-test:latest -v
# refer output at /build and push/build-squash.json

# Build without cache
clnstrt build --no-cache python-test.yaml python-test:latest -v
# refer output at /build and push/build-nocache.json

# Custom cache directory
clnstrt build --cache-dir /tmp/cache python-test.yaml python-test:latest -v
# refer output at /build and push/build-cachedir.json

```

- Purpose: Builds a Docker image using the provided config.yaml file.
- How It Works: The clnstrt build command reads the config.yaml file, installs the specified base image and packages, sets environment variables, and configures the image according to the YAML specifications.
- Outcome: A new Docker image named python-test:latest is created.

---

### Detailed Image Analysis

Analyze a container image and provide detailed information about its structure, security posture and performance characteristics.

```bash
# Basic analysis
clnstrt analyze python-test:latest -v
# refer output at /build and push/analyze.txt

# Using config file
clnstrt analyze -c python-test.yaml python-test:latest -v
# refer output at /build and push/analyze-c.txt
```

- Purpose: Facilitates the analysis of container images by providing detailed insights into their structure, security posture, and performance characteristics.
- How It Works: The clnstrt analyze command examines a container image, offering comprehensive information about its internal components. Users can request detailed analysis of the image’s structure, including its layers, dependencies, and configurations. The command also includes options for security analysis, highlighting vulnerabilities or misconfigurations, as well as performance metrics to assess efficiency and resource usage. 
- Outcome: This command helps users assess the quality, security, and performance of container images, enabling more informed decision-making for deployment and optimization across various environments. It ensures that users can gain a complete understanding of an image’s behavior and potential risks, assisting in better management and compliance.

---

### Layer Management

Displays detailed information about the image layers.

```bash
# Inspect image layers 
clnstrt layer inspect python-test:latest -v
# refer output at /build and push/layer.txt

# Compare layers between images
clnstrt layer compare python-test:latest python:latest -v
# refer output at /build and push/layer-compare.txt

# Optimize layers
clnstrt layer optimize python-test:latest -v
# refer output at /build and push/layer-optimize.txt
```

- Purpose: Manages image layers to optimize and inspect images.
- How It Works: The inspect command displays layer details, optimize improves efficiency, and compare highlights differences between images.
- Outcome: Layer details, optimization results, and comparison differences.

---

### Difference between two images - Compare Images

Compares two images and shows exactly what changed across layers and files.

```bash
# Compare two images
clnstrt diff python-test:latest python:latest -v
# Outout will be similar to this:
# Comparing images:
#   1: python-test:latest
#   2: python:latest
# Output will be written to: diff_20251031_130657.csv
# Adjusting output filename to ensure .json extension: diff_20251031_130657.json
# Successfully wrote comparison report to: diff_20251031_130657.json
# refer output at /build and push/diff_20251031_130657.json

# Compare same image (should show no differences)
clnstrt diff python-test:latest python-test:latest -v
# Outout will be similar to this:
# Comparing images:
#   1: python-test:latest
#   2: python-test:latest
# Output will be written to: diff_20251029_115654.csv
# Adjusting output filename to ensure .json extension: diff_20251029_115654.json
# Successfully wrote comparison report to: diff_20251029_115654.json
# refer output at /build and push/diff_20251029_115654.json
```

- Detailed differences between images including layers and files.

---

### push image to Registry

#### Authentication Setup and login to your registry account

```bash
# For Docker Hub
docker login
# For private registries
docker login your-registry.com
```

#### Authenticates and uploads a tagged image to a docker registry.

```bash
# Push to Docker Hub (requires username/image format)
clnstrt push -u username -p password username/image:tag -v
# Outout will be similar to this:
# Pushing image: username/python-test:latest
# The push refers to repository [docker.io/username/python-test]
# [47536822ea4a] Preparing
# [dd470f20ade0] Preparing
# [256f393e029f] Preparing
# [dd470f20ade0] Layer already exists
# [47536822ea4a] Layer already exists
# [256f393e029f] Layer already exists
# [256f393e029f] latest: digest: sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx size: 946
# [256f393e029f] latest: digest: sha256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx size: 946
# Successfully pushed username/python-test:latest
```

---