# System Patterns

## Remote MCP Deployment Pattern

Open Brain MCP servers should run as remote Supabase Edge Functions, not local desktop MCP servers. The validated setup path is:

1. Deploy the Edge Function from `server/index.ts`.
2. Set runtime secrets in Supabase.
3. Apply the base database schema before semantic search testing.
4. Verify with MCP `initialize`, `tools/list`, read-only database calls, semantic search, then capture.

## Secret Handling Pattern

Connector URLs may include `MCP_ACCESS_KEY`, so treat them as secrets.

- Prefer user/global MCP configuration over repo config.
- Do not store access keys in `.cursor/rules`, committed files, docs, or task notes.
- If a key appears in terminal logs or chat context, rotate it unless it is intentionally disposable.

## Smoke Test Pattern

Use staged verification:

1. `initialize` confirms transport and auth.
2. `tools/list` confirms the MCP server builds correctly.
3. `thought_stats` confirms Supabase service role access.
4. `search_thoughts` confirms OpenRouter embeddings and `match_thoughts`.
5. `capture_thought` confirms write path and embedding persistence.
