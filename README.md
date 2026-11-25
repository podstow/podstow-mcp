# podstow MCP server

Text to speech MCP server: send web articles or AI-written text to a private podcast RSS feed, and listen in podstow or any podcast app.

podstow is a hosted service. This repository holds its documentation. It contains no server code and there is nothing to install: point your assistant at the endpoint and sign in.

- **Endpoint:** `https://mcp.podstow.app/` (streamable HTTP)
- **Sign-in:** OAuth 2.1, with dynamic client registration
- **Docs:** <https://podstow.com/assistants/?utm_source=github&utm_medium=readme&utm_campaign=mcp-listing>
- **Account:** created when you first sign in. 5 articles a week are free, no card required.

## What it does

podstow turns the things you mean to read into a private podcast. A connected assistant can send a web article, or text it wrote itself (a summary, a research report, a digest), to your feed. podstow narrates it word for word with natural text to speech and publishes it as an episode. You listen in podstow, or in Apple Podcasts, Overcast, Pocket Casts or any other podcast app.

It reads your text. It does not make a show out of it: one voice, the source read word for word, no generated hosts and no invented discussion. The transcript you get back is the text that was read.

## Connect

### Claude

1. Open **Customize → Connectors → Add custom connector** and paste `https://mcp.podstow.app/`.
2. Sign in to podstow when Claude prompts you.

### ChatGPT

Developer mode, on the web, with a Plus, Pro, Business, Enterprise or Edu plan.

1. Turn on developer mode: **Settings → Security and login → Developer mode**.
2. Go to chatgpt.com/plugins, select **+**, give it a name and description, and paste `https://mcp.podstow.app/` exactly as shown. Do not add `/mcp` to the end: the server answers at the root.
3. Sign in to podstow when ChatGPT prompts you.
4. In a chat, pick podstow from the **+** menu.

### Cursor, VS Code and other MCP clients

Add a remote server. The client handles sign-in itself.

```json
{
  "mcpServers": {
    "podstow": {
      "url": "https://mcp.podstow.app/"
    }
  }
}
```

For a client that only speaks stdio, use the `mcp-remote` bridge:

```json
{
  "mcpServers": {
    "podstow": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.podstow.app/"]
    }
  }
}
```

## Tools

| Tool | Access | What it does |
|---|---|---|
| `submit_url` | write | Send the URL of an article, blog post or web page. podstow reads the page, narrates it and publishes an episode. Uses one article from your quota. |
| `submit_text` | write | Publish text the assistant wrote as an episode, titled `[AI] ...` so you can tell it apart. Uses one article from your quota. |
| `list_episodes` | read | Your most recent episodes: titles, links and publish dates, with a handle for each transcript. |
| `get_episode_transcript` | read | The transcript of an episode: an inline preview, plus a link to the full text. |
| `get_account` | read | Your plan, article usage and limits, voice preferences, and whether you are set up to listen. |
| `show_listen_instructions` | none needed | How to listen: open podstow on this device, or subscribe in a podcast app. |

## Permissions

The server uses two OAuth scopes. `episodes:read` covers reading your episodes and account. `episodes:create` is needed by the two write tools. The app you connect asks for the scopes it needs, and the consent screen lists them. Each connected app can be revoked on its own from your podstow account page.

## Try asking

- "Send this article to my podstow feed: https://example.com/a-long-read"
- "Send this deep research report to my podstow feed."
- "What's in my podstow feed?"

## Listening

Episodes land in your private RSS feed. The feed has a private link nobody can guess. It works like a password, so keep it to yourself. Ask your assistant how to listen and it will walk you through it.

## Links

- Website: <https://podstow.com>
- Setup and tool docs: <https://podstow.com/assistants/?utm_source=github&utm_medium=readme&utm_campaign=mcp-listing>
- Support: <https://podstow.com/support/>
- Privacy: <https://podstow.com/privacy>
- Official MCP Registry: `app.podstow/podstow`

## Licence

The documentation and configuration snippets in this repository are released under the [MIT licence](LICENSE). The licence covers this repository only. The podstow service is a hosted product, and its code is not here.
