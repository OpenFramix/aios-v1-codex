# /install

Set up credentials for this AIOS install by walking through every variable in `.env.example` interactively. Writes `.env` automatically — no manual file editing required.

## When to use
- First time opening a new AIOS install (the system will suggest this if `.env` is missing)
- When setting up on a new machine with a cloned repo
- When adding a new integration and you need to add its credentials

## What it does
1. Reads `.env.example` to find which credentials this client needs
2. Asks for each value one at a time in plain language
3. Writes the completed `.env` file
4. Confirms setup is complete

## Instructions

When the operator runs `/install` (or is prompted to run it because `.env` is missing):

### Step 1 — Check current state
- If `.env` already exists, say: "Credentials are already set up. If you want to update a specific value, tell me which tool you'd like to reconfigure."
- If `.env` is missing and `.env.example` exists, continue to Step 2
- If both are missing, say: "No credential template found. Run `/onboard` first to set up this AIOS."

### Step 2 — Read the template
Read `.env.example`. Parse every line that contains `=` and is not a comment (`#`). Build a list of variables to collect.

### Step 3 — Ask for each value

For each variable, ask using the plain-English prompt from this reference table. If a variable isn't listed, ask generically: *"What is the value for `{VAR_NAME}`?"*

| Variable | Plain-English Prompt |
|---|---|
| `GHL_LOCATION_ID` | "GoHighLevel Location ID — find this in GHL → Settings → Business Profile, or in the URL when you're inside the location (the long code after `/location/`)." |
| `GHL_API_KEY` | "GoHighLevel API Key — find this in GHL → Settings → API Keys. Create one if it doesn't exist yet." |
| `GHL_PIT_TOKEN` | "GoHighLevel Private Integration Token (PIT) — find this in GHL → Settings → Private Integrations. Create a new integration for this AIOS if needed." |
| `GMAIL_ADDRESS` | "Gmail address for this AIOS — the email account you want to connect for sending and reading email." |
| `GOOGLE_CREDENTIALS_PATH` | "Path to your Google OAuth credentials file. If you haven't set up Google OAuth yet, press Enter to skip — you'll need to complete the OAuth flow separately. Default: `credentials.json`" |
| `HUBSPOT_PORTAL_ID` | "HubSpot Portal ID — find this in HubSpot → Account Settings → Account Details." |
| `HUBSPOT_API_KEY` | "HubSpot API Key — find this in HubSpot → Settings → Integrations → API Key." |
| `OUTLOOK_EMAIL` | "Outlook / Microsoft 365 email address for this AIOS." |
| `MS_CLIENT_ID` | "Microsoft App Client ID — from your Azure app registration." |
| `MS_CLIENT_SECRET` | "Microsoft App Client Secret — from your Azure app registration." |
| `CALENDLY_API_KEY` | "Calendly API Key — find this in Calendly → Integrations → API & Webhooks." |
| `STRIPE_SECRET_KEY` | "Stripe Secret Key — find this in Stripe Dashboard → Developers → API Keys. Use the secret key (starts with `sk_`)." |
| `STRIPE_WEBHOOK_SECRET` | "Stripe Webhook Secret — find this in Stripe Dashboard → Developers → Webhooks, next to your webhook endpoint." |
| `N8N_WEBHOOK_BASE_URL` | "n8n Webhook Base URL — the base URL where your n8n instance receives webhooks (e.g., `https://n8n.yourdomain.com/webhook`)." |
| `OPENROUTER_API_KEY` | "OpenRouter API Key — find this at openrouter.ai under your account settings." |
| `SLACK_BOT_TOKEN` | "Slack Bot Token — starts with `xoxb-`. Find this in your Slack app settings under OAuth & Permissions." |
| `SLACK_SIGNING_SECRET` | "Slack Signing Secret — find this in your Slack app settings under Basic Information." |
| `NOTION_API_KEY` | "Notion API Key — find this at notion.so/my-integrations after creating an integration." |
| `NOTION_DATABASE_ID` | "Notion Database ID — the long code in the URL when you open the database page in Notion." |
| `AIRTABLE_API_KEY` | "Airtable API Key — find this in Airtable → Account → API section." |
| `AIRTABLE_BASE_ID` | "Airtable Base ID — find this in the API docs for your base (starts with `app`)." |
| `TWILIO_ACCOUNT_SID` | "Twilio Account SID — find this on your Twilio Console dashboard." |
| `TWILIO_AUTH_TOKEN` | "Twilio Auth Token — find this on your Twilio Console dashboard, next to the Account SID." |
| `TWILIO_PHONE_NUMBER` | "Twilio Phone Number — the phone number you purchased in Twilio (format: +15551234567)." |

Allow the operator to press Enter to skip a value (it will be left empty in `.env`). Skipped values can be filled in later by re-running `/install`.

### Step 4 — Write `.env`
Write all collected values to `.env` in the same format as `.env.example`, preserving section headers and comments.

### Step 5 — Confirm
```
Credentials saved to .env

Connected:
  ✓ {Tool} — {variable name}
  (list each filled variable)

Skipped:
  - {variable name} — fill this in later when you set up {tool}

.env is gitignored — these credentials stay on this machine only.
Run /onboard if you haven't completed setup yet.
```

## Notes
- Never print credential values back to the screen — confirm the variable name only
- `.env` is gitignored — it will never be pushed to GitHub
- If the client runs `/sync-up`, `.env` is excluded automatically
- To update a single credential later: "Update my GHL API key" — the skill edits only that line
