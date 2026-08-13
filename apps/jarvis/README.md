# CIPHER Command Deck (JARVIS-style UI)

A single-file, dependency-free HUD for talking to the OpenClaw gateway — parallax starfield, boot sequence, agent fleet cards, and a live chat uplink to the default agent session.

## Serve it

Any static file server works. On the gateway host:

```bash
cd apps/jarvis
python3 -m http.server 8080
# open http://localhost:8080
```

## Link it

Click the status pill (top right) and set:

- **Gateway WS URL** — `ws://127.0.0.1:18789` (default)
- **Gateway token** — `openclaw config get gateway.auth.token`
- **Session key** — `main` (default agent session)

## Notes

- Over plain HTTP the browser cannot do device-key auth (`crypto.subtle` requires a secure context). For loopback use set `gateway.controlUi.allowInsecureAuth: true`; for remote access prefer an HTTPS tunnel (Tailscale Serve, Cloudflare Tunnel) so device auth works.
- The page speaks gateway protocol v3: `connect.challenge` → `connect` → `chat.send` / `chat.abort`, streaming replies via `chat` events.
- Fleet cards mirror the Hermes / Worker / Researcher agent setup; the Worker card lights up on tool events.
