## Package Management

Lists and exports OS/application packages detected inside an image.

```bash
# List packages in image
clnstrt package image-packages python-test:latest -v
# refer output at /list packages/imagespackages.txt

# General package list
clnstrt package list python-test:latest -v
# Outout will be similar to this:
# Package list saved to packages.txt in txt format
# refer output at /list packages/packages.txt


# With output format
clnstrt package image-packages --format json python-test:latest -v
# Outout will be similar to this:
# Package analysis saved to: image_packages_python-test_latest.json
# refer output at /list packages/image_packages_python-test_latest.json

# Save to file
clnstrt package image-packages python-test:latest --format json --output packages.json -v
# Outout will be similar to this:
# Package analysis saved to: packages.json
# refer output at /list packages/packages.json
```

- Purpose: Searches, installs, and manages packages within a container image.
- How It Works: The clnstrt package command provides functionality to inspect and manage packages within container images. The image-packages subcommand lists the packages present in an image, while the list subcommand retrieves a list of packages available for management or installation.
- Outcome: The command displays package information from container images, helping users manage, verify and maintain package states effectively.

- Note: Some minimal images may return "no packages found".
