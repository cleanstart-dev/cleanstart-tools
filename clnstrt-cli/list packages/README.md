## Package Management

Lists and exports OS/application packages detected inside an image.

```bash
# List packages in image
clnstrt package image-packages image:tag
# General package list
clnstrt package list
# With output format
clnstrt package image-packages --format json image:tag
# Save to file
clnstrt package image-packages --output packages.csv image:tag
```

- Purpose: Searches, installs, and manages packages within a container image.
- How It Works: The clnstrt package command provides functionality to inspect and manage packages within container images. The image-packages subcommand lists the packages present in an image, while the list subcommand retrieves a list of packages available for management or installation.
- Outcome: The command displays package information from container images, helping users manage, verify and maintain package states effectively.

- Note: Some minimal images may return "no packages found".
