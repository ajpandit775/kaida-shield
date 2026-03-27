# Protecting LangChain Agents with Kaida Shield

LangChain agents can search the web, execute code, and access APIs. Kaida Shield monitors what they actually do.

## Quick Setup

1. Install both:
   ```
   pip install kaida-shield langchain
   ```

2. Create your LangChain script as normal (e.g., `my_agent.py`)

3. Run it through Kaida:
   ```
   kaida shield run python my_agent.py
   ```

That's it. Kaida wraps the process and monitors everything at the OS level. No code changes needed in your LangChain script.

## Creating a Policy

Open the dashboard:
```
kaida ui
```

Go to **Rules** → describe your agent:

*"My LangChain agent searches Google for product reviews and saves summaries to ~/reviews/output.csv"*

Kaida generates YAML rules automatically. Select the policy when you run your agent.

## Example

```
kaida shield run --policy web-researcher python my_agent.py
```

Your agent runs normally. If it tries to access a domain not in the policy, Kaida freezes it and notifies you.
