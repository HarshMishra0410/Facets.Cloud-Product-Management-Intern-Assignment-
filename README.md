# AI DriftGuard – Facets Prototype

An intelligent n8n workflow that automatically detects and analyzes configuration drift between Dev and Production environments using AI-powered analysis.

## Overview

AI DriftGuard monitors configuration differences across environments and provides intelligent summaries of discrepancies, helping teams maintain consistency and catch potential issues before they impact production.

## Features

-  **Automated Drift Detection**: Compares Dev and Prod configurations in real-time
- **AI-Powered Analysis**: Uses OpenAI to provide context-aware summaries of differences
-  **Structured Logging**: Automatically logs drift events to Google Sheets
-  **Chat Interface**: Interactive workflow triggered via chat messages
-  **Structured Output**: Consistent, parseable drift reports

## Workflow Architecture

```
Chat Trigger → Fetch Dev Config → Fetch Prod Config → JavaScript Analysis
                                                              ↓
                                                        Compare Datasets
                                                              ↓
                                                          AI Agent
                                                              ↓
                                                    Append to Google Sheet
```

## Components

### 1. Configuration Fetching
- **Fetch Dev Config**: Retrieves development environment configuration
- **Fetch Prod Config**: Retrieves production environment configuration
- Uses mock API endpoints (replaceable with actual config sources)

### 2. Drift Analysis
- **JavaScript Code Node**: Performs initial comparison between configs
- **Compare Datasets Node**: Deep comparison with fuzzy matching support
- Identifies parameters with differing values across environments

### 3. AI Processing
- **AI Agent**: Analyzes drift data and generates human-readable summaries
- **OpenAI Chat Model**: GPT-3.5-turbo with optimized parameters
  - Temperature: 0.7 (balanced creativity/consistency)
  - Max Tokens: 512
- **Structured Output Parser**: Ensures consistent JSON output format

### 4. Logging
- **Google Sheets Integration**: Automatically appends drift records with:
  - Timestamp
  - Drift type
  - Difference summary
  - Status
  - AI-generated comments

## Setup Instructions

### Prerequisites
- n8n instance (self-hosted or cloud)
- OpenAI API account
- Google Sheets API access

### Configuration

1. **OpenAI Credentials**
   - Add your OpenAI API key to n8n credentials
   - Credential ID: `bbs5UEcxXicEA9m9` (or create new)

2. **Google Sheets Credentials**
   - Set up Google OAuth2 credentials in n8n
   - Credential ID: `yDvWqa4sN8hBHgeo` (or create new)
   - Grant access to your target spreadsheet

3. **Configuration Endpoints**
   - Update the HTTP Request nodes with your actual config endpoints:
     ```
     Dev Config:  https://your-api.com/dev/config
     Prod Config: https://your-api.com/prod/config
     ```

4. **Google Sheet**
   - Create a spreadsheet with columns:
     - `timestamp`
     - `drift_type`
     - `difference_summary`
     - `status`
     - `ai_comment`
   - Update the document ID in the "Append row in sheet" node

## Usage

### Manual Trigger
1. Open the workflow in n8n
2. Click "Test Workflow"
3. The chat trigger will initiate the drift analysis

### Automated Execution
Configure the workflow to run:
- On a schedule (add a Schedule Trigger node)
- Via webhook (use the existing chat webhook)
- On external events (add appropriate trigger nodes)

## Output Format

The AI Agent produces structured output:

```json
{
  "summary": "Brief overview of configuration drift",
  "differences": [
    {
      "parameter": "database_host",
      "dev_value": "localhost",
      "prod_value": "prod-db.company.com"
    }
  ]
}
```

## Customization

### Adjusting AI Behavior
Modify the AI Agent prompt to change analysis style:
```javascript
text: "You are an AI drift analyzer..."
```

### Adding Filters
Extend the JavaScript code to:
- Ignore certain parameters
- Flag critical differences
- Apply custom business logic

### Enhanced Notifications
Add nodes for:
- Slack/Teams notifications
- Email alerts for critical drift
- Webhook integrations for incident management tools

## Best Practices

1. **Regular Monitoring**: Schedule the workflow to run at appropriate intervals
2. **Threshold Alerts**: Set up conditions to only alert on significant drift
3. **Audit Trail**: Maintain the Google Sheet as a historical record
4. **Review Cycle**: Regularly review AI summaries for accuracy
5. **Config Source**: Use version-controlled config sources when possible

## Troubleshooting

### Common Issues

**No drift detected despite differences:**
- Check the Compare Datasets fuzzy matching settings
- Verify the JavaScript comparison logic

**AI Agent timeouts:**
- Reduce data size sent to the agent
- Increase timeout settings in the AI Agent node

**Google Sheets errors:**
- Verify OAuth2 credentials are valid
- Check sheet permissions and column names

## Future Enhancements

- [ ] Multi-environment support (QA, Staging, etc.)
- [ ] Drift trend analysis and visualization
- [ ] Automated remediation suggestions
- [ ] Integration with GitOps workflows
- [ ] Custom drift severity scoring
- [ ] Historical drift pattern recognition

## License

[Specify your license]

## Contributing

[Add contribution guidelines]

## Support

For issues and questions:
- Open an issue in the repository
- Contact: [your-contact-info]

---

**Version**: 1.0.0  
**Last Updated**: 2025-11-03  
**n8n Version Compatibility**: 1.0+
