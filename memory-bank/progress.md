# Progress

## 2026-06-23 - Open Brain VM and Supabase Setup

Completed setup of the OpenBrain VM and deployed Open Brain MCP service.

Verified:
- SSH alias `openbrain` reaches the VM.
- VM hostname is `openbrain`.
- OB1 repo exists at `~/git/OB1` on the VM.
- Supabase Edge Function `open-brain-mcp` is active.
- MCP `initialize` returns protocol version `2024-11-05`.
- MCP `tools/list` returns six tools: `search`, `fetch`, `search_thoughts`, `list_thoughts`, `thought_stats`, and `capture_thought`.
- `thought_stats` reaches Supabase successfully.
- `search_thoughts` reaches the OpenRouter embedding path and Supabase `match_thoughts` RPC.
- `capture_thought` successfully wrote the first memory.

Current status:
- Completed and archived.
- Archive: `memory-bank/archive/archive-open-brain-vm-supabase-setup.md`

Risks and follow-up:
- Rotate any access key that was pasted into terminal/chat context if it is not a disposable test key.
- Remove and rotate any Supabase token accidentally stored in project files.
- Prefer user/global MCP configuration for connector URLs that include access keys.
