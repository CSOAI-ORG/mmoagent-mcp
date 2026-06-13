# mmoagent-mcp

<p align="center">
  <img src="https://img.shields.io/badge/MEOK-GAMING-purple?style=for-the-badge&logo=gamepad" />
  <img src="https://img.shields.io/badge/Cross--Game-6%20MMOs-blue?style=for-the-badge&logo=web" />
  <img src="https://img.shields.io/badge/SOV3-Sovereign%20Data-green?style=for-the-badge&logo=lock" />
  <img src="https://img.shields.io/badge/MCP-Compatible-blue?style=for-the-badge&logo=protocol" />
</p>

**The AI Agent for the $200B Gaming Economy.** Cross-game market intelligence, unified currency conversion, player portfolio tracking, and intelligent farming optimization across World of Warcraft, Final Fantasy XIV, EVE Online, Old School RuneScape, Path of Exile, and Diablo IV.

> Part of the **MEOK GAMING** suite by [MEOK AI Labs](https://meok.ai) / [CSOAI-ORG](https://github.com/CSOAI-ORG).

---

## The $200B Opportunity

| Game | API Status | Economy Size | MCP Gap |
|------|-----------|-------------|---------|
| **World of Warcraft** | Retail: ✅ Classic: ⚠️ | £100M+ RMT | ❌ None existed |
| **Final Fantasy XIV** | XIVAPI + Universalis | £50M+ RMT | ❌ None existed |
| **EVE Online** | ESI API (excellent) | £10M+ monthly | ❌ None existed |
| **Old School RuneScape** | Wiki API | £20M+ RMT | ❌ None existed |
| **Path of Exile** | Official Trade API | £30M+ RMT | ❌ None existed |
| **Diablo IV** | Limited API | £10M+ RMT | ❌ None existed |

**14,000+ MCP servers. Zero gaming.** This changes now.

---

## Features

| Tool | Description |
|------|-------------|
| `mmo_unified_market_search` | Search ALL game marketplaces simultaneously |
| `mmo_economy_dashboard` | Macro-economic dashboard — inflation, volume, health scores |
| `mmo_gold_conversion` | Convert currency across games using real-money equivalents |
| `mmo_player_portfolio` | Aggregate assets across all connected MMOs |
| `mmo_meta_trend_analysis` | Cross-game meta trend detection |
| `mmo_intelligent_farming` | "I have 2 hours, tell me where to farm across all my games" |

---

## Currency Conversion Reference

| Game | Currency | USD per 1M | Rate Source |
|------|----------|-----------|-------------|
| WoW | Gold | $77.25 | WoW Token ($20 = ~259k) |
| FFXIV | Gil | $20.00 | Mog Station estimate |
| EVE Online | ISK | $0.004 | PLEX ($20 = ~500M) |
| OSRS | GP | $0.20 | Bond ($2 = ~10M) |
| Path of Exile | Chaos Orb | $0.01 | Divine Orb conversion |
| Diablo IV | Platinum | $1.00 | In-game store |

---

## Installation

```bash
npx -y @smithery/cli install @csoai-org/mmoagent-mcp
```

Or add to your MCP client config:
```json
{
  "mcpServers": {
    "mmoagent": {
      "command": "npx",
      "args": ["-y", "@csoai-org/mmoagent-mcp"]
    }
  }
}
```

---

## Example: "I Have 2 Hours"

```json
{
  "tool": "mmo_intelligent_farming",
  "arguments": {
    "player_games": ["wow", "osrs", "ffxiv"],
    "time_minutes": 120,
    "target_value_usd": 15
  }
}
```

Response:
```json
{
  "optimal_choice": {
    "game": "Old School RuneScape",
    "activity": "Vorkath kills",
    "expected_yield_usd": "18.50",
    "roi_score": 9.2
  }
}
```

---

## SOV3: Sovereign Gaming Data

This server is **SOV3-enabled**: your gaming intelligence is yours. No platform can lock you in, delete your data, or monetize your patterns without consent. Full data portability across the MEOK gaming mesh.

---

## License

MIT

---

<p align="center">
  <b>MEOK GAMING</b> · One Agent. Six Worlds. Infinite Gold.<br/>
  <a href="https://meok.ai">meok.ai</a> · <a href="https://github.com/CSOAI-ORG">CSOAI-ORG</a>
</p>
