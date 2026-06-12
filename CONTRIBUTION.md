# Contribution Guidelines — Reverse Flight

Welcome! This component is part of the BetoOS Datacore library. Please adhere to the following architectural standards.

## Codebase Architecture

The module utilizes a split-file structure to guarantee legibility, testability, and isolated execution scopes:

```text
ReverseFlight/
├── REVERSE FLIGHT.md      # Obsidian entry point
├── METADATA.md            # Component manifest
├── README.md              # Documentation
├── CONTRIBUTION.md        # This file
├── LICENSE.md             # MIT license
├── data/
│   └── mcp_commands.json  # External watch/reload trigger
├── assets/
│   ├── image/
│   │   └── preview_1.webp # Static preview image
│   ├── videos/
│   │   └── preview.gif    # Interactive walkthrough GIF
│   └── cache/             # Local offline-ready CDN scripts caching
└── src/
    ├── index.jsx          # Event-driven code watch & reload daemon
    ├── App.jsx            # Main layout and coordinator
    ├── components/
    │   └── FlightComponent.jsx # Core WebGL landscape flight simulation
    ├── styles/
    │   └── styles.jsx     # Scoped Javascript design token sheet
    └── utils/
        ├── domUtils.jsx   # Workspace leaf node locators
        └── loadScript.js  # Vault-caching script loader utility
```

## Developer Standards

1. **Strict Zero Emojis**: All UI elements, buttons, headers, and control indicators must use Lucide vector icons (`<dc.Icon>`) or plain text. Emojis are reserved strictly for documentation.
2. **Path Safety**: Do not hardcode absolute path strings (e.g. `/Volumes/` or `file:///`). Always resolve vault directories dynamically.
3. **No-Polling Code Watcher**: The index bootstrapper registers an event listener with `app.vault.on("modify")` targeting files under `ReverseFlight/src/`. This triggers an instant reload of the component's React view when source code modifications are saved, bypassing background CPU polling entirely.
4. **HMR Command System**: To force a code reload or command watch directory path change remotely via MCP agents, write the reload payload to `data/mcp_commands.json`.
