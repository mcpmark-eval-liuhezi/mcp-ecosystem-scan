# MCP Ecosystem Snapshot

Live scan of the Model Context Protocol (MCP) ecosystem on GitHub, performed via the GitHub Search API on **2026-10-22**. Everything below is recorded exactly as the searches returned it at scan time — nothing is filled in from prior knowledge.

---

## Top repositories

**Search:** repositories matching `model context protocol` — the API reported **31,857** total matches. The top five results, in the order the search API returned them (relevance order, not star order):

| # | Repository | Stars | Description (as reported) |
|---|------------|-------|---------------------------|
| 1 | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) | 91,486 | Model Context Protocol Servers |
| 2 | [modelcontextprotocol/modelcontextprotocol](https://github.com/modelcontextprotocol/modelcontextprotocol) | 9,510 | Specification and documentation for the Model Context Protocol |
| 3 | [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk) | 24,643 | The official Python SDK for Model Context Protocol servers and clients |
| 4 | [wong2/awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) | 4,379 | A curated list of Model Context Protocol (MCP) servers |
| 5 | [modelcontextprotocol/typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk) | 13,639 | The official TypeScript SDK for Model Context Protocol servers and clients |

**Observations from the returned data:**

- The official `modelcontextprotocol` organization owns three of the top five results (`servers`, the spec repo, and both SDKs), with `wong2/awesome-mcp-servers` the only third-party entry in the top five.
- `modelcontextprotocol/servers` dominates at 91,486 stars — roughly 10x the spec repo (9,510) and 3.7x the Python SDK (24,643). The TypeScript SDK (13,639) also outranks the spec repo itself.
- Reference server implementations, not the specification, are the community's main gravitational center.
- All five are active: `updated_at` timestamps returned by the API fell on the scan date itself (2026-10-22).

---

## Where the MCP Python SDK shows up in real code

**Search 1:** `modelcontextprotocol language:python` — the API reported **36,352** total matches. Representative repositories and file paths returned by the search:

| Repository | File path | Link |
|------------|-----------|------|
| snmendoza01/InfoSys_Hackathon | `q.py` | [view](https://github.com/snmendoza01/InfoSys_Hackathon/blob/d8718665e538512ef22d8e1e7bc0edd41f255d3b/q.py) |
| ShreyasTembhare/MCP---Audio-Transcriber | `mcp.py` | [view](https://github.com/ShreyasTembhare/MCP---Audio-Transcriber/blob/d96d1c0744ed9d7642fa3753659a20dbf250b89b/mcp.py) |
| ManashNepal/AskPDF | `MCP.py` | [view](https://github.com/ManashNepal/AskPDF/blob/3bbcab6a9ee22e1b726e32801e822b0bc0391a66/MCP.py) |
| yashwatwani/story-writer-ai | `mcp.py` | [view](https://github.com/yashwatwani/story-writer-ai/blob/bc94eceb2934d5314ac5a8f257141028f4955f7f/mcp.py) |
| malfet/fluffy-succotash | `claude-mcp.py` | [view](https://github.com/malfet/fluffy-succotash/blob/f85b1162e7f6da102541be3e481a76932edac37c/claude-mcp.py) |
| Minkov/python_meetup_april_rag_mcp | `app/mcp.py` | [view](https://github.com/Minkov/python_meetup_april_rag_mcp/blob/4a669cb9de68e2597f0e2e485182ee904ed2d850/app/mcp.py) |

**Search 2:** `"from mcp import" language:python` — the API reported **82,688** total matches. Representative results:

| Repository | File path | Repo description (as reported) |
|------------|-----------|------|
| mikegc-aws/amazon-bedrock-mcp | `app.py` | Demo of Anthropic's open source MCP used with Amazon Bedrock Converse API |
| mihirrd/ollama-mcp-client | `main.py` | MCP client for local ollama models |

**Observations from the returned data:**

- ~36K Python files reference `modelcontextprotocol` directly, and ~83K use the `from mcp import ...` import pattern — real-world adoption of the SDK is broad and appears to be growing in both client and server roles.
- Usage skews toward standalone, single-file MCP entry points (`mcp.py`, `q.py`, `app.py`, `main.py`) at a project's root, suggesting many integrations are bootstrapped as small, self-contained servers rather than embedded into larger package structures.
- Matched projects span hackathon entries, demo repos, meet-up samples, and hobbyist tools (PDF Q&A chatbots, audio transcribers, story writers) alongside infrastructure-style demos (Amazon Bedrock integration, a local Ollama MCP client).

---

## Open-issue themes

**Search:** open issues mentioning MCP. A plain `MCP is:open` query reported **381,464** total matches; a narrower `MCP model context protocol is:open` query reported **28,988**. Sample of titles and numbers actually returned:

- `T3-P4-Auto-n8n/zapateria-paso-firme` **#136** — "Servidor MCP (MCP Server Trigger)"
- `Lowpower/pigo` **#373** — "mcp: add the /mcp screen and pigo mcp commands"
- `Lowpower/pigo` **#371** — "mcp: load servers from user and project config and connect lazily"
- `Lowpower/pigo` **#372** — "mcp: sign in with OAuth, CIMD, and step-up scopes"
- `InnerScopeHearing/otchealth-mcp-server` **#258** — "fleet-medic alert log v2 (successor to #21)" (2,500 comments — at GitHub's comment cap)
- `vyavahareyash/total-recall` **#9** — "Local Model Context Protocol (MCP) Server"
- `mcpmark-eval-liuhezi/agent-standards-watch` **#2** — "Research: Model Context Protocol (MCP)"

**Themes visible in the returned issues:**

1. **Client-side integration effort is the dominant workstream.** A cluster of issues in one tool (`Lowpower/pigo` #371, #372, #373) breaks MCP adoption into exactly the seams our team would hit: config loading and lazy connection, transport lifecycle (stdio / streamable HTTP), OAuth sign-in, and surfacing MCP servers and tools in a TUI/CLI. Notably, MCP functionality is being treated as expected, built-in behavior for an agent CLI.
2. **Authorization is the hard part.** The OAuth issue (#372) alone covers dynamic client registration, Client ID Metadata Documents (CIMD), issuer checks, and per-server credentials — a recurring complexity tax for HTTP-transport MCP servers.
3. **Operational scale problems.** `InnerScopeHearing/otchealth-mcp-server` #258 is a machine-written log channel that hit GitHub's 2,500-comment cap and forced a "successor issue" rollover — teams are using issues as MCP-driven automation channels and running into platform limits.
4. **Domain-specific local servers are a common build pattern.** `vyavahareyash/total-recall` #9 specifies a local-first, `127.0.0.1`-bound, token-authenticated MCP server with a deliberately reduced tool surface (read-only search, reply staging, no autonomous send tools) — reflecting security-conscious scoping of what agents may do.
5. **Protocol governance research.** One returned research note (`agent-standards-watch` #2) records that MCP is maintained under the Agentic AI Foundation (Linux Foundation) with lead maintainers David Soria Parra and Den Delimarsky, that the current spec version is `2026-07-28`, and that its headline change is a move to a stateless protocol core (retiring the `initialize` handshake and `Mcp-Session-Id` header) alongside cacheable list results, a formal extensions framework, and a 12-month deprecation policy. It also cites ~500M monthly SDK downloads across Tier 1 SDKs.
6. **Search noise is real.** The broad `MCP is:open` query also surfaced issues that merely contain the string "MCP" somewhere but have nothing to do with the protocol (e.g. `microsoft/vscode` #519, a workbench font-size request). Any issue mining for MCP should use the narrower "MCP model context protocol" phrasing or filter by repository/topic.

---

*Snapshot generated for the team's quarterly MCP ecosystem evaluation. See the tracking issues in this repository for per-project adoption checks.*
