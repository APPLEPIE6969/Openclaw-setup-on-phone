# The Ultimate OpenClaw Android Setup Guide

Setting up OpenClaw on your phone isn't magic, but if you mess up the basics, nothing works. Here is the exact step-by-step to get this AI agent running locally on your device.

---

## Phase 1: Prep Your Phone

> **Do not skip this.** Android will aggressively kill the background process if you don't.

1. Go to **Android Settings → Battery** (or **Apps**).
2. Turn off **Battery Optimization** for Termux (we'll install this next).
3. Keep your phone plugged in, or enable **Stay Awake** in Developer Options while working through this guide.

---

## Phase 2: Get Termux — The Right Way

> ⚠️ **Do NOT download Termux from the Google Play Store.** It's completely dead and broken.

1. Open your phone's browser and go to **[f-droid.org](https://f-droid.org)**.
2. Download the F-Droid app, install it, and search for **Termux**.
3. Install Termux and open it.
4. Update everything so it doesn't crash later:
   ```bash
   pkg update -y && pkg upgrade -y
   ```
5. Grant storage access:
   ```bash
   termux-setup-storage
   ```
   Tap **Allow** when the popup appears.

---

## Phase 3: Install OpenClaw

We're using the single-command method — no manual Ubuntu proot configuration needed.

1. Install `curl`:
   ```bash
   pkg install -y curl
   ```
2. Run the install script — copy and paste this exact line into Termux:
   ```bash
   curl -sL myopenclawhub.com/install | bash && source ~/.bashrc
   ```
3. Wait **5–10 minutes**. Grab a coffee. Let it do its thing. A Wi-Fi connection is strongly recommended.

---

## Phase 4: Onboarding — The Brains

Now you need to give it an AI model and connect it to a chat app.

1. Start the onboarding wizard:
   ```bash
   openclaw onboard
   ```
   If it asks to install a **system daemon**, say **NO** — Android doesn't play well with that.

2. **Choose your AI provider.** Anthropic Claude or Google Gemini are the easiest options right now. Paste your API key when prompted.

3. **Choose a channel.** When asked where you want to chat with it, select **Telegram**.

4. **Create your Telegram bot:**
   - Open Telegram and search for **@BotFather**.
   - Type `/newbot`, give your bot a name, and copy the **HTTP API Token** it returns.
   - Paste that token into the Termux prompt.

5. **Lock down your bot:**
   - Message **@userinfobot** on Telegram to get your personal numerical User ID.
   - Paste that ID into Termux so random people can't hijack your bot.

---

## Phase 5: Start the Engine

1. Keep Termux awake in the background:
   ```bash
   termux-wake-lock
   ```
2. Start the gateway:
   ```bash
   openclaw gateway
   ```
3. It will output a local address (e.g. `localhost:18789`). Open that in your phone's browser to access the **control dashboard**.

4. If the dashboard asks for an auth token, open a **new Termux session** (swipe in from the left edge of the screen) and run:
   ```bash
   openclaw gateway status
   ```
   Copy the token and paste it into the dashboard.

---

## You're Done! 🎉

Head to Telegram, say hi to your bot, and watch it get to work. Just leave Termux running in the background — don't swipe it away.
