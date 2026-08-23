# MCP Setup Guide — Connecting Claude to Jira
## Vibetesting in 2026 — Course Resources

Connects Claude Desktop to your Jira project using Claude's **built-in Atlassian connector** —
no API token, no config files, no terminal. You connect once and Claude can create tickets,
read project data, and generate reports directly.

**Time to complete:** ~3 minutes
**Requires:** Claude Desktop app (not the browser version), and your **TechShop Testing** Jira
project (created in the setup clip).

---

## Step 1 — Have your Jira project ready

You already created a Jira site and a **TechShop Testing** project (key **TECH**) in the setup
clip. Make sure you can sign in to it in your browser — that is the account the connector will
link to. Nothing else to prepare: **you do not need to create an API token.**

---

## Step 2 — Connect Atlassian in Claude Desktop

1. Open **Claude Desktop**.
2. Go to **Settings → Connectors**.
3. Search for **Atlassian** (the connector is **Atlassian Rovo**).
4. Click **Connect**. A browser window opens — **sign in to your Atlassian account** and
   **approve access** to your Jira site.

That's the whole setup. No token to paste, no config file to edit, no OS-specific steps.

> If you have more than one Atlassian site, the connector may ask which one to use — pick the
> site that has your **TechShop Testing** project.

---

## Step 3 — Test the connection

Open a **new chat** and send:

```
List all projects in my Jira account.
```

Claude should respond with your project list, including your **TECH** project. The connection
is active and working.

---

## Troubleshooting

**Don't see Atlassian under Connectors:**
- Update Claude Desktop to the latest version, then reopen Settings → Connectors.

**Connected but "0 projects" or "no tools available":**
- Make sure you authorised the **same Atlassian account** that owns your TechShop Testing site.
- Start a **new chat** after connecting — an older chat won't have the connector attached.

**Wrong or empty results:**
- If you have multiple Atlassian sites, re-check that the connector is pointed at the site with
  your **TECH** project.

---

## What Claude can do with this connection

- Create Jira tickets (Task, Bug issue types)
- Read all tickets in a project or sprint
- Update ticket status, add comments, set priority
- Generate test reports from sprint data

You will use this in Sections 6, 8, and 10.
