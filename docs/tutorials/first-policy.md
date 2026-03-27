# Writing Your First Kaida Policy

Kaida policies are written in plain English. You describe what your bot should do, and Kaida generates the rules.

## Step 1: Open the Dashboard

```
kaida ui
```

## Step 2: Go to the Rules Tab

Click **Rules** in the top navigation.

## Step 3: Describe Your Bot

In the text box, write what your bot does. Be specific about:
- Which websites it should access
- Which files/folders it should read or write
- What it should NOT do

### Good Example
*"My bot checks Indeed.com and LinkedIn for software engineer jobs in Virginia, saves results to ~/Documents/jobs.csv, and sends me a summary email through Gmail."*

### Too Vague
*"My bot finds jobs."*

## Step 4: Generate Rules

Click **Generate Rules**. Kaida creates a YAML policy with:
- Allowed domains (indeed.com, linkedin.com, gmail.com)
- Allowed file paths (~/Documents/jobs.csv)
- Blocked patterns (dangerous commands)
- Anomaly detection thresholds

## Step 5: Use Your Policy

Select the policy on the **Home** tab and click **Start Bot With Protection**.

## Tips

- Start with a restrictive policy and add permissions as needed
- Use **Supervised mode** for the first few runs
- The first freeze is normal — it means Kaida is working
