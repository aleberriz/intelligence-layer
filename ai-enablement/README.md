# AI Enablement

Patterns for connecting AI agents to analytics infrastructure — and for building the infrastructure worth connecting to.

The semantic layer is becoming an API for AI agents. The Model Context Protocol (MCP) is the transport layer. The practical work is: (1) designing an Omni model that answers well when queried by an AI, and (2) building skills and prompts that make that querying reliable and useful.

---

## Subdirectories

### `mcp/`
MCP server architecture and integration patterns. Covers:
- What MCP resources, tools, and prompts are at the spec level
- How Omni's MCP server works and how to configure it
- Differences in how Claude Desktop, Cursor, ChatGPT, and Codex consume the same MCP server
- Authentication patterns and multi-client considerations

Key reference: [Model Context Protocol spec](https://modelcontextprotocol.io) | [Omni MCP docs](https://docs.omni.co/ai/mcp/)

### `skills/`
AI skill design — reusable, composable instructions that guide an AI agent through a repeatable analytics workflow. Covers Omni-style skills and general patterns applicable across tools.

Key reference: [omni-claude-skills](https://github.com/exploreomni/omni-claude-skills)

### `prompts/`
Curated and tested prompt templates for analytics contexts — querying a semantic layer, interpreting experiment results, drafting metric definitions, summarizing cohort behavior. Each prompt includes the context it was designed for and known failure modes.

---

## Design Principle

AI-readiness is a modeling concern, not a prompting concern. A semantic layer with good `ai_context` fields, clear `synonyms`, well-scoped topics, and descriptive measure definitions will outperform one with elaborate prompts wrapped around a poorly modeled layer. Fix the model first.
