+++
title = "Xpnss"
date = "2026-08-05"
weight = 1

[taxonomies]
tags = ["flutter", "dart", "isar"]

[extra]
local_image = "xpnss.png"
+++

Local-first expense tracker for people who don't want their financial data sitting on someone else's server. No accounts, no cloud sync, no telemetry — everything lives in an on-device Isar database.

## Dark mode

<div style="display:flex; gap:8px; overflow-x:auto;">
  <img src="/screenshots/xpnss/d_home.png" alt="Home" width="200">
  <img src="/screenshots/xpnss/d_insights.png" alt="Insights" width="200">
  <img src="/screenshots/xpnss/d_settings.png" alt="Settings" width="200">
</div>

## Light mode

<div style="display:flex; gap:8px; overflow-x:auto;">
  <img src="/screenshots/xpnss/l_home.png" alt="Home" width="200">
  <img src="/screenshots/xpnss/l_insights.png" alt="Insights" width="200">
  <img src="/screenshots/xpnss/l_settings.png" alt="Settings" width="200">
</div>

## Why it exists

Most expense trackers make money selling your spending data or lock features behind a subscription. Xpnss does neither — it's built on the assumption that your bank transactions are nobody's business but yours.

## Features

- **Fully offline** — works with no internet connection, ever
- **No account required** — open the app, start tracking
- **Insights** — spending breakdowns without sending a single byte off-device
- **Fast** — Isar's local storage means no loading spinners waiting on a server

## Details

| | |
|---|---|
| **Platform** | Android · iOS |
| **Stack** | Flutter, Isar |
| **Status** | In dev |
| **Website** | [xpnss.com](https://xpnss.com) |
| **Download** | [APK (Android)](https://xpnss.com/download/xpnss.apk) |
