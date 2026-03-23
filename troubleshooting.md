# OpenClaw Android: Troubleshooting Guide

If things aren't working, you probably skipped a step. Here's how to fix the most common issues.

---

## Problem 1: Termux Randomly Closes or Crashes

**Why it happens:** Your phone thinks Termux is draining the battery, so Android kills it in the background.

**The Fix:**

1. Go to **Android Settings → Apps → Termux → Battery** and set it to **Unrestricted** (or turn off battery optimization).
2. Every time you open Termux, run:
   ```bash
   termux-wake-lock
   ```

---

## Problem 2: "Command Not Found" Errors

**Why it happens:** Either a typo, or the basic packages weren't installed first.

**The Fix:** Stop rushing. Run these in order:

```bash
pkg update -y && pkg upgrade -y
```
```bash
pkg install -y curl
```

Then try your command again.

---

## Problem 3: The Telegram Bot Is Ignoring Me

**Why it happens:** Either Termux closed in the background, or you pasted the wrong API keys during onboarding.

**The Fix:**

1. Check that Termux is actually open and running on your phone. If it's closed, the bot is dead.
2. If Termux is running, you likely entered the wrong keys. Re-run onboarding:
   ```bash
   openclaw onboard
   ```
   Take your time. Paste the exact Anthropic/Gemini API key and the exact Telegram Bot token — no extra spaces.

---

## Problem 4: Can't Open the Web Dashboard / "Site Can't Be Reached"

**Why it happens:** The gateway isn't running, or you typed the local address wrong in your browser.

**The Fix:**

1. Make sure you actually started the gateway in Termux:
   ```bash
   openclaw gateway
   ```
2. Look at the output — it will give you a link like `http://localhost:18789`.
3. **Do not type it manually.** Copy it and paste it directly into Chrome or Brave.

---

## Problem 5: "Permission Denied" When Reading or Writing Files

**Why it happens:** OpenClaw doesn't have access to your phone's storage.

**The Fix:** Run this in Termux:

```bash
termux-setup-storage
```

A popup will appear — tap **Allow**. If you tap Deny, nothing will work until you do this correctly.
