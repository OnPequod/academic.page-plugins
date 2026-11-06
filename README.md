# Academic.page plugins

Plugins that connect Claude and ChatGPT to [Academic.page](https://academic.page).
Once connected, the agent can read your site, add publications, talks,
projects, and courses, and check your publication details against their
published records.

## Install

**Claude** (desktop app): open Customize, then Plugins. Select Add, then Add
marketplace, then Add from a repository, and enter `OnPequod/academic.page-plugins`.
Under Discover, add Academic.page. In Claude Code, run:

```
claude plugin marketplace add OnPequod/academic.page-plugins
claude plugin install academic-page@academic-page
```

**ChatGPT and Codex**: in the ChatGPT desktop app, open Customize, then
Plugins. Select Add, then Add a marketplace, and enter
`OnPequod/academic.page-plugins`. In Codex, run:

```
codex plugin marketplace add OnPequod/academic.page-plugins
codex plugin add academic-page@academic-page
codex mcp login academic-page
```

The first time the agent uses Academic.page, it opens academic.page in your
browser. Sign in, choose a site and what the agent may do, and select
Connect. The [guide to connecting an AI app](https://academic.page/manual/ai-apps)
explains each access level. Connecting an agent needs a site on Pro or Pro+.

## What's inside

`plugins/academic-page` connects to the Academic.page MCP server at
`https://academic.page/mcp`. It holds a Claude manifest
(`.claude-plugin/plugin.json`) and a Codex manifest (`.codex-plugin/plugin.json`).
Both read the server from `.mcp.json`. The marketplace files are
`.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json`.
