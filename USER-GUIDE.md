# Quota Monitor — User Guide

Quota Monitor shows what is left of your **GitHub Copilot**, **Claude Code** and **Codex** limits, in Visual Studio Code's status bar, in a side panel and on a dashboard.

*Not affiliated with or endorsed by Microsoft, GitHub, Anthropic or OpenAI. Quota Monitor reads each tool through the sign-ins you already have on your computer — Claude Code's, Codex's and Visual Studio Code's GitHub sign-in — and never asks for a password.*

---

## 1. Getting started

1. Install Quota Monitor. Its icon appears in the activity bar on the left.
2. Soon after, the status bar shows a short tag for every tool it found, for example `Cl 64% · Cx 82% · Co 35%` (the first Claude Code reading can take a minute or two). `Cl` is Claude Code, `Cx` is Codex, `Co` is GitHub Copilot. **Each number is what is left** of that tool's lowest limit, not what you have used.
3. Quota Monitor finds Claude Code and Codex automatically when they are installed and signed in. GitHub Copilot needs one click: see section 3.
4. If no tool has numbers yet (none is installed, signed in or connected), the status bar says **AI limits: connect**. Click it to see what each tool needs.

## 2. Where the numbers appear

- **Status bar.** Click the tag to open the quick menu (dashboard, refresh, settings, user guide). Hover over it to see every limit and what is left of it (with Pro, also when it resets).
- **Side panel.** Click Quota Monitor's icon in the activity bar. It shows the same limits, one row per tool, and the buttons to connect a tool.
- **Dashboard.** Command Palette (`Ctrl+Shift+P`, on a Mac `Cmd+Shift+P`) → **Quota Monitor: Open Visual Dashboard**. It has three tabs:
  - **Overview:** a card for every limit, with what is left (and, with Pro, when it resets).
  - **Analytics:** your usage history and, with Pro, trends and a day × hour heatmap.
  - **Settings:** everything in section 6.
- **In a web browser (Pro):** **Quota Monitor: Open Dashboard in Web Browser (Pro)** opens the same dashboard in your browser, for example on a second monitor. It runs only on your own computer (`127.0.0.1`).

Drag a card by its `⋮⋮` handle, give it one of six colours, or hide it with its ×; hidden cards come back from the **Hidden** row. Hiding a card changes only what you see, never your limits.

## 3. The three tools

### Claude Code

Quota Monitor runs `claude -p /usage` on your computer. These are the same numbers Claude Code shows with `/usage`. It does not start a conversation and does not use any of your limit.

- Claude Code is read every **15 minutes** by default (you can choose 30 or 60) while you are using Visual Studio Code. When a Claude Code limit has less than 20% left, it is read every 5 minutes; below 5%, every 3 minutes.
- When you open the dashboard and the last reading is more than 2 minutes old, Claude Code is read again.
- Claude Code does not always report a 5-hour limit. If you see only weekly limits, that is what Claude Code reported at that moment.

### Codex

Quota Monitor asks the Codex program on your computer (`codex app-server`) for your account type and rate limits, and nothing else. Codex is read every 5 minutes by default (2–30 minutes in the settings).

### GitHub Copilot

GitHub Copilot is read from GitHub, so it needs your permission once:

1. In the side panel, click **Connect with GitHub**.
2. Visual Studio Code asks whether Quota Monitor may use your GitHub sign-in. Click **Allow**. If you are not signed in to GitHub in Visual Studio Code yet, it first opens your browser so you can sign in to GitHub.
3. Your Copilot usage appears within a few seconds. After that it is read every 10 minutes, or at your Codex interval if that is longer.

Quota Monitor asks only for permission to read your email address (or your public profile, if Visual Studio Code already has that) and reads only your Copilot usage. It never asks for access to your code.

**Another way:** if you would rather not share the sign-in, run **Quota Monitor: Use a GitHub Token for Copilot Usage** and paste a fine-grained personal access token with the user permission **Plan: read**. It is kept in Visual Studio Code's secret storage and sent only to `api.github.com`. **Quota Monitor: Remove the GitHub Token for Copilot Usage** deletes it.

### When a tool shows no numbers

Each tool's row says why, in plain words:

| The row says | What to do |
| :--- | :--- |
| not installed | Install the tool, or switch it off in **Settings → Tools** if you do not use it |
| not signed in | Sign in to the tool itself (for example run `claude` or `codex` once in a terminal) |
| not connected (Copilot) | Click **Connect with GitHub** (section 3) |
| could not read (timed out, no connection …) | Quota Monitor tries again by itself, first after a minute or two and then less often, and keeps the last numbers, labelled as old |

**Quota Monitor: Refresh Data Now** reads again immediately (Claude Code at most once every 2 minutes, the other tools once a minute).

However many Visual Studio Code windows you have open, only one of them reads; the others show its numbers.

## 4. Free and Pro

**Free, always:** the status bar, the side panel and dashboard, all three tools, the bar styles, card colours and themes, alerts inside the editor when a limit runs low or resets, and 24 hours of history.

**Pro adds:**

- **Reset countdown and clock** on every limit, and the **run-out forecast**: at your current pace, will this limit run out before it resets?
- **Reserve Guard:** a warning when, at your current pace, a limit would fall below the reserve you set (20% by default).
- **Switch hint:** when one tool runs low, the alert names another tool you use that still has plenty left, for example "Codex still has 82%."
- **90 days of history**, trend lines and a day × hour heatmap.
- **Phone and chat notifications** through ntfy.sh, Telegram, Discord or Slack (section 5).
- **Remind me at reset** (the 🔔 on a card) and a **morning summary** once a day between 06:00 and 11:59.
- **Weekly report** in HTML and Markdown, one table per tool.
- **Sounds** when a limit resets or runs low.
- **Export** your history as CSV or JSON (up to 90 days).
- **Terminal status file and shell snippets** (section 7), and the **browser view** (section 2).

### The 14-day trial

Every new installation gets **14 days of full Pro**, with no card and no sign-up. The 14 days start when Quota Monitor shows your **first reading**, not when you install it, so a day spent setting up does not count. The side panel shows how many days are left.

When 3 days of the trial are left, Quota Monitor tells you once. When the trial ends, Pro features stop and the free part keeps working. **Your history is kept.** Anything older than 24 hours is hidden, not deleted, and comes back the moment you unlock Pro.

### Buying Pro

Pro is a **one-time payment of €9.99** — no subscription. Not happy? Full refund within 30 days.

1. Click **Unlock Pro — €9.99** in the side panel or on the dashboard, or run **Quota Monitor: Unlock Pro (€9.99 one-time)**.
2. Visual Studio Code first asks **"Do you want Code to open the external website?"** and shows the address `buy.polar.sh`. This question is Visual Studio Code's own safety check and appears for every extension that opens a web page. Click **Open**.
3. Pay on the Polar page. Polar is the shop that sells Quota Monitor Pro and handles the payment; Quota Monitor never sees your card.
4. Your license key arrives by email. It starts with `QMV-`.
5. Run **Quota Monitor: Enter Pro License Key** and paste the key. Pro is on at once.

One key works in up to 5 editors, for example on 5 computers. **Quota Monitor: Remove Pro License Key** frees this computer's place, so you can use the key on another computer. A key from another extension (for example one starting with `PRO-`) does not unlock Quota Monitor.

## 5. Phone and chat notifications (Pro)

Open **Settings → Phone and chat notifications** on the dashboard.

- **ntfy.sh (easiest, no account):** install the free ntfy app, add the topic name the dashboard shows (or scan the QR code on Android), then click **Save and send a test notification**. ntfy.sh topics are public, so do not share the random name with anyone.
- **Telegram:** create a bot with @BotFather, set its token with **Quota Monitor: Set Telegram Bot Token (Pro)**, write to your bot once, and enter your chat ID. The dashboard's help (ⓘ) walks you through each step.
- **Discord or Slack:** paste an incoming webhook URL.

**Quota Monitor: Send Test Notification (Pro)** checks every channel you have set up.

## 6. Settings

On the dashboard's **Settings** tab, or in Visual Studio Code's settings under **Quota Monitor**:

| Setting | What it does |
| :--- | :--- |
| Interface language | Automatic, English or Estonian. Automatic follows the editor's language, or the system's language when the editor is in English. |
| Theme | Night, day, or follow the editor |
| Status bar display mode | All tools, the one limit with the least left, or a single tool |
| Progress bar style | Eight styles, coloured or monochrome |
| Warning and critical thresholds | The status bar turns yellow when a limit has this percentage left or less (30% by default), and red at 15% |
| Tools | Switch off a tool you never use |
| How often the tools are read | Codex and GitHub Copilot 2–30 minutes (Copilot never more often than every 10); Claude Code 15, 30 or 60 minutes |
| Sounds, morning summary | On or off (Pro) |
| Forecast warning, reserve | Warn when, at your current pace, a limit will run out within this many minutes and before it resets (25 by default); the reserve that Reserve Guard keeps (20%) |
| History | How many days of history to keep (90 by default) |

## 7. Terminal status file (Pro)

After every reading Quota Monitor writes what is left to `~/.quota-cockpit/status.json` (numbers and times only). **Quota Monitor: Terminal Snippets (Pro)** gives you ready-made lines for zsh, Starship and tmux on macOS and Linux, and for PowerShell and Starship on Windows, so your shell prompt can show your limits.

## 8. Your data

On your computer:

- the history, in Visual Studio Code's storage for this extension;
- the folder `~/.quota-cockpit/`: the latest reading, shared between windows, and with Pro the terminal status file;
- your Pro license key, and a GitHub token or Telegram bot token if you set one, in Visual Studio Code's secret storage.

Over the network, only:

- **GitHub** (`api.github.com`): your Copilot usage, after you connect Copilot;
- **Claude Code and Codex** fetch your limits from Anthropic and OpenAI themselves, with their own sign-in, as they do when you use them;
- **Polar** (`api.polar.sh`): your license key, if you entered one — to check it when you enter it and once a day after that, and to free its place when you remove it;
- **ntfy.sh, Telegram, Discord, Slack:** only the notifications you set up;
- **Open VSX:** a check for a newer version of Quota Monitor.

Nothing is sent to us: no usage numbers, no files, no account details. This version sends no error reports. The history stores a short code for each account instead of your email address.

## 9. Help

- Something looks wrong? **Quota Monitor: Refresh Data Now**, then look at the tool's row in the side panel: it says what is missing.
- Write to **support@nordicmoonlight.com**. Tell us your operating system, your Visual Studio Code version and what the tool's row says.
