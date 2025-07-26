# Troubleshooting Guide

> **⚠️ DEMO PURPOSES ONLY**: This troubleshooting guide is provided for demonstration and educational purposes. For production implementations, consult with Content Leverage OS© for official support.

## Common Issues & Solutions

### Workflow Import Problems

#### Issue: "Blueprint import failed" or missing modules
**Symptoms**: Error during JSON import, some modules don't appear in workflow
**Causes**: 
- Make.com plan limitations
- Missing app connections
- Outdated blueprint format

**Solutions**:
```bash
# For demo purposes only - verify these settings:
1. Ensure Make.com Pro plan (some modules require paid features)
2. Pre-install required apps: Airtable, Google Docs, OpenAI
3. Check JSON file integrity (should be ~29KB)
4. Try importing in new scenario rather than existing one
5. Follow detailed import guide: https://scribehow.com/shared/How_to_Import_a_Makecom_Blueprint_Into_Your_ScenarioWorkflow__1XGGdC5NRo2yAXsjQKOPZA
```

#### Issue: "Webhook URL not generating"
**Symptoms**: First module shows "No webhook URL available"
**Solution**: 
```
Demo Note: This often requires saving the scenario first
1. Save scenario (Ctrl+S)
2. Click webhook module
3. Copy generated URL
4. If still no URL, recreate webhook module from scratch
```

### API Connection Errors

#### Issue: Airtable "401 Unauthorized"
**Demo Configuration**:
```
Error: Invalid API key or insufficient permissions
Solution (Demo Setup):
1. Generate Personal Access Token in Airtable
2. Ensure token has read/write access to demo base
3. Verify base ID matches: appv6znNqj8jmKf5D
4. Check table name: "Asset Library"

Note: For production use, implement proper API key rotation
```

#### Issue: Google Docs "403 Forbidden"
**Demo Troubleshooting**:
```
Error: Cannot access document
Common Causes:
- Document not shared with service account
- Incorrect document ID in URL
- Google account lacks document permissions

Demo Fix:
1. Ensure Google Doc is publicly readable OR
2. Share doc with connected Google account
3. Verify document URL format is correct
```

#### Issue: OpenAI Rate Limiting
**Demo Considerations**:
```
Error: "Rate limit exceeded"
Demo Workaround:
- Reduce test frequency (wait 1 minute between runs)
- Use lower-tier model for testing (gpt-3.5-turbo)
- Implement manual delay in Make.com (sleep module)

Production Note: Enterprise accounts have higher limits
```

### Data Processing Issues

#### Issue: Tags not appearing in Airtable
**Demo Debugging Steps**:
```
1. Check if Tags table exists in your Airtable base
2. Verify tag names match predefined list exactly
3. Ensure Tags field is configured as "Link to another record"
4. Review Make.com execution log for tag conversion errors

Demo Limitation: Uses simplified tag set for demonstration
```

#### Issue: "No content found" in Google Docs
**Demo Solutions**:
```
Symptoms: Workflow runs but no text extracted
Checklist:
- Document contains actual text (not just images)
- Document is not password protected
- Google Docs API has read permissions
- Document ID is correctly extracted from URL

Demo Test: Use provided sample documents first
```

#### Issue: AI tagging produces inconsistent results
**Demo Expectations**:
```
Note: Demo uses simplified prompts for illustration
Expected Accuracy: ~85-90% (demo configuration)
Production Accuracy: 94%+ (with full prompt engineering)

Demo Tuning:
- Temperature set to 0.3 for consistency
- Max tokens: 250 (sufficient for tag lists)
- Review sample outputs for expected format
```

### Workflow Execution Problems

#### Issue: Workflow times out
**Demo Configuration**:
```
Timeout after: 2-3 minutes per document
Causes in Demo:
- Large documents (>10,000 words)
- OpenAI API delays
- Google Docs processing slow

Demo Solutions:
- Use smaller test documents (<2,000 words)
- Increase timeout in Make.com settings
- Split large documents before processing
```

#### Issue: Webhook not triggering
**Demo Setup**:
```
Symptoms: Airtable updates don't start workflow
Debug Steps:
1. Test webhook URL directly with sample data
2. Check Airtable automation is active
3. Verify trigger conditions ("Tag Content?" = true)
4. Review webhook delivery logs in Airtable

Demo Test Data:
{
  "recordId": "recDEMO123456789",
  "fields": {
    "Asset/File Name": "Demo Test",
    "⚡ Tag Content?": true
  }
}
```

#### Issue: Execution fails randomly
**Demo Monitoring**:
```
Common Demo Issues:
- API quotas exceeded (OpenAI, Google, Airtable)
- Network timeouts
- Temporary service outages

Demo Debugging:
1. Check Make.com execution history
2. Review error messages in logs
3. Verify all API services are operational
4. Test with simpler content first
```

## Demo Limitations & Considerations

### Simplified Configuration
```
⚠️ This demo uses simplified settings:
- Basic tag taxonomy (10-15 tags vs. production 100+)
- Single content type processing
- Minimal error handling
- Basic prompt engineering

Production systems include:
- Advanced taxonomy management
- Multi-format content support  
- Comprehensive error handling
- Optimized prompt engineering
- Performance monitoring
```

### Scale Limitations
```
Demo Constraints:
- Processing: 1-5 documents per hour
- API calls: Limited by free tier quotas
- Storage: Minimal sample data
- Features: Core functionality only

Production Capabilities:
- Processing: 40-60 documents per hour
- API calls: Enterprise quota management
- Storage: Unlimited content processing
- Features: Full CLOS automation suite
```

### Data Handling
```
⚠️ Demo Data Notice:
- Use only non-sensitive test content
- Sample data provided for illustration
- No production data should be processed
- All API keys should be demo/test accounts

For production data:
- Implement proper security protocols
- Use enterprise-grade API accounts
- Follow data privacy regulations
- Implement audit logging
```

## Getting Help

### Demo Support Resources
- **Sample Data**: Use provided examples in `02-examples/`
- **Setup Guide**: Follow `03-setup/make-com-import-guide.md` exactly
- **Architecture**: Review `04-documentation/workflow-architecture.md`

### Production Implementation
- **Commercial License**: Visit [contentleverageos.com](https://contentleverageos.com)
- **Enterprise Support**: Contact Hidden Levers AI for production deployments
- **Custom Integration**: Professional services available for complex requirements

### Community Resources
```
⚠️ Demo Disclaimer:
This is a demonstration system only. For production use:
- Professional implementation required
- Enterprise support recommended  
- Custom configuration needed
- Security audit required
```

## Demo Testing Checklist

Before reporting issues, verify:
- [ ] Using provided sample data
- [ ] All API connections configured with demo accounts
- [ ] Following setup guide exactly
- [ ] Testing with simple content first
- [ ] Checking execution logs for specific errors
- [ ] Understanding this is demo-only configuration

---

**Important**: This troubleshooting guide covers demo scenarios only. Production implementations require enterprise-grade configuration, monitoring, and support not covered in this demonstration.

**For Production Use**: Contact Content Leverage OS© for commercial licensing, professional implementation, and enterprise support services.
