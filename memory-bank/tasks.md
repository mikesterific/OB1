# Tasks

## open-brain-vm-supabase-setup

Status: Completed and archived

Complexity: Level 3

Goal: Set up the OpenBrain VM and deploy the Open Brain remote MCP function backed by Supabase.

Completed:
- Restored passwordless SSH access to the VM using a dedicated Ed25519 key and the `openbrain` SSH alias.
- Renamed the Linux host from `openclaw` to `openbrain`.
- Cloned the OB1 repository to `~/git/OB1` on the VM.
- Logged in and linked the Supabase CLI to project `dxgppqznnwxwavvuwhza`.
- Deployed the `open-brain-mcp` Supabase Edge Function.
- Set required function secrets.
- Applied the base database schema, including `thoughts`, `upsert_thought`, and `match_thoughts`.
- Verified MCP initialization, tool registration, Supabase access, semantic search, and capture.
- Added the first memory: "Open Brain was created today, June 23, 2026."

Reflection:
- Created: `memory-bank/reflection/reflection-open-brain-vm-supabase-setup.md`

Archive:
- Created: `memory-bank/archive/archive-open-brain-vm-supabase-setup.md`
