# Getting Telegram Notifications from Kaida

Get instant alerts on your phone when Kaida freezes or kills a bot.

## Step 1: Create a Telegram Bot

1. Open Telegram and search for **@BotFather**
2. Send `/newbot`
3. Choose a name (e.g., "My Kaida Alerts")
4. Choose a username (e.g., "my_kaida_alerts_bot")
5. BotFather gives you a **token** — save this

## Step 2: Get Your Chat ID

1. Send any message to your new bot
2. Run this in your terminal:
   ```
   kaida setup telegram
   ```
3. Enter your bot token when asked
4. Kaida discovers your chat ID automatically and sends a test message

## Step 3: Verify

You should see a test message from your bot in Telegram. From now on, every FREEZE or KILL event sends you an alert with:
- What happened
- Which domain/file/command was involved
- What action Kaida took

## Alternative: Dashboard Setup

You can also configure Telegram from the dashboard:
1. `kaida ui`
2. Go to **Help** tab
3. Find **Telegram Notifications**
4. Enter your bot token and chat ID
5. Click **Save** and **Send Test**
