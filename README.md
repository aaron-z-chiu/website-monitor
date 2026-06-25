# Website Monitor

[![Website monitor](https://github.com/aaron-z-chiu/website-monitor/actions/workflows/website-monitor.yml/badge.svg)](https://github.com/aaron-z-chiu/website-monitor/actions/workflows/website-monitor.yml)

A lightweight uptime and TLS monitor for my personal website:

- <https://zecqiu.com>

The monitor runs automatically with GitHub Actions and sends Telegram alerts when potential website issues are detected.

## What It Checks

This workflow checks several common failure cases:

- The website cannot be reached.
- HTTPS/TLS handshake fails.
- The HTTP status code is abnormal, such as `4xx`, `5xx`, or Cloudflare `52x`.
- The page loads but the expected keyword is missing.
- The public TLS certificate is close to expiry.
- The GitHub Pages origin check fails when bypassing Cloudflare.

This is useful for detecting issues such as invalid SSL certificates, Cloudflare 526 errors, GitHub Pages certificate problems, or accidental broken deployments.

## How It Works

The workflow is defined in:

```text
.github/workflows/website-monitor.yml
```

It runs on a schedule and can also be triggered manually from the GitHub Actions page.

Current monitoring target:

```text
https://zecqiu.com
```

Current content keyword check:

```text
Zecheng
```

If any check fails, the workflow sends an alert message to Telegram using a Telegram bot.

## Required Secrets

The following GitHub Actions secrets are required:

```text
TELEGRAM_BOT_TOKEN
TELEGRAM_CHAT_ID
```

These values are stored in GitHub repository secrets and are not committed to this repository.

## Manual Test

To manually run the monitor:

1. Open the repository on GitHub.
2. Go to **Actions**.
3. Select **Website monitor**.
4. Click **Run workflow**.

If the website is healthy, the workflow should succeed without sending a Telegram message.

To test whether Telegram alerts work, temporarily change the expected keyword in the workflow to a string that does not exist on the website, then run the workflow manually. After confirming that the Telegram alert is received, change the keyword back.

## Notes

* The schedule uses UTC time.
* The monitor is designed for simple personal website monitoring, not for high-availability production systems.
* Telegram secrets should never be written directly into the workflow file or README.



