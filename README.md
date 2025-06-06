# API Token Monitor

A GitHub Actions workflow that monitors API token usage and sends Discord notifications when issues are detected.

## Features

- ✅ Monitors API token status every 30 minutes
- 🚨 Sends Discord alerts when "requires more credits" is detected
- ⚠️ Detects other token-related warnings and API failures
- 📊 Sends success notifications to confirm monitoring is working
- 🔧 Tests Discord webhook connectivity
- 🔍 Enhanced error handling and debugging

## Setup

### 1. GitHub Secrets

You need to configure these secrets in your GitHub repository:

- `API_TOKEN`: Your OpenRouter API token
- `DISCORD_WEBHOOK_URL`: Your Discord webhook URL

To add secrets:
1. Go to your GitHub repository
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret" for each secret

### 2. Discord Webhook Setup

1. Go to your Discord server
2. Right-click on the channel where you want notifications
3. Select "Edit Channel" → "Integrations" → "Webhooks"
4. Click "New Webhook"
5. Copy the webhook URL and add it as `DISCORD_WEBHOOK_URL` secret

## Troubleshooting

### Not Getting Notifications?

1. **Check if the workflow is running:**
   - Go to the "Actions" tab in your GitHub repository
   - Look for recent runs of "API Token Monitor"

2. **Manual trigger:**
   - Go to Actions → API Token Monitor
   - Click "Run workflow" to trigger manually

3. **Check secrets:**
   - Ensure `API_TOKEN` and `DISCORD_WEBHOOK_URL` are properly set
   - Webhook URL should look like: `https://discord.com/api/webhooks/...`

4. **Check Discord permissions:**
   - Ensure the webhook has permission to post in the channel
   - Verify the webhook URL is correct and active

5. **Review workflow logs:**
   - Check the Actions tab for any error messages
   - Look for failed steps or HTTP errors

### Notification Types

- 🚨 **TOKENS EXHAUSTED**: Sent when API response contains "requires more credits"
- ⚠️ **Token Warning**: Sent when other token-related issues are detected
- 🚨 **API Failure**: Sent when API calls fail (HTTP errors)
- ✅ **Success**: Sent when API check passes (confirms monitoring is working)
- 🔧 **Test**: Sent to verify webhook connectivity

## Manual Testing

To test the workflow immediately:

1. Go to GitHub Actions
2. Select "API Token Monitor" workflow
3. Click "Run workflow"
4. Check Discord for notifications

## Schedule

The workflow runs automatically every 30 minutes, providing frequent monitoring of your API token status.
