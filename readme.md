# Google Meet Recording Bot - Setup and Usage

This document explains how to set up and use the Google Meet recording bot.

## Prerequisites

Before you begin, make sure you have the following:

1. Node.js installed (version 14 or higher)
2. A Google account (regular Gmail is fine)
3. Google Drive API credentials (for uploading recordings)

## Installation

1. Create a new directory for the project:
```bash
mkdir google-meet-bot
cd google-meet-bot
```

2. Initialize a new Node.js project:
```bash
npm init -y
```

3. Install the required dependencies:
```bash
npm install puppeteer-extra puppeteer-extra-plugin-stealth google-apis-nodejs-client google-auth-library dotenv
```

4. Create the main files:
```bash
touch index.js recording-utils.js .env
```

5. Copy the code from the provided artifacts into `index.js` and `recording-utils.js`

## Configuration

1. Set up Google Drive API:
   - Go to the [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project
   - Enable the Google Drive API
   - Create OAuth 2.0 credentials
   - Download the credentials JSON file

2. Configure your environment variables in the `.env` file:
```
GOOGLE_EMAIL=your-email@gmail.com
GOOGLE_PASSWORD=your-password
GOOGLE_CLIENT_ID=your-client-id
GOOGLE_CLIENT_SECRET=your-client-secret
REDIRECT_URI=http://localhost:3000/oauth2callback
REFRESH_TOKEN=your-refresh-token
MEET_LINK=https://meet.google.com/xxx-xxxx-xxx
OUTPUT_FOLDER=./recordings
UPLOAD_TO_DRIVE=true
DRIVE_FOLDER_ID=folder-id-or-root
```

3. Obtain a refresh token for Google Drive API access:
   - Run a script to get an authorization URL
   - Visit the URL and authorize your application
   - Extract the refresh token from the response

## Usage

Run the bot to join and record a meeting:

```bash
node index.js
```

The bot will:
1. Launch a browser window
2. Log in to your Google account
3. Join the specified Google Meet session
4. Start recording the screen and audio
5. Continue recording until you press Ctrl+C or the meeting ends
6. Save the recording locally and optionally upload it to Google Drive

## Customization

You can modify the code to:
- Schedule recordings at specific times
- Join multiple meetings sequentially
- Change recording quality settings
- Add notifications when recordings complete

## Limitations

- The recording quality depends on your internet connection
- Google Meet may detect and prevent automated logins (use the stealth plugin to minimize this risk)
- The bot needs to run on a computer with audio capabilities
- Extended recordings require sufficient disk space

## Troubleshooting

If you encounter issues:
1. Check that your Google account credentials are correct
2. Ensure your Google Drive API credentials have the necessary permissions
3. Verify that puppeteer can access your Google account (CAPTCHA issues may prevent login)
4. Make sure your computer has audio capabilities enabled