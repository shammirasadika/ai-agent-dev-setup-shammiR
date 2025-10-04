## MCP Servers List

This document lists the MCP servers referenced in this workspace and how to connect to them.

1) Rolldice
- Name: Rolldice
- URL: https://rolldice.ausbizconsulting.com.au/api/mcp
- How it's launched: Configured in `mcp-configs/claude_desktop_config.json` to use `npx mcp-remote <url>`.
- Notes: Server accepts HTTP methods GET, POST, OPTIONS. No auth information found in repository. Contact your infra owner if credentials or API keys are required.

2) Bootcamp AI Agent (ai-assist)
- Name: Bootcamp RAG / Tech Bootcamp Consultations
- URL: https://ai-assist.ausbizconsulting.com.au/api/mcp
- How it's launched: Configured in `mcp-configs/claude_desktop_config.json` to use `npx mcp-remote <url>`.
- Notes: Same base URL used for two server entries (`bootcamp-rag` and `tech-bootcamp-consultations`). Server accepts HTTP methods GET, POST, OPTIONS. No auth information found in repository.

3) Calendar Booking (placeholder)
- Name: Calendar Booking
- URL: (not found in repository)
- How to add: Provide the MCP URL and add an entry to `mcp-configs/claude_desktop_config.json` similar to the existing entries:

```
"calendar-booking": {
  "command": "npx",
  "args": ["-y","mcp-remote","https://your-calendar.example.com/api/mcp"]
}
```

- Notes: If the server requires authentication, add secure storage for API keys (do not commit secrets to the repo). See `connection-test.md` for testing guidance.

4) GitHub (placeholder)
- Name: GitHub MCP (placeholder)
- URL: (not found in repository)
- How to add: If you run an MCP fronting GitHub actions or a custom GitHub MCP, add it to `mcp-configs/claude_desktop_config.json` with the URL.

---

Assumptions and next steps
- The workspace currently includes three MCP entries (two unique URLs). No Calendar Booking or GitHub MCP URLs were found; placeholders were added above with instructions.
- If any of these servers require special headers or API keys, update the configs and store secrets securely (environment variables or local-only config not checked into git).
