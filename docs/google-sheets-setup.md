# Google Sheets Registration Backend — Setup Guide

## Step 1: Create the Google Sheet

1. Go to https://sheets.google.com → **Blank spreadsheet**
2. Name it: `VITVI Workshop 2026 — Registrations`
3. In **row 1**, paste these headers (one per cell, A1 through M1):

```
timestamp | participant_type | name | email | affiliation | role | topic | attendance | presenting | topics_interest | hotel | dinner_may6 | lunch_may7 | dietary | billing_address
```

## Step 2: Add the Apps Script

1. In your spreadsheet, go to **Extensions → Apps Script**
2. Delete any existing code in `Code.gs`
3. Paste the following:

```javascript
function doPost(e) {
  var data = e.parameter;

  // Server-side domain whitelist
  var ALLOWED_DOMAINS = [
    'th-brandenburg.de',
    'rolls-royce.com',
    'friendship-systems.com',
    'tu-berlin.de',
    'b-tu.de'
  ];
  var email = (data.email || '').toLowerCase().trim();
  var domain = email.split('@')[1] || '';
  var allowed = ALLOWED_DOMAINS.some(function(d) {
    return domain === d || domain.endsWith('.' + d);
  });
  if (!allowed) {
    return ContentService
      .createTextOutput(JSON.stringify({ result: 'rejected', reason: 'domain' }))
      .setMimeType(ContentService.MimeType.JSON);
  }

  // Honeypot check
  if (data.website) {
    return ContentService
      .createTextOutput(JSON.stringify({ result: 'rejected', reason: 'bot' }))
      .setMimeType(ContentService.MimeType.JSON);
  }

  // Captcha check — answer must match expected value
  if (data.captcha !== data.captcha_answer) {
    return ContentService
      .createTextOutput(JSON.stringify({ result: 'rejected', reason: 'captcha' }))
      .setMimeType(ContentService.MimeType.JSON);
  }

  // Rate limiting — max 3 submissions per email per hour
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var rows = sheet.getDataRange().getValues();
  var oneHourAgo = new Date(Date.now() - 3600000);
  var recentCount = 0;
  for (var i = 1; i < rows.length; i++) {
    if (rows[i][3] === email && new Date(rows[i][0]) > oneHourAgo) {
      recentCount++;
    }
  }
  if (recentCount >= 3) {
    return ContentService
      .createTextOutput(JSON.stringify({ result: 'rejected', reason: 'rate_limit' }))
      .setMimeType(ContentService.MimeType.JSON);
  }

  sheet.appendRow([
    new Date().toISOString(),
    data.participant_type || '',
    data.name || '',
    data.email || '',
    data.affiliation || '',
    data.role || '',
    data.topic || '',
    data.attendance || '',
    data.presenting || '',
    data.topics_interest || '',
    data.hotel || '',
    data.dinner_may6 || '',
    data.lunch_may7 || '',
    data.dietary || '',
    data.billing_address || ''
  ]);

  return ContentService
    .createTextOutput(JSON.stringify({ result: 'success' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

> **IMPORTANT:** After updating the script, you must create a **new deployment** (Deploy → New deployment) for changes to take effect. The URL will change — update `register.html` with the new URL.

4. Click **Save** (Ctrl+S)

## Step 3: Deploy as Web App

1. Click **Deploy → New deployment**
2. Click the gear icon → select **Web app**
3. Settings:
   - Description: `VITVI Registration`
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Click **Deploy**
5. Click **Authorize access** → choose your Google account → Allow
6. Copy the **Web app URL** (looks like `https://script.google.com/macros/s/.../exec`)

## Step 4: Update the website

Give the Web app URL to your assistant — they'll update `register.html` to POST to it instead of Formspree.

## Step 5: Test

Submit a test registration on the website and check if a new row appears in your Google Sheet.
