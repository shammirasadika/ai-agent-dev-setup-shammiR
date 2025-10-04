# Verification — Proof of MCP Functionality

This file lists the evidence required and what is already captured in this repository. Some items require interactive steps (screenshots, authenticated GitHub MCP use) that must be produced locally; instructions are provided.

1) Screenshot of each MCP server working in Claude Desktop
- What I can provide: I ran HTTP checks from PowerShell showing both discovered endpoints are reachable and accept POST/GET (OPTIONS returned 204 and Allow: GET, HEAD, OPTIONS, POST). See `connection-test.md` for the exact command outputs.
- What you must provide: Claude Desktop screenshots showing the MCPs connected and responding. Suggested names and folder:

  

2) Example of using GitHub MCP server to interact with your repository
- Status: No GitHub MCP URL was found in the repository. I added a placeholder entry in `mcp-servers-list.md` and instructions for adding a GitHub MCP.
- To demonstrate this, follow these steps locally:

  1. Run or configure a GitHub MCP service that exposes an MCP endpoint for repo actions (issue create, PR comment). Add its URL to `mcp-configs/claude_desktop_config.json` under a key like `github-mcp`.
  2. In Claude Desktop, connect to the `github-mcp` server.
  3. From the Claude UI or via `npx mcp-remote <url>`, send a test payload to create an issue or list repo contents. Capture the request and the successful response.
  4. Save the request/response pair to `assets/verification-screenshots/github-mcp-example.txt` or a screenshot `assets/verification-screenshots/claude_github.png`.

Example minimal POST (adjust headers/auth as required):

```powershell
$body = '{"type":"createIssue","repo":"<owner>/<repo>","title":"Test from MCP"}' ;
Invoke-RestMethod -Method Post -Uri 'https://your-github-mcp.example.com/api/mcp' -Body $body -ContentType 'application/json' -Headers @{ Authorization = 'Bearer <token>' }
```

3) Git commit history showing proper version control workflow
- I cannot run git commands on your machine for you, but you can generate a git-history artifact locally with the following command and commit it to the repo:

```powershell
git log --oneline --graph --decorate -n 200 > verification/git-history.txt
git add verification/git-history.txt; git commit -m "Add verification: git history"; git push
```

- Suggested file: `verification/git-history.txt` (commit and push this file so reviewers can see the history).

4) What I already added to this repository
- `mcp-servers-list.md` — documented discovered MCP servers and placeholders.
- `connection-test.md` — contains the exact PowerShell commands and outputs I ran showing OPTIONS/GET behaviors for the two discovered endpoints.

5) Limits and next steps
- I cannot take or upload UI screenshots or run Claude Desktop locally from this environment. Please follow the screenshot steps above and add the files in `assets/verification-screenshots/`.
- If you provide a GitHub MCP URL and any required tokens (or run the example POST locally and paste the results here), I can help format the evidence and update `VERIFICATION.md` with the inserted outputs.

If you'd like, I can also create a small PowerShell script to automate the local verification steps (POST tests and capturing outputs) — tell me if you want that and whether authentication should be read from environment variables.
