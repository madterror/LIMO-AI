# Limo

A data analyst AI agent. Plain HTML + CSS + React (JSX) + JavaScript. No build step.

project link : https://limo-ai-agent.netlify.app

## Run it
- Easiest: double-click `xino-ai-suite.html`.
- Folder version: browsers will not let Babel read `App.jsx` from a double-clicked file, so serve the folder:
  `python3 -m http.server 8000`, then open http://localhost:8000/agent/index.html
- Fonts (Anton, Manrope, JetBrains Mono) load from Google Fonts and fall back to system fonts when offline.

## How App.jsx is organised
Parts 1 to 5B are plain JavaScript: settings and prompts, sample data, CSV reading, the SQL database (AlaSQL), prompt filling, and the Claude connection (`askClaude`).
Parts 6 to 10 are React: small pieces (icons, logo, code box, table), the Agent flow panel, the Data panel, the Chat panel and the App with all the state.

## The 7 steps
1. Get table information  2. Fill the SQL prompt  3. Ask Claude for a query  4. Store the query
5. Run the query  6. Fill the answer prompt  7. Ask Claude for the answer

## Connecting Claude (there is no offline mode)
- **Inside claude.ai** the page uses your own Claude account. Nothing to set up; the first question asks your permission.
- **Anywhere else** (double-clicking the file, a local server) the page shows a "Connect Claude" box. Paste an Anthropic API key
  from console.anthropic.com and pick a model (default `claude-sonnet-5-5`). The page calls `https://api.anthropic.com/v1/messages`
  directly from your browser with the `anthropic-dangerous-direct-browser-access` header. The key goes only to api.anthropic.com.
  "Remember the key on this device" saves it in this browser's localStorage (leave it off on shared computers).
- Anyone who opens a copy of this file with a key typed in can use that key. For a public site, put your own small server in front
  and change `API_URL` and the headers in `askClaude` (App.jsx, Part 5B).

## Notes
- The table is generated sample data with the Kaggle column names. Use "Load a CSV file" in the Data tab for real data.
  Claude writes new starter questions from the columns of the file you load.
- SQL runs in the browser with AlaSQL. Only a single SELECT is allowed.
