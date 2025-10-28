Create python-test.yaml using "nano python-test.yaml" and paste below config file.

Build a Minimal Docker Image

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


Purpose of the YAML Configuration:

Base Image: Specifies the base image (alpine:latest) from which the build will start.
Packages: Lists additional packages to be installed in the container (e.g., curl, python3).
Environment Variables: Defines the environment variables for the container.
Work Directory: Sets the working directory for executing commands (/app).
User: Specifies the user under which commands will run (nobody).
Command: Default command to execute when the container runs.
Labels: Metadata labels for the image.

#### Build - Build Container Images

Builds a new container image from a declarative config with options for caching and squashing.

```bash
# Basic build
clnstrt build python-test.yaml python-test:latest
# Build with squashed layers
clnstrt build --squash python-test.yaml python-test:latest
# Build without cache
clnstrt build --no-cache python-test.yaml python-test:latest
# Custom cache directory
clnstrt build --cache-dir /tmp/cache python-test.yaml python-test:latest
```

Purpose: Builds a Docker image using the provided config.yaml file.
How It Works: The clnstrt build command reads the config.yaml file, installs the specified base image and packages, sets environment variables, and configures the image according to the YAML specifications.
Outcome: A new Docker image named python-test:latest is created.
Required: Config file with from: field specifying base image.

---

#### analyze - Detailed Image Analysis

Analyze a container image and provide detailed information about its structure, security posture and performance characteristics.

```bash
# Basic analysis
clnstrt analyze python-test:latest
# With verbose output
clnstrt analyze -v python-test:latest
# Using config file
clnstrt analyze -c python-test.yaml python-test:latest
```

Purpose: Facilitates the analysis of container images by providing detailed insights into their structure, security posture, and performance characteristics.
How It Works: The clnstrt analyze command examines a container image, offering comprehensive information about its internal components. Users can request detailed analysis of the image’s structure, including its layers, dependencies, and configurations. The command also includes options for security analysis, highlighting vulnerabilities or misconfigurations, as well as performance metrics to assess efficiency and resource usage. 
Outcome: This command helps users assess the quality, security, and performance of container images, enabling more informed decision-making for deployment and optimization across various environments. It ensures that users can gain a complete understanding of an image’s behavior and potential risks, assisting in better management and compliance.

---

#### layer - Layer Management

Displays detailed information about the image layers in that having layers' metadata, including size and content.

```bash
# Inspect image layers
clnstrt layer inspect image:tag
# Compare layers between images  
clnstrt layer compare image1:tag image2:tag
# Optimize layers
clnstrt layer optimize image:tag
```

Purpose: Manages image layers to optimize and inspect images.
How It Works: The inspect command displays layer details, optimize improves efficiency, and compare highlights differences between images.
Outcome: Layer details, optimization results, and comparison differences.

---

#### difference between two images - Compare Images

Compares two images and shows exactly what changed across layers and files.

```bash
# Compare two images
clnstrt diff image1:tag image2:tag -v
# Compare same image (should show no differences)
clnstrt diff image:tag image:tag
```

Detailed differences between images including layers and files.

---

#### push - Push to Registry

### Authentication Setup and login to your registry account

```bash
# For Docker Hub
docker login
# For private registries
docker login your-registry.com
```

Authenticates and uploads a tagged image to a docker registry.

```bash
# Push to Docker Hub (requires username/image format)
clnstrt push -u username -p password username/image:tag
# Push with verbose output
clnstrt push -u username -p password username/image:tag -v
```

---