# MCP Setup Guide — Connecting Claude to Jira
## Vibetesting in 2026 — Course Resources

Connects Claude Desktop to your Jira project. Once done, Claude can create tickets, read
project data, and generate reports directly — no copy-paste required.

**Time to complete:** ~5 minutes
**Requires:** Claude Desktop app (not the browser version), and any AI coding agent you
installed earlier in this section (GitHub Copilot, Cursor, Windsurf, Antigravity, or Claude
Code — any one works).

> **Why we do it this way.** The MCP config lives in a different place on macOS than on
> Windows, and it needs `uv` installed and the JSON merged correctly. That is exactly the kind
> of fiddly, OS-specific chore an AI agent does perfectly — so instead of following different
> steps per platform, you hand it to the agent and it does the right thing for *your* machine.

---

## Step 1 — Generate your Jira API token (do this yourself)

This is the one step you must do by hand, because the token is a secret the agent should never
generate or guess:

1. Go to **id.atlassian.com/manage-profile/security/api-tokens**
2. Click **Create API token**, name it `MCP Course`, click **Create**
3. **Copy the token immediately** — you cannot view it again after closing

Keep the token somewhere safe for the next step. Never commit it to GitHub or paste it into a
public chat.

---

## Step 2 — Let an agent set up MCP for you

Open **any** AI agent you installed in this section (Copilot Chat, Cursor, Windsurf,
Antigravity, or Claude Code — pick whichever you like). Paste the prompt below, filling in the
three values in brackets, and let it run. It will detect your operating system, install `uv` if
needed, and write the Claude Desktop config to the correct location — merging with any existing
config instead of overwriting it.

```text
Set up the Atlassian (Jira) MCP server for my Claude Desktop app on THIS machine. Detect
whether I'm on macOS or Windows and do the right thing for my OS. Steps:

1. Make sure `uv` is installed (it provides `uvx`). If `uvx --version` fails, install uv:
   - macOS: curl -LsSf https://astral.sh/uv/install.sh | sh   (then ensure ~/.local/bin is on PATH)
   - Windows: powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

2. Locate the Claude Desktop config file:
   - macOS: ~/Library/Application Support/Claude/claude_desktop_config.json
   - Windows: %APPDATA%\Claude\claude_desktop_config.json
   Create the folder and file if they don't exist.

3. Add this MCP server to the config. If the file already has an "mcpServers" object, MERGE
   this entry into it — do NOT overwrite the whole file. Use these values:
     JIRA_URL      = [https://YOUR-SITE.atlassian.net]
     JIRA_USERNAME = [your@email.com]
     JIRA_API_TOKEN = [the token you created in Step 1]

   The entry to add:
   "atlassian": {
     "command": "uvx",
     "args": ["mcp-atlassian"],
     "env": {
       "JIRA_URL": "...",
       "JIRA_USERNAME": "...",
       "JIRA_API_TOKEN": "..."
     }
   }

4. Validate that the final file is valid JSON, show me the file path you wrote and the config
   (with the token masked), and tell me to fully quit and reopen Claude Desktop.

Do not print my API token back in plain text. If anything fails, tell me exactly what and how
to fix it.
```

A reference version of the config lives at
[`claude_desktop_config_template.json`](claude_desktop_config_template.json) if you want to
see the shape, or hand it to the agent.

---

## Step 3 — Restart Claude Desktop and test

1. **Fully quit** Claude Desktop (right-click the tray/menu-bar icon → **Quit** — don't just
   close the window), then reopen it.
2. Open a new conversation and send:

```
List all projects in my Jira account.
```

Claude should respond with your project list, including your **TECH** project. MCP is active
and working.

---

## Troubleshooting

**0 projects or "no tools available":**
- Ask the agent to re-check the config: `JIRA_URL` must include `https://` and end with
  `.atlassian.net`, the token must be complete, and the JSON must be valid.
- Make sure you **fully quit** Claude Desktop (not just closed the window) before reopening.

**`uvx` not found after install:**
- Ask the agent to ensure `uv`'s install location is on your PATH, then fully quit and reopen
  Claude Desktop.

**The agent can't reach the Claude config folder** (some sandboxed setups):
- Ask it to instead **output the finished JSON and the exact destination path** for your OS,
  then create the file yourself in that folder (macOS: `~/Library/Application Support/Claude/`,
  Windows: `%APPDATA%\Claude\`) and rename it to `claude_desktop_config.json`.

---

## What Claude can do with this connection

- Create Jira tickets (Task, Bug issue types)
- Read all tickets in a project or sprint
- Update ticket status, add comments, set priority
- Generate test reports from sprint data

You will use this in Sections 6, 8, and 10.
