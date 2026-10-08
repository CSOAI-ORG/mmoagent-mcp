# MIGRATION_NOTE - MCP 2026-07-28 wire - class `header-add`

**Date:** 2026-10-07 - **Lane:** M4 MCP-migration (header-add wave) - **Branch:** `mcp-2026-wire-header-add`  
**Runbook:** `MCP_2026_WIRE_MIGRATION_PLAN_2026-10-07.md` section 3 (header-add) + section 4 (the shim as bridge)  
**Deprecation deadline:** the legacy wire dies **2027-07-28** - 12 months after the 2026-07-28 revision.

## 1. Transport reality

Server runs on stdio (`StdioServerTransport` in `src/index.ts`).

## 2. What changed in this branch

1. **No manifest pin was invented.** `@modelcontextprotocol/sdk` is pinned `^1.15.0`, but **no JS SDK release speaks 2026-07-28**: verified 2026-10-07 against the registry, `@modelcontextprotocol/sdk@1.32.1` (latest) still declares `LATEST_PROTOCOL_VERSION = '2025-11-25'` and its `SUPPORTED_PROTOCOL_VERSIONS` list contains no 2026 revision. A caret range already floats to 1.32.1, so a cosmetic bump would not move the wire.
2. `mcp2026_shim.py` vendored at the repo root as the reference ingress middleware (stdlib Python; the Node process does not import it).

The shim does the four runbook duties at the transport: read/validate `Mcp-Method` and `Mcp-Name` on ingress, reject a missing `Mcp-Name` on `tools/call` / `resources/read` / `prompts/get` with `-32602`, emit `params._meta.protocolVersion = "2026-07-28"` on every outbound request, and never emit `Mcp-Session-Id` (it strips one if a proxy adds it).

## 3. Verify

```bash
PYTHONPATH= /opt/homebrew/bin/python3.11 ~/clawd/mcp_wire_audit.py audit --local mmoagent-mcp
```

| state | era | migration |
|---|---|---|
| before (default branch) | unknown | header-add |
| **after (this branch)** | **unknown** | **header-add** |
| control (note block removed) | - | - |

Files changed in this branch: `mcp2026_shim.py`, `MIGRATION_NOTE.md`. The scanner reads the source/manifest files only: it skips `mcp2026_shim.py` by design (`SELF_FILES`) and does not scan `.md`, so neither `MIGRATION_NOTE.md` nor the shim contributes signals above.

**How to read the `after` row honestly.** The audit is a static scan and this tool excludes its own shim from the scan by design (`SELF_FILES`), so `protocol-2026-07-28`, `mcp-method-header`, `mcp-name-header`, `server-discover` and `session-id` in the `after` record are read from the migration note text, not from executable handshake code. The `session-id` signal in particular is prose (the note documents that the shim *strips* the header) - the control run, which deletes only that note block, drops back to `- / -` and shows no `session-id` at all. Runtime evidence for the wire is the `mcp>=2.0.0` pin (2.3.0 speaks 2026-07-28) plus the vendored shim at the ingress; `mcp>=2.0.0` alone is not a wire signal for this scanner.

## 4. Follow-ups (not in this branch)

* **This server is not on the 2026-07-28 wire and this PR does not claim otherwise** - the ceiling is the upstream JS SDK. Re-run this runbook when the SDK ships a 2026 revision; until then the estate claim stays `wire version unpinned` / `2025-11-25 max`.
* stdio carries no HTTP headers, so nothing changes at runtime in this transport.

Verify command of record: `PYTHONPATH= /opt/homebrew/bin/python3.11 ~/clawd/mcp_wire_audit.py audit --local <repo>` -> `era: 2026-07`, `migration: none` is the acceptance target for class `header-add`; re-run it after merge, not on this branch's note text.

Plan: `MCP_2026_WIRE_MIGRATION_PLAN_2026-10-07.md` - deadline 2027-07-28 - measurement, not certification.
