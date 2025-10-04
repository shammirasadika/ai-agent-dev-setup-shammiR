# MCP Connection Tests

This file records the connection tests performed against the MCP endpoints discovered in the workspace. All commands were run from Windows PowerShell (powershell.exe).

## Commands used

1) Simple GET (used to show server behavior for GET requests)

PowerShell command used:

```
Invoke-WebRequest -Uri 'https://ai-assist.ausbizconsulting.com.au/api/mcp' -UseBasicParsing -TimeoutSec 15
```

Observed output (truncated):

```
ERROR: The remote server returned an error: (405) Method Not Allowed.
```

2) OPTIONS request (used to capture allowed methods and CORS headers)

PowerShell command used:

```
Invoke-WebRequest -Method Options -Uri 'https://ai-assist.ausbizconsulting.com.au/api/mcp' -UseBasicParsing -TimeoutSec 15
```

Observed output (key lines):

```
Status: 204 No Content
Allow: GET, HEAD, OPTIONS, POST
Access-Control-Allow-Origin:
```

3) Rolldice GET

PowerShell command used:

```
Invoke-WebRequest -Uri 'https://rolldice.ausbizconsulting.com.au/api/mcp' -UseBasicParsing -TimeoutSec 15
```

Observed output (truncated):

```
ERROR: The remote server returned an error: (405) Method Not Allowed.
```

4) Rolldice OPTIONS

PowerShell command used:

```
Invoke-WebRequest -Method Options -Uri 'https://rolldice.ausbizconsulting.com.au/api/mcp' -UseBasicParsing -TimeoutSec 15
```

Observed output (key lines):

```
Status: 204 No Content
Allow: GET, HEAD, OPTIONS, POST
Access-Control-Allow-Origin:
```

## Interpretation & next steps
- Both endpoints are reachable over HTTPS and return 204 for OPTIONS with Allow headers showing GET and POST are supported. This indicates the MCP HTTP endpoints are up and responding, but GET without required parameters returned 405 (Method Not Allowed). Use POST with the expected MCP JSON payloads when testing actual MCP behavior.
- No authentication tokens or keys were found in the repository. If the servers require auth, obtain credentials from the project owner and use them in the request (e.g., Authorization header or API key).
- For deeper testing, run a POST request with a minimal MCP-compliant message payload or use the `npx mcp-remote <url>` command configured in `mcp-configs/claude_desktop_config.json`.

Example POST test (adjust headers/payload as required):

```
$body = '{"type":"ping"}' ; Invoke-RestMethod -Method Post -Uri 'https://ai-assist.ausbizconsulting.com.au/api/mcp' -Body $body -ContentType 'application/json'
```

Replace payload and add authentication headers if required.
