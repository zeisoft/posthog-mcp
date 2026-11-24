<div align="center">

<img src="assets/cover.png" alt="PostHog through HeyMetra's MCP server" width="100%">

# PostHog &times; HeyMetra

**Events, funnels and retention, asked in plain words.**

PostHog knows what people did. It does not know what it cost, or what it earned. Connect it beside the accounts that do.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.heymetra%2Fheymetra-1f6feb)](https://registry.modelcontextprotocol.io/v0/servers/com.heymetra%2Fheymetra/versions)
[![Transport](https://img.shields.io/badge/transport-Streamable_HTTP-444)](https://modelcontextprotocol.io/)
[![Auth](https://img.shields.io/badge/auth-OAuth_2.1-444)](https://heymetra.com/security/)
[![Connector page](https://img.shields.io/badge/heymetra.com-posthog-1f6feb)](https://heymetra.com/connectors/posthog/)

```
https://mcp.heymetra.com/mcp
```

</div>

---

## Ask it things like

> How many people signed up last week?

> Where do people drop out of the onboarding funnel?

> Which events fired most yesterday?

> What does the saved insight for weekly retention say?

No dashboard, no export, no query language. You ask in the assistant you already use and the answer comes back with the account it came from.

## Connect PostHog

**1. Say whether PostHog is theirs or yours**

PostHog Cloud is the hosted one you sign in to at posthog.com. Choose your own server only if somebody at your company installed PostHog on a machine you run.

> You are not asked which Cloud region you are in. A personal API key belongs to one region and is refused by the other, so HeyMetra asks the key rather than asking you.

**2. If it is your own server, note its address**

The address you open PostHog at, like analytics.acme.com. On PostHog Cloud there is nothing to fill in here, and the box is not shown.

**3. Open Settings → Personal API keys**

It is under your own account menu rather than the project's settings. A personal API key belongs to you, not to one project, and reaches every project you can open.

> PostHog allows ten personal keys per person. Make one for HeyMetra rather than reusing the key in a script: revoking it later then costs nothing else.

**4. Create a key with read scopes**

Choose the scopes rather than granting everything. Reading needs Projects, Insights, Queries and Events, which PostHog lists as `project:read`, `insight:read`, `query:read` and `event:read`. Leave the write scopes off unless you intend to let your assistant propose changes.

> If a scope turns out to be missing, PostHog answers 403 and names the one it wanted, so this is correctable rather than a guess you are stuck with.

**5. Copy the key immediately**

It starts with `phx_` and is shown once. Refreshing the page loses it, and there is no way to read it back; the only remedy is creating another one.

**6. Paste it into HeyMetra and name the connection**

On the Connections screen choose PostHog, paste the key, type the address from step one, and name the connection after the product rather than after PostHog. The key is stored encrypted and never shown again, and HeyMetra checks it works against that address before keeping it.

Watch what you paste:

- Anything starting `phc_` is **a project API key, which is the public one your app ships with and cannot read anything back** and will be refused by name.

The same steps are on the docs page: [PostHog setup guide](https://heymetra.com/docs/posthog/).

## Then add HeyMetra to your assistant

Add HeyMetra once and it is there in every conversation. The address is the same everywhere:

```
https://mcp.heymetra.com/mcp
```

### One command

```bash
npx add-mcp https://mcp.heymetra.com/mcp
```

[`add-mcp`](https://www.npmjs.com/package/add-mcp) is a third-party installer that writes the configuration for Claude Code, Codex, Cursor, Antigravity, VS Code and seventeen other agents. It infers the name from the address, so the server lands as `heymetra`. Run against this endpoint before it was written here.

### Or by hand

<details>
<summary><b>Claude</b> — Settings → Customize → Connectors → Add custom connector</summary>

Paste the address above into Settings → Customize → Connectors → Add custom connector.

_On Team and Enterprise plans, an owner adds the connector for the whole organization under Organization settings → Connectors, and each member then connects to it._

Full walkthrough: [heymetra.com/mcp/claude/](https://heymetra.com/mcp/claude/)
</details>

<details>
<summary><b>ChatGPT</b> — chatgpt.com/plugins → + → Add custom MCP server</summary>

Paste the address above into chatgpt.com/plugins → + → Add custom MCP server.

_Add it on chatgpt.com in a browser, because the mobile app cannot add one. Every ChatGPT plan can, Free included. In a Business, Enterprise or Edu workspace, an admin or owner decides whether members can add custom MCP servers. ChatGPT needs the full address, including /mcp at the end._

Full walkthrough: [heymetra.com/mcp/chatgpt/](https://heymetra.com/mcp/chatgpt/)
</details>

<details>
<summary><b>Grok</b> — grok.com/connectors → New Connector → Custom</summary>

Paste the address above into grok.com/connectors → New Connector → Custom.

_On Grok Business and Enterprise, a team admin has to provision the connector in xAI's cloud console before members can use it._

Full walkthrough: [heymetra.com/mcp/grok/](https://heymetra.com/mcp/grok/)
</details>

<details>
<summary><b>Perplexity</b> — Plugins → Add custom → Connector → Add MCP connector → Remote</summary>

Paste the address above into Plugins → Add custom → Connector → Add MCP connector → Remote.

_In an organization, members can add a custom connector only after an admin turns on Allow members to add custom connectors, which is off by default._

Full walkthrough: [heymetra.com/mcp/perplexity/](https://heymetra.com/mcp/perplexity/)
</details>

<details>
<summary><b>Claude Code</b> — claude mcp add --transport http</summary>

```bash
claude mcp add --transport http heymetra https://mcp.heymetra.com/mcp
```

_You can also add the server to a .mcp.json file at the project root. Run /mcp in a session to sign in and to check that it connected._

Full walkthrough: [heymetra.com/mcp/claude-code/](https://heymetra.com/mcp/claude-code/)
</details>

<details>
<summary><b>Codex</b> — ~/.codex/config.toml</summary>

```toml
[mcp_servers.heymetra]
url = "https://mcp.heymetra.com/mcp"
```

_Codex reads the server from an [mcp_servers.<name>] section in config.toml, and you sign in with codex mcp login <name>._

Full walkthrough: [heymetra.com/mcp/codex/](https://heymetra.com/mcp/codex/)
</details>

<details>
<summary><b>Cursor</b> — ~/.cursor/mcp.json, or .cursor/mcp.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "url": "https://mcp.heymetra.com/mcp" }
  }
}
```

_Cursor signs in to HeyMetra without a client ID or secret, so the server entry needs no auth block._

Full walkthrough: [heymetra.com/mcp/cursor/](https://heymetra.com/mcp/cursor/)
</details>

<details>
<summary><b>Antigravity</b> — ~/.gemini/config/mcp_config.json, or .agents/mcp_config.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "serverUrl": "https://mcp.heymetra.com/mcp" }
  }
}
```

_Antigravity's documented key for the address is serverUrl, though it also accepts url._

Full walkthrough: [heymetra.com/mcp/antigravity/](https://heymetra.com/mcp/antigravity/)
</details>

## What it may and may not touch

Propose a change to this account. Nothing is sent until you approve it, and HeyMetra cannot undo it afterwards.

Permissions are switched on per connection, and one you leave off is a tool your assistant never sees.

| Permission | What it covers | Changes anything? |
|---|---|---|
| **Full account access** | Lets your assistant read anything in this account to answer your questions. The figures are the provider's own, not ones HeyMetra has checked. It can also propose changes: none is applied until you approve it, and HeyMetra cannot undo one afterwards — A personal API key reaches the projects the person who made it can open, so a project nobody shared is invisible rather than empty; Event data is queried, not exported: a question spanning months of raw events is a query PostHog may refuse on time rather than a download that eventually finishes. | Yes — every change waits for your approval |

<details>
<summary>What each permission lets an assistant do, in full</summary>

- Ask anything about this account and get the answer from its live data. Reads only, and the figures are the provider's own rather than ones HeyMetra has checked.
- Propose a change to this account. Nothing is sent until you approve it, and HeyMetra cannot undo it afterwards.
</details>

Anything that would change something comes back as a proposal you approve. Nothing is applied before your yes, and only on an account you connected with permission to change it. [How that works](https://heymetra.com/security/).

## When something goes wrong

<details>
<summary>The key is rejected and it was copied correctly.</summary>

**Why:** The address is the wrong one. A key issued in the EU account is not a key the US host has ever seen, and a key from a company's own installation is unknown to both. All three look like a bad key rather than a wrong address.

**Fix:** Sign in to PostHog, read the address out of the address bar, and edit the connection to match.

</details>

<details>
<summary>You run PostHog yourselves and it is not reachable from the internet.</summary>

**Why:** HeyMetra calls your installation from its own servers. An address that only resolves inside your network, or one behind a VPN, is not an address we can reach.

**Fix:** Connect an installation that answers on a public address. There is no tunnel or agent to install, and nothing here can work around it.

</details>

<details>
<summary>It connects, but a question comes back with 403.</summary>

**Why:** The key was made without the scope that question needs. Reading events and running a HogQL query are separate scopes, so one can work while the other does not.

**Fix:** Add the scope in PostHog (the 403 names it), or create a key with the read scopes and replace this one with the pencil. The connection keeps its name and everything pointing at it.

</details>

<details>
<summary>Only some of your products appear.</summary>

**Why:** A personal API key reaches the projects YOU can open. A project somebody else owns and never shared is not one of them.

**Fix:** Ask to be added to that project in PostHog, then reconnect so the project list is read again.

</details>

## What HeyMetra reads from PostHog

Connect with a personal API key and one answer: is this PostHog Cloud, or PostHog on a machine you run? Cloud needs nothing else, because HeyMetra works out your region from the key. Your own installation needs its address, and it has to be reachable on the public internet. A key reaches every project in your organisation, so a portfolio is one connection per project and each is named here; that name is what you call it when you ask. Then ask your assistant about your saved insights and their results, your events, and questions nobody has saved an insight for. The answers are PostHog's own rather than figures HeyMetra has checked, and say so. Nothing is changed unless you connected it to allow that, and then only through a card you approve.

<details>
<summary>About PostHog</summary>

PostHog is product analytics: every event your app or site sends, the funnels and retention built on top of them, the cohorts of people behind a number, session replays and feature flags. It is where "what did people actually do" is answered, as opposed to what an ad platform says it delivered.
</details>

## One connection, not seven

The reason to read PostHog through HeyMetra rather than through a server that only knows PostHog is everything else it can answer in the same breath:

**Ads** — [Google Ads](https://github.com/zeisoft/google-ads-mcp)

**Analytics** — [Google Analytics 4](https://github.com/zeisoft/google-analytics-4-mcp) · [Google Search Console](https://github.com/zeisoft/google-search-console-mcp) · **PostHog**

**Ecommerce** — [Trendyol](https://github.com/zeisoft/trendyol-mcp) · [n11](https://github.com/zeisoft/n11-mcp) · [Çiçeksepeti](https://github.com/zeisoft/ciceksepeti-mcp) · [Amazon Seller Central](https://github.com/zeisoft/amazon-seller-central-mcp) · [ikas](https://github.com/zeisoft/ikas-mcp) · [WooCommerce](https://github.com/zeisoft/woocommerce-mcp)

**Revenue & CRM** — [Stripe](https://github.com/zeisoft/stripe-mcp) · [Zoho CRM](https://github.com/zeisoft/zoho-crm-mcp) · [Zoho SalesIQ](https://github.com/zeisoft/zoho-salesiq-mcp) · [Zoho Marketing Automation](https://github.com/zeisoft/zoho-marketing-automation-mcp)

**Mobile** — [AppsFlyer](https://github.com/zeisoft/appsflyer-mcp) · [RevenueCat](https://github.com/zeisoft/revenuecat-mcp) · [Adapty](https://github.com/zeisoft/adapty-mcp) · [App Store Connect](https://github.com/zeisoft/app-store-connect-mcp)

**Work** — [Jira](https://github.com/zeisoft/jira-mcp)

**Channels** — [Slack](https://github.com/zeisoft/slack-mcp) · [Telegram](https://github.com/zeisoft/telegram-mcp)

The full catalogue is at [heymetra.com/connectors/](https://heymetra.com/connectors/).

## Links

- [PostHog connector page](https://heymetra.com/connectors/posthog/)
- [PostHog setup guide](https://heymetra.com/docs/posthog/)
- [HeyMetra](https://heymetra.com/) — what the product is
- [Setup for every assistant](https://heymetra.com/mcp/)
- [Security and limits](https://heymetra.com/security/)
- [Pricing](https://heymetra.com/pricing/)
- [HeyMetra's own repository](https://github.com/zeisoft/heymetra-mcp)

---

<sub>Built by <a href="https://zeisoft.com">Zeisoft</a>, who make HeyMetra. Not affiliated with PostHog. This README is generated from HeyMetra's live connector catalogue and refreshed daily; corrections are welcome as issues.</sub>
