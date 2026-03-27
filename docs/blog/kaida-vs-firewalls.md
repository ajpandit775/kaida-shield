# Why Traditional Firewalls Don't Work for AI Agents

Firewalls block or allow based on rules: this IP is allowed, that port is blocked, this domain is permitted. They work great for traditional software.

AI agents break this model.

## Agents Need Broad Permissions

A useful AI agent needs to access the web, read files, run commands, and talk to APIs. If you lock it down with a traditional firewall, it can't do its job. If you open it up, it can do anything.

## The Action Looks Fine. The Pattern Doesn't.

A firewall sees: "Process 1234 connected to api.example.com on port 443." That's an allowed connection. Approved.

But what the firewall doesn't see: Process 1234 connected to api.example.com 500 times in the last minute, downloading every customer record in the database. The individual connection is fine. The pattern is an exfiltration attack.

## Behavioral Monitoring: The Missing Layer

Behavioral monitoring watches patterns over time:
- Is the agent making an unusual number of requests?
- Is it accessing files outside its normal scope?
- Is it stuck in a loop, burning tokens?
- Is it connecting to domains it's never contacted before?

This is what Kaida Shield does. It doesn't replace your firewall — it adds a layer that firewalls can't provide.

## Try It

```
pip install kaida-shield
kaida quickstart
```

See behavioral monitoring in action. The bot follows its rules, then goes off-script, and Kaida freezes it.
