---
date: 2025-03-08T23:30:26+05:30
title: "How to Create a Link Tracker with Node.js"
weight: 2
summary: "Learn how to create a simple Node.js tracker that checks if a link is published or not."
---

## Introduction

In our college, we don’t receive official announcements when our results are published. However, we know the exact URL where the results will be posted. If we visit the URL before the results are available, we encounter a classic 404 error.

To solve this problem, we decided to create a link tracker that automatically checks the URL every 60 seconds to determine whether the results have been published.

## Prerequisites

To follow this guide, you will need:

- A computer with Node.js installed
- A GitHub account
- A Vercel account (for free deployment)
- The `ntfy` app (for push notifications)

## Setting Up Notifications

1. Install the `ntfy` app on your mobile device from the Play Store (Android) or the App Store (iOS).
2. Open the app, tap on the `+` icon, and add a topic name. **Remember this topic name.**
3. Tap `Subscribe` and enable the lightning icon at the top right corner for instant notifications (optional).

## Setting Up the Project

### Install Dependencies

1. Open your terminal and navigate to the folder where you want to create the project.
2. Run the following commands:

```bash
npm init -y
npm install express axios
```

### Create the Tracker Script

1. Create a file named `index.js` in your project folder.
2. Paste the following code into `index.js`:

```javascript
const axios = require("axios");
const express = require("express");

const app = express();
const LINK = "YOUR_TARGET_URL";
const ntfyTopic = "YOUR_NTFY_TOPIC";

function getTimestamp() {
  return new Date().toISOString();
}

app.get("/", (req, res) => {
  res.send("Server running");
});

app.get("/request", async (req, res) => {
  try {
    await axios.get(LINK);
    await axios.post(`https://ntfy.sh/${ntfyTopic}`, LINK);
    console.log(`[${getTimestamp()}]: LINK IS PUBLISHED!`);
  } catch (error) {
    if (error.response && error.response.status === 404) {
      console.log(`[${getTimestamp()}]: 404 LINK NOT PUBLISHED YET`);
    } else {
      console.log(`[${getTimestamp()}]: ERROR DURING REQUEST: ${error}`);
    }
    res.send("Working...");
  }
});

app.listen(3000);
```

3. Replace `"YOUR_TARGET_URL"` with the actual URL you want to track.
4. Replace `"YOUR_NTFY_TOPIC"` with the topic name you subscribed to in the `ntfy` app.

### Running the Tracker

1. Start the server by running:

```bash
node index.js
```

2. Open your browser and visit `http://localhost:3000/request`.
   - If the link is not published yet, you won’t receive a notification.
   - If the link is available, you’ll receive a notification in the `ntfy` app.

## Deploying the Tracker for Free

To make your tracker run online, deploy it on Vercel.

### Configure Vercel Deployment

1. Create a `vercel.json` file in your project folder with the following content:

```json
{
  "version": 2,
  "builds": [
    {
      "src": "index.js",
      "use": "@vercel/node",
      "config": { "includeFiles": ["dist/**"] }
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "index.js"
    }
  ]
}
```

2. Upload your project to GitHub.
3. Visit [Vercel](https://vercel.com) and sign in.
4. Click on **Add New > Project** and select your GitHub repository.
5. Click **Deploy**.
6. Once the deployment is complete, visit `https://YOURWEBSITE.XYZ/request` to check if the link is published.

## Automating the Process

Instead of manually visiting the `/request` route, you can automate the tracking process.

### Using a Cron Job

1. Visit [cron-job.org](https://cron-job.org) and create an account.
2. Click on **Create Cron Job**.
3. Enter a title and paste your deployed Vercel URL with the `/request` route.
   - Example: `https://foo-tracker.vercel.app/request`
4. Set the execution schedule to **Every 1 minute(s)**.
5. Click **Create**.

Now, your tracker will automatically check the link every minute, and you will receive a notification when the link is published.

## Summary

In this guide, we:

- Built a simple Node.js tracker using Express and Axios.
- Set up mobile notifications with `ntfy`.
- Deployed the tracker for free using Vercel.
- Automated the process using `cron-job.org`.

This method is useful for tracking published links, announcements, or any webpage updates efficiently.

Thank you :)
