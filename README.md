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
