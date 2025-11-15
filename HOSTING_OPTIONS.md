# GitHub-Based Static Hosting Options for Claude Code Work

## Overview
This document explores how to host and share work created in the Claude Code virtualized environment using GitHub's static hosting capabilities.

## Environment Constraints

### What Claude CAN Do:
- ✅ Create static files (HTML, CSS, JavaScript)
- ✅ Commit and push to GitHub repositories
- ✅ Create branches (with naming restrictions: must start with 'claude/')
- ✅ Make unauthenticated GitHub API calls (60/hour limit)
- ✅ Access internet via WebFetch/WebSearch tools (read-only)
- ✅ Run code locally in sandbox (not externally accessible)

### What Claude CANNOT Do:
- ❌ Use GitHub CLI (`gh` not available)
- ❌ Create authenticated GitHub API requests (no token access)
- ❌ Create Gists programmatically
- ❌ Configure repository settings via API
- ❌ Create publicly accessible network endpoints directly
- ❌ Use tunneling services (ngrok, cloudflared not installed)

---

## Option 1: GitHub Gists

### What Are Gists?
- Simplified repositories for sharing code snippets
- Can contain multiple files
- Support static HTML rendering
- Have their own URLs: `gist.github.com/username/gist-id`

### Capabilities:
- **Static HTML hosting**: Gists with `index.html` can be viewed via services like:
  - `bl.ocks.org/username/gist-id` (D3 blocks)
  - `htmlpreview.github.io/?https://gist.githubusercontent.com/username/gist-id/raw/file.html`
- **Versioning**: Full git history
- **Embedding**: Can be embedded in other sites
- **Public or Secret**: Control visibility

### Claude's Limitations with Gists:
- **Cannot create directly**: No `gh` CLI or authenticated API access
- **Workaround**: Claude creates content → User manually creates Gist

### Process:
1. Claude creates HTML/JS/CSS files in repo
2. User copies content and creates Gist manually
3. User shares Gist URL
4. Content viewable via Gist viewers/preview services

### Use Cases:
- Quick one-off tools or demos
- Small interactive utilities
- Code snippets with visualization
- Shareable prototypes

---

## Option 2: GitHub Pages

### What Is GitHub Pages?
- Static site hosting directly from GitHub repositories
- Free hosting at `username.github.io/repo-name`
- Supports custom domains
- Jekyll support (optional)
- HTTPS by default

### Capabilities:
- **Full client-side applications**: React, Vue, vanilla JS, etc.
- **WebAssembly**: Python (Pyodide), Rust, C++, etc. compiled to WASM
- **Progressive Web Apps**: Can work offline
- **External API calls**: Can interact with third-party services
- **Client-side storage**: localStorage, IndexedDB
- **Interactive REPLs**: JavaScript, Python (via Pyodide), etc.
- **No server-side execution**: Pure static hosting

### Claude's Capabilities with GitHub Pages:
- ✅ Create all static content (HTML/CSS/JS)
- ✅ Push to appropriate branch
- ✅ Create `gh-pages` branch
- ✅ Organize files in `/docs` folder
- ❌ Cannot enable Pages in repo settings (user must do this)
- ❌ Cannot configure Pages settings via API

### Setup Process:

#### Method 1: gh-pages Branch
1. Claude creates `gh-pages` branch
2. Claude adds `index.html` and assets
3. Claude commits and pushes
4. **User enables** in repo: Settings → Pages → Source: `gh-pages` branch
5. Site live at: `https://tylerstoltz.github.io/git_pages/`

#### Method 2: /docs Folder on Main
1. Claude creates `/docs` directory
2. Claude adds `index.html` and assets
3. Claude commits and pushes to main
4. **User enables** in repo: Settings → Pages → Source: main branch `/docs` folder
5. Site live at: `https://tylerstoltz.github.io/git_pages/`

#### Method 3: Feature Branch → PR → Deploy
1. Claude creates content on feature branch
2. User reviews PR
3. User merges to main/gh-pages
4. User configures Pages

### Use Cases:
- Interactive documentation
- Web-based REPLs (JS, Python via Pyodide)
- Data visualization tools
- Calculator/utility web apps
- Portfolio/demo sites
- Interactive tutorials

---

## Comparison Matrix

| Feature | GitHub Gists | GitHub Pages |
|---------|--------------|--------------|
| **Claude Can Create Directly** | ❌ No | ✅ Yes (content only) |
| **User Setup Required** | Manual Gist creation | Enable in repo settings |
| **URL Format** | `gist.github.com/user/id` | `user.github.io/repo` |
| **Custom Domain** | ❌ No | ✅ Yes |
| **Multiple Pages** | Limited | ✅ Full site structure |
| **Version Control** | ✅ Yes | ✅ Yes |
| **File Size** | Small files preferred | Larger projects supported |
| **Discoverability** | Lower | Higher (can be indexed) |
| **Best For** | Quick demos, snippets | Full applications, docs |

---

## What Can We Build?

### Client-Side REPLs:
1. **JavaScript REPL**: Immediate execution in browser
2. **Python REPL**: Using Pyodide (Python → WebAssembly)
3. **SQL REPL**: Using sql.js (SQLite in browser)
4. **Regex Tester**: Live pattern matching
5. **Markdown Editor**: Live preview

### Interactive Tools:
- JSON formatter/validator
- Base64 encoder/decoder
- Color picker/converter
- Chart/graph generators
- API testing interface
- File format converters

### Communication Possibilities:
- **One-way (Claude → User)**: Claude updates content, user refreshes
- **Storage**: localStorage for user state between sessions
- **External APIs**: Could integrate with third-party services
- **No real-time bidirectional**: Without external service (Firebase, Supabase, etc.)

---

## Recommended Approach: GitHub Pages

### Why GitHub Pages?
1. Claude can create everything except final enablement
2. User involvement minimal (just enable in settings)
3. Supports complex applications
4. Permanent, shareable URL
5. Can evolve over time

### Initial Setup:
```bash
# Claude will:
1. Create gh-pages branch
2. Add index.html with interactive REPL
3. Push to remote
4. Provide instructions for user

# User will:
1. Go to repo Settings → Pages
2. Select "gh-pages" branch as source
3. Save
4. Access site at provided URL
```

---

## Next Steps

1. **Choose REPL type**: JavaScript, Python (Pyodide), or multi-language?
2. **Define features**: What functionality is most useful?
3. **Create and deploy**: Claude builds, user enables
4. **Iterate**: Update content as needed via git pushes

---

## Questions for User

1. What type of REPL/tool would be most valuable?
2. Should we start simple (JS REPL) or more complex (Python via Pyodide)?
3. Any specific features or integrations needed?
4. Preference for gh-pages branch vs /docs folder approach?

---

**Last Updated**: 2025-11-15
**Environment**: Claude Code Virtualized Sandbox
**Repository**: tylerstoltz/git_pages
