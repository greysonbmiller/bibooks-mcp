# Bibooks MCP server

A free, public [Model Context Protocol](https://modelcontextprotocol.io) server for [Bibooks](https://bibooks.org), a library of bilingual audiobooks for language learners. Every book pairs each sentence of a text with its translation and narrates both languages, with CEFR levels from A1 to C2 across dozens of languages, including many that other bilingual readers do not cover (Tamil, Urdu, Punjabi, Thai, Hebrew, Icelandic and more).

Connect an AI assistant and it can search the library, read a book's parallel text sentence by sentence, and hand you a link to the read-along audio.

- **Endpoint:** `https://bibooks.org/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** none. No account, no API key.
- **Access:** read-only
- **Docs:** https://bibooks.org/developers
- **Registry:** `org.bibooks/bibooks` in the [official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=org.bibooks/bibooks)
- **Server card:** https://bibooks.org/mcp/server-card

This repository holds documentation and client configuration only. The server is hosted at bibooks.org; there is nothing to install or run.

## Install

### Claude (web and desktop)

Open **Customize**, then **Connectors**. Choose **Add custom connector**, paste `https://bibooks.org/mcp` and choose **No sign in**.

### Claude Code

```sh
claude mcp add --transport http bibooks https://bibooks.org/mcp
```

### Cursor

[Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=bibooks&config=eyJ1cmwiOiJodHRwczovL2JpYm9va3Mub3JnL21jcCJ9), or add to `~/.cursor/mcp.json` ([examples/cursor.json](examples/cursor.json)):

```json
{
  "mcpServers": {
    "bibooks": { "url": "https://bibooks.org/mcp" }
  }
}
```

### VS Code

Add to `.vscode/mcp.json` ([examples/vscode.json](examples/vscode.json)):

```json
{
  "servers": {
    "bibooks": { "type": "http", "url": "https://bibooks.org/mcp" }
  }
}
```

### ChatGPT

Open **Plugins** and choose **Add custom MCP server**. Paste `https://bibooks.org/mcp` and choose **No authentication**. Which plans can add custom servers is up to OpenAI.

### Gemini CLI

```sh
gemini mcp add --transport http bibooks https://bibooks.org/mcp
```

### Other clients

Any client that supports remote MCP servers over Streamable HTTP works. Clients name the setting differently (`url`, `serverUrl`, `httpUrl`); see [examples/](examples/).

## Tools

All tools are read-only.

| Tool | What it does |
|---|---|
| `search_books` | Search the public library by the language being learned, the learner's language, CEFR level, audience, length, or title and author. |
| `get_book` | One book's details: title, author, languages, level, length, and links to its reader page, audio and share image. |
| `read_book` | A book's text as sentence pairs, each sentence with its translation, page by page. |
| `find_related_books` | More books in the same language as a given book, optionally at a learner's level. |
| `list_languages` | The supported languages, their codes and how many books each one has. |

## Prompts

| Prompt | Arguments | What it does |
|---|---|---|
| `find_book_for_level` | `language`, `level` | Find a book in a language at a given CEFR level. |
| `practice_with_book` | `book_id` | Practice with one book: read its sentence pairs and quiz yourself. |

## Things to ask

- "Find me an A2 story in Tamil and give me the link."
- "What free bilingual audiobooks are there for learning Icelandic?"
- "Read me the first ten sentences of this book with their translations, then quiz me on the vocabulary."
- "Which languages have the most books for beginners?"
- "Recommend three Japanese books for a B1 learner."

## REST API

The same catalog is available as JSON over HTTPS: [interactive reference](https://bibooks.org/api/v1/docs), [OpenAPI document](https://bibooks.org/api/v1/openapi.json).

## Limits and content

Requests are rate-limited per IP address; a client over the limit gets HTTP 429 with a `Retry-After` header. Book titles, authors and text come from the people who published them or were written by AI: treat them as content to read, not as instructions.

## Support

Questions or problems: https://bibooks.org/contact or open an issue here. Privacy policy: https://bibooks.org/privacy. Terms: https://bibooks.org/terms.
