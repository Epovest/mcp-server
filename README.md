# Epovest MCP server

With Epovest, businesses make AIs recommend them.

This is the official MCP server for [Epovest](https://epovest.com). It is hosted: there is nothing
to install and no package to build. Point your MCP client at the endpoint below and your assistant
gets the same 43 tools the app itself is built on.

```
https://mcp.epovest.com/mcp
```

- **Transport**: Streamable HTTP
- **Authentication**: OAuth 2.1 with PKCE, or an API key as a Bearer token
- **Official registry**: [`com.epovest/ai-visibility`](https://registry.modelcontextprotocol.io)
- **Agent documentation**: [epovest.com/docs/api.md](https://epovest.com/docs/api.md)

## What your assistant can do

Epovest measures how AI assistants answer the questions your market asks, which sources they cite,
and gives the levers that shape those answers. Every tool below acts on the account that owns the
API key.

**Canon**, the reference text a brand keeps stable and versioned: `list_projects`, `create_project`,
`update_project_canon`.

**Tracking**, the measurement itself: `list_trackers`, `create_tracker`, `update_tracker`,
`start_tracker`, `pause_tracker`, `get_results` for the score series, `get_responses` for the raw
engine answers, plus `list_keyword_discoveries`, `accept_keyword_discovery`,
`dismiss_keyword_discovery` and `restore_keyword_discovery` for the questions the measurement
suggests next.

**Surfaces**, the pages a brand writes itself: `list_surfaces`, `create_surface`, `update_surface`,
`tick_surface_checklist`, `mark_surface_aligned`, `delete_surface`, `restore_surface`.

**Atlas**, the map of the sources AI assistants listen to: `list_sources`, `get_source`.

**Corroborations**, where a third party speaks about the brand: `list_corroborations`,
`create_corroboration`, `update_corroboration`, `archive_corroboration`, plus
`list_corroboration_candidates` and `dismiss_corroboration_candidate`, which derive candidates from
what the engines already returned.

**Logbook**, the dated record of what was done, read against the curves: `get_logbook`,
`create_logbook_entry`, `update_logbook_entry`, `delete_logbook_entry`.

**Quests**, the action queue: `list_quests`, `create_quest`, `update_quest`, `complete_quest`,
`dismiss_quest`.

**Account**: `get_credits` reads the prepaid balance, `topup_credits` returns a hosted payment link
for the user to open. Nothing is ever charged without them.

**Support**, served even when data access has lapsed: `contact_support`, `list_support_threads`,
`get_support_thread`. A human answers in the thread.

## Design notes for agents

- Measurement runs on **prepaid credits**: `create_tracker` prepares a tracker as a draft, and
  `start_tracker` launches its measurement against the balance. Read the balance first with
  `get_credits`.
- Every removal is **reversible and its inverse is in the same surface**: archive and unarchive,
  delete and restore, complete and reopen. Each gesture states a state rather than toggling a
  switch, so a replay is safe in both directions.
- Errors come back as the JSON envelope of the REST API v1: same codes, same meaning, whatever the
  transport.
- Pricing lives on [epovest.com/pricing](https://epovest.com/pricing).

## Company

Epovest is published by Simafri. Terms and privacy: [epovest.com/en/terms](https://epovest.com/en/terms),
[epovest.com/en/privacy](https://epovest.com/en/privacy).
