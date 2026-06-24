# Reflection: open-brain-vm-supabase-setup

## Summary

Completed the OpenBrain VM setup and brought the Open Brain remote MCP service online. The final system uses a Supabase Edge Function (`open-brain-mcp`), Supabase/Postgres with pgvector, OpenRouter embeddings, and the VM as the operational setup host.

The deployment was verified through MCP health checks, tool registration, database access, semantic search, and a successful memory capture.

## What Worked Well

- SSH troubleshooting improved once the local SSH config was inspected. The original config explicitly disabled public key auth for the VM, which explained why server-side key changes did not help.
- Creating a dedicated `openbrain` Ed25519 key removed ambiguity from expired certificates and old passphrase-protected keys.
- Renaming the VM hostname in place avoided a Linux reinstall and preserved the existing setup.
- Using `~/git/OB1` on the VM kept the repo in a predictable user-owned location.
- Persisting the Supabase access token on the VM resolved the repeated CLI login issue for non-interactive deploy commands.
- The MCP smoke-test sequence made failure boundaries clear: auth and transport passed first, then database schema issues surfaced cleanly.
- Applying the base Supabase schema fixed the missing `match_thoughts` RPC and confirmed that the Edge Function itself was already healthy.

## Challenges Faced

- The initial SSH failure had multiple overlapping causes: a mistyped IP address, old/expired key material, passphrase prompts, and a local SSH config override.
- `ssh-copy-id` and manual `authorized_keys` checks were misleading until the local client config was corrected.
- Supabase CLI login appeared successful but did not satisfy all deploy/list commands in the VM's non-interactive shell context.
- The Edge Function could deploy before the database schema was fully ready, so early MCP health checks passed while semantic search failed.
- Secret handling became a visible risk once access keys and Supabase token-like values appeared in terminal or project-file context.

## Lessons Learned

- When SSH keys appear correct on the server, inspect `~/.ssh/config` early. Client-side overrides can silently defeat public key auth.
- For VM automation, use a dedicated key and alias instead of reusing personal or work keys with certificates and expiration policies.
- Supabase Edge Function deployment success does not prove the database contract is ready. Always test the RPC functions the MCP server depends on.
- A read-only smoke test should precede write tests. It verifies auth, tools, and schema without mutating memory.
- Treat MCP connector URLs as credentials when they contain `?key=...`.

## Future Recommendations

- Add a repo-local, non-secret smoke-test script that reads the MCP key from an environment variable or private local file.
- Document a CLI-first setup path for the base Supabase schema so future VM installs do not rely only on dashboard copy/paste.
- Add an explicit post-deploy checklist: secrets, schema, `initialize`, `tools/list`, `thought_stats`, `search_thoughts`, `capture_thought`.
- Rotate any key that was copied into chat, terminal logs, or project files unless it was created as a disposable test key.
- Keep Memory Bank docs local unless the maintainer explicitly wants to commit them.

## Verification

- MCP `initialize`: passed.
- MCP `tools/list`: passed.
- Supabase-backed `thought_stats`: passed.
- Semantic `search_thoughts`: passed after applying schema.
- `capture_thought`: passed.
- First memory captured: "Open Brain was created today, June 23, 2026."
