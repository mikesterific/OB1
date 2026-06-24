# Archive: open-brain-vm-supabase-setup

## Task Summary

Set up the OpenBrain VM as the operational host for OB1 and deployed the Open Brain remote MCP service to Supabase. The completed system exposes `open-brain-mcp` as a Supabase Edge Function backed by Supabase/Postgres with pgvector and OpenRouter embeddings.

## Implementation Details

- Established reliable SSH access to the VM through a dedicated Ed25519 key and `openbrain` SSH alias.
- Renamed the Linux hostname from `openclaw` to `openbrain` without reinstalling the OS.
- Cloned the OB1 repository on the VM at `~/git/OB1`.
- Linked Supabase CLI to project `dxgppqznnwxwavvuwhza`.
- Deployed the `open-brain-mcp` Edge Function.
- Set required function secrets for Supabase, OpenRouter, and MCP access.
- Applied the base database schema, including `thoughts`, `upsert_thought`, and `match_thoughts`.
- Verified MCP transport, auth, tool registration, database access, semantic search, and capture.
- Captured the first memory: "Open Brain was created today, June 23, 2026."

## Verification Results

- `initialize`: passed with protocol version `2024-11-05`.
- `tools/list`: passed with six tools registered.
- `thought_stats`: passed and reached Supabase.
- `search_thoughts`: passed after the base schema was applied.
- `capture_thought`: passed and wrote the first memory.

## Files Changed

- `memory-bank/tasks.md`
- `memory-bank/progress.md`
- `memory-bank/activeContext.md`
- `memory-bank/systemPatterns.md`
- `memory-bank/reflection/reflection-open-brain-vm-supabase-setup.md`
- `memory-bank/archive/archive-open-brain-vm-supabase-setup.md`

## Lessons Learned

- Inspect local SSH client configuration early when key auth fails; client-side overrides can defeat correct server-side setup.
- Use dedicated VM keys and aliases for operational hosts instead of reusing expired, certificate-backed, or passphrase-protected personal keys.
- Treat Supabase Edge Function deployment as separate from database readiness; semantic search requires the schema and RPCs to be present.
- Verify remote MCP services in layers: transport/auth, tool list, read-only database call, semantic search, then write/capture.
- Treat MCP URLs containing `?key=...` as credentials and keep them out of repo files.

## Related Documents

- `memory-bank/reflection/reflection-open-brain-vm-supabase-setup.md`
- `memory-bank/systemPatterns.md`
