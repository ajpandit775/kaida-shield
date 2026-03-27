# Protecting CrewAI Agents with Kaida Shield

CrewAI runs multiple agents working together. Kaida Shield monitors the entire crew.

## Quick Setup

1. Install both:
   ```
   pip install kaida-shield crewai
   ```

2. Run your crew through Kaida:
   ```
   kaida shield run python my_crew.py
   ```

Kaida monitors all agents in the crew as a single process. Any agent that goes off-script triggers a freeze.

## Policy Tips for CrewAI

Since CrewAI runs multiple agents, your policy should cover all of them:

*"My crew has a researcher that searches the web, a writer that saves articles to ~/content/, and a reviewer that checks grammar. None of them should access social media or download executables."*

## Monitoring the Crew

Use `kaida ui` to watch the Activity tab. You'll see network connections, file writes, and process activity from all agents in real time.
