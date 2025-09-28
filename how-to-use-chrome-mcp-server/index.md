# How to use Chrome MCP: a simple guide


## Introduction

**mcp-chrome** (also called *Chrome MCP Server*) is a Chrome extension–based MCP (Model Context Protocol) server.
It lets MCP clients (e.g. AI agents, chatbots) connect to your regular Chrome/Chromium browser, use your existing login state, and control or inspect web pages. 

[Main GitHub Repo is here](https://github.com/hangwin/mcp-chrome/)

## Main Features

* Works with your real browser (no separate headless instance)
* Fully local (no remote server)
* Uses *streamable HTTP* as connection method (or stdio alternative)
* Semantic search across tabs (vector index) & content analysis
* Over 20 “tools” (APIs) to interact with browser: navigation, network, screenshots, DOM, bookmarks, history, etc.

## Installation & Usage Guide

### Requirements

* Node.js **= 18.19.0** and `npm` or `pnpm`
* Chrome or Chromium browser

### Installation Steps

1. Install the bridge globally:

   ```bash
   npm install -g mcp-chrome-bridge
   ```

   Or with pnpm (enabling pre/post scripts):

   ```bash
   pnpm config set enable-pre-post-scripts true && pnpm install -g mcp-chrome-Bridge
   ```
2. Register the bridge:

   ```bash
   mcp-chrome-bridge register
   ```
3. Download & install the Chrome extension:
   Go to the [GitHub Releases of mcp-chrome](https://github.com/hangwin/mcp-chrome/releases) and download the extension.
4. In Chrome, open `chrome://extensions/`, enable **Developer mode**, “Load unpacked” and select the extension folder, then open the extension’s popup.

### Using It

* In the extension popup, click **Connect** to establish the bridge connection.
* The extension will show a port (default **12306**) for the MCP server.
* In your MCP client config, add:

  ```json
  {
    "mcpServers": {
      "chrome-mcp-server": {
        "type": "streamableHttp",
        "url": "http://127.0.0.1:12306/mcp"
      }
    }
  }
  ```

  (Port 12306 is the default shown in extension popup)
* Alternatively, if your client only supports stdio mode, use the `mcp-server-stdio.js` shipped in the bridge and configure as a command/args in MCP client config.

## Tools (APIs) in mcp-chrome

The following is a more complete list of tools exposed by mcp-chrome (v0.0.6)

### Browser Management

* `get_windows_and_tabs` — list all browser windows & tabs
* `chrome_navigate` — navigate to URL, control viewport
* `chrome_close_tabs` — close specific tabs or windows
* `chrome_go_back_or_forward` — browser back / forward navigation
* `chrome_inject_script` — inject content scripts into pages
* `chrome_send_command_to_inject_script` — send commands to scripts you injected

### Screenshots & Visual

* `chrome_screenshot` — capture screenshot, full page or element-level

### Network Monitoring

* `chrome_network_capture_start` / `chrome_network_capture_stop` — use webRequest API to capture network activity
* `chrome_network_debugger_start` / `chrome_network_debugger_stop` — use Debugger API to capture deeper request/response data
* `chrome_network_request` — send custom HTTP requests from browser context

### Content & Analysis

* `search_tabs_content` — semantic search across all open tab contents
* `chrome_get_web_content` — extract HTML / text content from a page
* `chrome_get_interactive_elements` — get clickable / interactive elements on page
* `chrome_console` — capture and retrieve console logs from browser tabs

### Interaction (User Actions)

* `chrome_click_element` — click element via CSS selector
* `chrome_fill_or_select` — fill forms, select dropdowns, set values
* `chrome_keyboard` — simulate keyboard events or shortcuts

### Data Management

* `chrome_history` — search browser history with time filters
* `chrome_bookmark_search` — search bookmarks by keyword
* `chrome_bookmark_add` — add a bookmark (with folder support)
* `chrome_bookmark_delete` — delete a bookmark

This set covers most of the common browser automation needs—navigation, content reading, network capture, user interactions, bookmarks, history, and more.

⚠️ **Note**: Because mcp-chrome is under active development, new tools might be added, or some may evolve. Always check the latest TOOLS documentation in the repo.

