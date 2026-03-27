# Protecting Any Python Script with Kaida Shield

Kaida Shield works with any Python script or command. No framework required.

## The Simplest Setup

```
pip install kaida-shield
kaida shield run python my_script.py
```

That's it. Kaida monitors your script at the OS level.

## With a Policy

1. Open the dashboard: `kaida ui`
2. Go to **Rules** tab
3. Describe what your script does in plain English
4. Run with the policy:
   ```
   kaida shield run --policy my-policy python my_script.py
   ```

## Works With Anything

Kaida doesn't care what language or framework you use. It monitors at the operating system level:

```
kaida shield run python my_bot.py
kaida shield run node my_agent.js
kaida shield run ./my_binary
```

If it runs as a process, Kaida can monitor it.
