# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

WebSocket Debug Tool - A pure frontend single-page application for debugging WebSocket connections. Built with HTML5, CSS3, and native JavaScript (ES6+) without any external dependencies.

## Development Commands

- **Preview**: Open `index.html` directly in any modern browser
- **Development**: Edit `index.html` and refresh the browser

## Architecture

### Project Structure
```
websocket-debug-tool/
├── index.html              # All HTML/CSS/JS in one file
├── docs/
│   ├── 需求文档.md          # Requirements (Chinese)
│   └── plans/
│       └── 实现计划.md      # Implementation plan
└── CLAUDE.md
```

### Design Decisions
- **Single file**: All code in `index.html` (~100KB)
- **No dependencies**: Pure vanilla JS, no CDNs
- **localStorage**: Key `ws-debug-config` for persistence
- **Global state**: Module-free organization with global variables

### Key Global State
- `ws`: WebSocket instance
- `isConnected`: Boolean connection status
- `messages`: Array of message objects
- `templates`: Array of template objects
- `heartbeatTimer`: Interval ID for heartbeat
- `reconnectAttempts`: Current reconnection attempt count

### Data Structures

**Message object:**
```json
{
  "id": 1707638626000,
  "type": "send" | "receive" | "system",
  "content": "原始消息内容",
  "timestamp": 1707638626000,
  "timeString": "11:23:46"
}
```

**Config stored in localStorage:**
```json
{
  "url": "wss://...",
  "protocol": "wss",
  "heartbeat": { "enabled": true, "interval": 30, ... },
  "reconnect": { "enabled": true, "maxAttempts": 5, ... },
  "templates": [{ "id": "1", "name": "Ping", "content": "...", "shortcut": "1" }]
}
```

### Code Sections (in index.html order)
1. **CSS**: CSS variables (`:root`), component styles, animations
2. **HTML**: App structure, modals, message containers
3. **JS State**: Global variables declaration
4. **JS DOM Ready**: `DOMContentLoaded` handler, `loadFromStorage()`
5. **JS Connection**: `connect()`, `disconnect()`, `updateConnectionUI()`
6. **JS Messages**: `sendMessage()`, `addMessage()`, `handleMessage()`
7. **JS JSON**: `tryParseJson()`, `syntaxHighlightJson()`
8. **JS Heartbeat**: `startHeartbeat()`, `stopHeartbeat()`, `getHeartbeatMessage()`
9. **JS Reconnect**: Auto-reconnect logic in `ws.onclose`
10. **JS Templates**: `addTemplate()`, `deleteTemplate()`, `useTemplate()`
11. **JS Config**: `exportConfig()`, `importConfig()`, `saveToStorage()`
12. **JS Utils**: `showToast()`, `escapeHtml()`

### Shortcuts
- `1-9`: Send template (when not in input)
- `Ctrl+Enter`: Send message
- `Escape`: Disconnect / close modal

## Implementation Plan

See `docs/plans/实现计划.md` for the 14-task implementation roadmap. Use `superpowers:executing-plans` to execute tasks from the plan.
