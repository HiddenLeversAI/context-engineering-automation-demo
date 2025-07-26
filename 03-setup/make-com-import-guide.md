# Make.com Workflow Import Guide

## Prerequisites

Before importing the workflow, ensure you have:

- [ ] **Make.com account** (Pro plan recommended for advanced features)
- [ ] **Airtable account** with API access
- [ ] **Google Workspace account** (Google Docs integration)
- [ ] **OpenAI API key** with GPT-4 access
- [ ] **Webhook endpoint** capability (provided by Make.com)

## Step 1: Import Workflow Blueprint

1. **Log into Make.com**
   - Navigate to your Make.com dashboard
   - Click "Create a new scenario"

2. **Import JSON Blueprint**
   - Click the three dots menu in scenario editor
   - Select "Import Blueprint"
   - Upload `../01-workflows/transcript-cleanup-tagging-v3.json`

3. **Verify Import**
   - Confirm all modules loaded correctly
   - Check for any missing connections (red warning icons)

## Step 2: Configure API Connections

### Airtable Connection
1. **Create Connection**
   - Click on Airtable module
   - Add new connection
   - Enter your Airtable Personal Access Token

2. **Configure Base Settings**
   - Base ID: `appv6znNqj8jmKf5D` (or your base ID)
   - Table: `Asset Library`
   - Fields: Ensure all required fields exist in your base

### Google Docs Connection
1. **OAuth Setup**
   - Click Google Docs module
   - Authenticate with Google account
   - Grant document read/write permissions

2. **Test Connection**
   - Verify access to target Google Drive folder
   - Confirm document creation permissions

### OpenAI Connection
1. **API Key Configuration**
   - Click OpenAI module
   - Add your OpenAI API key
   - Select GPT-4 model (recommended)

2. **Configure Parameters**
   - Temperature: `0.3` (for consistent tagging)
   - Max Tokens: `250`
   - Model: `gpt-4` or `gpt-4-turbo`

## Step 3: Configure Webhook Trigger

1. **Generate Webhook URL**
   - Click the webhook module (first module)
   - Copy the generated webhook URL
   - Note: This URL will trigger your workflow

2. **Configure Airtable Automation**
   - In your Airtable base, create an automation
   - Trigger: "When record enters view" or "When record updated"
   - Action: "Send webhook" to the URL from step 1

## Step 4: Test the Workflow

### Sample Test Data
```json
{
  "recordId": "recXXXXXXXXXXXXXX",
  "fields": {
    "Asset/File Name": "Test Transcript",
    "Transcript Doc URL": "https://docs.google.com/document/d/YOUR_DOC_ID/edit",
    "⚡ Tag Content?": true
  }
}
```

### Testing Steps
1. **Manual Test**
   - Click "Run once" in Make.com
   - Send test webhook payload
   - Monitor execution log

2. **End-to-End Test**
   - Add a record to your Airtable base
   - Ensure it triggers the webhook
   - Verify the complete workflow execution

## Step 5: Configure Error Handling

1. **Error Filters**
   - Review error handling modules
   - Configure retry logic (3 attempts recommended)
   - Set up error notifications

2. **Monitoring**
   - Enable execution history logging
   - Set up email notifications for failures
   - Configure webhook delivery monitoring

## Common Issues & Solutions

### Connection Errors
- **Airtable 401 Unauthorized**: Check API token permissions
- **Google Docs 403 Forbidden**: Verify document sharing settings
- **OpenAI Rate Limit**: Implement exponential backoff

### Data Flow Issues
- **Missing Fields**: Ensure Airtable schema matches expected fields
- **Empty Responses**: Check OpenAI prompt configuration
- **Webhook Timeouts**: Increase timeout settings in Make.com

### Performance Optimization
- **Execution Time**: Monitor average processing time per document
- **API Quotas**: Track usage against service limits
- **Error Rates**: Maintain <2% error rate for production use

## Production Deployment

### Security Checklist
- [ ] Use environment variables for API keys
- [ ] Implement webhook signature verification
- [ ] Set up proper IAM roles for service accounts
- [ ] Enable audit logging for all integrations

### Scalability Considerations
- [ ] Configure auto-scaling for high-volume processing
- [ ] Implement queue management for batch processing
- [ ] Set up monitoring and alerting
- [ ] Plan for API rate limit management

### Maintenance
- [ ] Schedule regular connection testing
- [ ] Monitor execution logs weekly
- [ ] Update API integrations as needed
- [ ] Review and optimize prompts monthly

## Support Resources

- **Make.com Documentation**: [make.com/help](https://make.com/help)
- **Airtable API Docs**: [airtable.com/developers](https://airtable.com/developers)
- **OpenAI API Reference**: [platform.openai.com/docs](https://platform.openai.com/docs)

## Next Steps

After successful setup:
1. Review `../04-documentation/workflow-architecture.md` for technical details
2. Examine sample outputs in `../02-examples/cleaned-outputs/`
3. Customize the tagging taxonomy for your use case
4. Scale the workflow for production volume

---

**Note**: This workflow processes sensitive content. Ensure all API connections use proper authentication and comply with your organization's data security policies.