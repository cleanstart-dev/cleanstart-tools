Create analysis reports for container images in multiple formats.

### 📋 Reporting & Documentation

#### report - Generate Reports

Produces image analysis reports in these formats (JSON/HTML/PDF/CSV/plain) for audits and sharing.

```bash
# JSON report (console output)
clnstrt report --format json image:tag
# Save JSON report to file
clnstrt report --format json --output analysis-report.json image:tag
# HTML report with custom output file
clnstrt report --format html --output custom-report.html image:tag
# PDF report saved to directory
clnstrt report --format pdf --dir ./reports image:tag
# Plain text report to file
clnstrt report --format plain --output report.txt image:tag
# CSV format report (if supported)
clnstrt report --format csv --output report.csv image:tag
# Report with custom directory and filename
clnstrt report --format json --dir ./security-reports --output detailed-analysis.json image:tag
```

Output Files Generated:

- `analysis-report.json` - Complete analysis in JSON format
- `custom-report.html` - Interactive HTML report with charts
- `report.txt` - Human-readable plain text report
- `report.csv` - Spreadsheet-compatible analysis data
- `./reports/` - Directory containing PDF reports
- `./security-reports/detailed-analysis.json` - Custom location report

Formats Available: json, html, pdf, plain, csv


Purpose: Facilitates the generation of detailed analysis reports for container images, providing insights into their structure, performance, and security in various formats.
How It Works: The clnstrt report command analyzes a specified container image and produces a comprehensive report. Users can customize the report's format (e.g., JSON, HTML, PDF, or plain text) and specify an output directory or file path. This flexibility allows users to generate and store analysis results in their preferred format for easy sharing, review, or archival.
Outcome: This command ensures a streamlined process for documenting container image insights, enabling users to understand and share key details about image structure, dependencies, security vulnerabilities, and performance metrics. It helps with audits, compliance, and optimization, providing actionable data in a format suitable for diverse stakeholders.