# API Token Monitor

A GitHub Actions workflow that monitors API token usage and sends Discord notifications.

## Features

- ✅ Monitors API token status every 30 minutes
- 📊 Sends API responses to Discord for monitoring
- ⏱️ Includes timestamps with each notification
- 🔄 Can be triggered manually or runs on schedule
- 📝 Formats JSON responses for easy reading

## Setup

### 1. GitHub Secrets

You need to configure these secrets in your GitHub repository:

- `API_KEY`: Your OpenRouter API key
- `DISCORD_WEBHOOK_URL`: Your Discord webhook URL
- `GMAIL_USERNAME`: Your Gmail email address
- `GMAIL_APP_PASSWORD`: An app password for your Gmail account
- `GMAIL_RECIPIENT`: Email address to receive notifications (can be same as GMAIL_USERNAME)

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

### 3. Gmail Setup for Email Notifications

To configure Gmail for sending email notifications when tokens are exhausted:

1. **Create an App Password for Gmail:**
   - Go to your Google Account settings (myaccount.google.com)
   - Select "Security"
   - Enable 2-Step Verification if not already enabled
   - Go to "App passwords" (under "Signing in to Google")
   - Create a new app password for "Mail" and "Other (Custom name)" - name it "API Token Monitor"
   - Copy the generated 16-character password

2. **Add Gmail Secrets to GitHub:**
   - Add these secrets to your repository:
     - `GMAIL_USERNAME`: Your full Gmail address (e.g., yourname@gmail.com)
     - `GMAIL_APP_PASSWORD`: The 16-character app password you generated
     - `GMAIL_RECIPIENT`: Email address that should receive notifications

3. **Important Notes:**
   - Never use your regular Gmail password - always use an app password
   - Gmail requires secure connections (SSL/TLS), which is configured in the workflow
   - You may need to check your spam folder for the first few notifications

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

- 🚨 **TOKENS EXHAUSTED**: Sent to Discord and Email when API response contains "requires more credits"
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
