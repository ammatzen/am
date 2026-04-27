# 👓 Weekly Eye Trends Dashboard

Automated Google Trends report for eyewear & eye health, delivered every Monday via email and logged to Google Sheets.

---

## Project Structure

your-repo/
├── .github/
│   └── workflows/
│       └── weekly_trends.yml
├── trends_dashboard.py
├── requirements.txt
└── README.md

---

## One-Time Setup

### Step 1 — SerpAPI Key
1. Sign up at https://serpapi.com
2. Copy your API key from the Dashboard
3. Free tier = 100 searches/month

### Step 2 — Gmail App Password
1. Enable 2-Factor Authentication on your Google account
2. Go to Google Account → Security → App Passwords
3. Generate a password for "Mail / Other"
4. Save the 16-character password — this is your EMAIL_PASSWORD

### Step 3 — Google Sheets + Service Account
1. Go to https://console.cloud.google.com
2. Enable Google Sheets API and Google Drive API
3. Go to IAM & Admin → Service Accounts → Create Service Account
4. Click the service account → Keys → Add Key → JSON and download it
5. Create a new Google Sheet at https://sheets.google.com
6. Copy the Sheet ID from the URL
7. Share the Sheet with the service account email (Editor access)

### Step 4 — GitHub Secrets
Go to Settings → Secrets and variables → Actions → New repository secret

| Secret Name         | Value                                          |
|---------------------|------------------------------------------------|
| SERPAPI_KEY         | Your SerpAPI key                               |
| EMAIL_FROM          | Your Gmail address                             |
| EMAIL_TO            | Recipient email                                |
| EMAIL_PASSWORD      | Your 16-char Gmail App Password                |
| GSHEET_ID           | The Sheet ID from the URL                      |
| GOOGLE_CREDS_JSON   | Full contents of the service account JSON file |

### Step 5 — Test It
Go to Actions → Weekly Eye Trends Dashboard → Run workflow to trigger manually.

---

## Google Sheets Output

The script auto-creates a "Weekly Log" tab with these columns:

| Week | Keyword | Avg Interest (0–100) | Peak | Direction |
|------|---------|----------------------|------|-----------|
| April 28, 2025 | blue light glasses | 74.3 | 100 | 📈 |

---

## Customizing Keywords

Edit the KEYWORDS list in trends_dashboard.py to add or remove terms.
Max 5 per SerpAPI call, but you can have as many groups as you like.

---

## Adjusting the Schedule

Edit the cron expression in weekly_trends.yml:
0 12 * * 1  →  Every Monday at 12:00 UTC (8:00 AM Eastern)
