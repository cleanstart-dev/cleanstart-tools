## Create analysis reports for container images in multiple formats.

### Generate Reports

#### Produces image analysis reports in these formats (JSON/HTML/plain) for audits and sharing.

```bash
# JSON report (console output)
clnstrt report --format json python-test:latest -v
# refer output at /reports/e32c6d95-c163-4b1f-b6f9-b51a1288a4d4.json

# Plain text report to file
clnstrt report --format plain python-test:latest -v
# refer output at /reports/328f210d-3533-4fef-9f59-590904c6a8bf.plain

# html text report to file
clnstrt report --format html python-test:latest -v
# refer output at /reports/a45f77a4-b48d-4480-b7fd-b45aa456c853.html
```

- Output Files Generated will be saved with randomly generated filename

#### Formats Available: json, html, plain


- Purpose: Facilitates the generation of detailed analysis reports for container images, providing insights into their structure, performance, and security in various formats.
- How It Works: The clnstrt report command analyzes a specified container image and produces a comprehensive report. Users can customize the report's format (e.g., JSON, HTML, plain text) and specify an output directory or file path. This flexibility allows users to generate and store analysis results in their preferred format for easy sharing, review, or archival.
- Outcome: This command ensures a streamlined process for documenting container image insights, enabling users to understand and share key details about image structure, dependencies, security vulnerabilities, and performance metrics. It helps with audits, compliance, and optimization, providing actionable data in a format suitable for diverse stakeholders.