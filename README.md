# ELDRICK MCP Server

<img src="assets/icon-512.png" alt="ELDRICK" width="96" align="right">

ELDRICK is a hosted golf club fitting MCP server. It fits drivers, fairway
woods, hybrids, irons and wedges from a golfer's handedness and club or ball
speed, and matches every spec to real heads, shafts and grips. It can also
search, compare and score clubs from the ELDRICK catalog. Putters aren't
supported.

Built on 100,000+ fittings.

This repository is the public listing for the server: connection steps, the
tool list and the registry metadata. The server itself is hosted by ELDRICK
and its source is not published here.

| | |
|---|---|
| URL | `https://api.eldrick.com/mcp` |
| Transport | Streamable HTTP (remote only) |
| Auth | OAuth 2.1 with PKCE, client ID metadata documents and dynamic client registration, or a developer API key sent as `Authorization: Bearer eld_...` |
| Registry name | `com.eldrick.api/fitting` |
| Server card | https://api.eldrick.com/mcp/server-card |
| Docs | https://api.eldrick.com/connect and https://api.eldrick.com/docs |
| Pricing | Every ELDRICK account includes 10 fittings a month. Searching, comparing, scoring and store links don't use one. |

## Connect

Any MCP client that supports remote servers can add ELDRICK by URL. The
first time you connect, sign in with your email and the 6-digit code ELDRICK
sends. A new email gets an account.

**Claude (claude.ai, Desktop, mobile).** Settings, then Connectors, then
Add custom connector. Name it ELDRICK, paste `https://api.eldrick.com/mcp`,
choose Connect and sign in.

**Claude Code.**

```sh
claude mcp add --transport http eldrick https://api.eldrick.com/mcp
```

Then run `/mcp`, pick `eldrick` and sign in.

**ChatGPT (Plus, Pro, Business, Enterprise, Edu).** Go to chatgpt.com/plugins,
choose + then Add custom MCP server, paste the URL, pick OAuth, then Create.

**Gemini CLI.**

```sh
gemini mcp add --transport http eldrick https://api.eldrick.com/mcp
```

Then run `/mcp auth eldrick`. There is also a Gemini CLI extension:
https://github.com/chadwittman/eldrick-gemini-extension

**Cursor** (`~/.cursor/mcp.json`):

```json
{ "mcpServers": { "eldrick": { "url": "https://api.eldrick.com/mcp" } } }
```

**VS Code** (`.vscode/mcp.json`):

```json
{ "servers": { "eldrick": { "type": "http", "url": "https://api.eldrick.com/mcp" } } }
```

**Windsurf** (`mcp_config.json`):

```json
{ "mcpServers": { "eldrick": { "serverUrl": "https://api.eldrick.com/mcp" } } }
```

**Perplexity, Le Chat, Grok, Microsoft Copilot Studio, Meta Muse.** Add a
custom or remote connector with the same URL and choose OAuth. Steps for each
client are at https://api.eldrick.com/connect.

**Clients without OAuth.** Create an API key in the ELDRICK dashboard and send
it as `Authorization: Bearer eld_...`. Keep keys in environment variables,
never in prompts or code.

## Tools

| Tool | What it does |
|---|---|
| `analyze_fitting` | Fits a driver, fairway wood, hybrid, set of irons or wedges from handedness and swing or ball speed, plus anything else known (height, wrist-to-floor, handicap, launch, spin, attack angle, carry, usual miss). Returns loft, shaft flex and weight, length, lie, swing weight and head profile, plus bounce and gapping for wedges. Uses one fitting. |
| `get_fitting` | Returns a saved fitting by its fitting ID. |
| `search_clubs` | Searches the catalog by club type, brand, head category, price, hand or keywords. |
| `get_club` | Shows one club's lofts, stock and upgrade shafts, grips, lengths and lies. |
| `compare_clubs` | Puts 2 to 4 clubs side by side and lists what differs. |
| `score_clubs` | Ranks clubs for one golfer, 0 to 100, with the reasons. |
| `build_store_link` | Links to a club on store.eldrick.com with the fitted build listed. Opens the product page, never a checkout. |
| `get_grip_size` | Recommends a grip size and extra wraps from hand and finger length. |
| `analyze_bag_gapping` | Checks the distance gaps across a bag and suggests what to add, drop or change. |
| `find_fitter` | Finds club fitters near a ZIP code. |
| `check_key_status` | Developer API keys: fittings left this month and the reset date. |
| `get_api_status` | Developer API keys: the API, engine and ruleset versions that answered. |

## Example prompts

- "Fit me for a driver. I'm right-handed, 6'0", swing about 98 mph with a fade, launch 14° and spin 3000 rpm."
- "Fit my wedges. Right-handed, 75 mph wedge speed, attack angle -5, my pitching wedge is 45 degrees."
- "Show me low-spin drivers under $600 and compare the top two."

## Files

- `server.json`: the Official MCP Registry entry (schema 2025-12-11). The
  live copy is served at https://api.eldrick.com/server.json.
- `glama.json`: maintainers for the Glama listing.
- `assets/icon-512.png`: the ELDRICK icon.

## Links

- Website: https://eldrick.com
- Connect guide: https://api.eldrick.com/connect
- API docs: https://api.eldrick.com/docs
- Privacy: https://api.eldrick.com/privacy
- Terms: https://api.eldrick.com/terms
- Support: https://api.eldrick.com/support (api@eldrick.com)

## License

The text and metadata in this repository are licensed under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The ELDRICK name and
icon are trademarks of ELDRICK and are not covered by that license. The hosted
service is governed by the terms at https://api.eldrick.com/terms.
