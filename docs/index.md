# Loran's AI Agent Lab

Built on the ZeroClaw framework.

## Why I built this
In the AI era, I want to own infrastructure, not just 
use tools. This lab documents how I designed, deployed, 
and secured a multi-agent system from scratch on a live VPS.

## Current lead agent: Nova
Nova is my Content Intelligence Officer — a YouTube 
specialist that finds the most relevant videos on chosen 
topics and delivers tight summaries.

- Searches YouTube via a custom MCP server (YouTube via Apify's YouTube scraper through a custom MCP server)
- Delivers top 3 videos with 3-bullet verdict-first summaries to Telegram
- Deep-dive analysis available on request
- Topics managed via /topics commands
- Delegates tasks automatically via ZeroClaw's routing system

## Architecture
ZeroClaw acts as the manager — receives commands via 
Telegram, delegates YouTube work to Nova, renders 
results. Nova focuses purely on content analysis.

## Navigation
- [Nova's Identity](02-Agents/Nova/IDENTITY.md)
- [Nova's Soul](02-Agents/Nova/SOUL.md)
- [Troubleshooting Journal](03-Journal/fixing-errors.md)
- [Showcase](04-Showcase/best-results.md)

