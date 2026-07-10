---
description: Start the local live-server dev server with auto-reload on port 8080.
allowed-tools: [Shell, Read, Await, CallMcpTool]
---

# Build Live Server

Start the project's local development server with live reload.

## Goal

Serve this static prototype at `http://127.0.0.1:8080` and auto-refresh the browser when `index.html` changes.

## Steps

1. Work from the project root.
2. Check whether a dev server is already running on port 8080:

```bash
lsof -i :8080
```

3. If port 8080 is occupied by a non-`live-server` process (for example Python), stop it before continuing.
4. If `live-server` is already serving this project on port 8080, confirm it is healthy and skip restart.
5. Install dependencies if `node_modules/` is missing:

```bash
npm install
```

6. Start the dev server in the background:

```bash
npm run dev
```

7. Verify the server is up and injecting live reload:

```bash
curl -s -o /dev/null -w "%{http_code}" http://127.0.0.1:8080/
curl -s http://127.0.0.1:8080/ | rg "live-server|WebSocket"
```

8. Open `http://127.0.0.1:8080/` in the browser.

## Expected Result

Tell the user:

- The local URL: `http://127.0.0.1:8080/`
- That saving `index.html` should refresh the page automatically
- How to restart later: `npm run dev`
- If port 8080 is busy: `lsof -i :8080`

## Notes

- Use `npm run dev`, not `python3 -m http.server`.
- `live-server` must bind to port 8080. If it falls back to another port, fix the port conflict and restart.
- Do not commit unless the user asks.
