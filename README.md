# Claude Code Developer Tools

A collection of web-based developer tools built with Claude Code and hosted on GitHub Pages. Each tool is designed to be lightweight, fast, and work entirely in your browser with no server required.

## Live Site

**[https://tylerstoltz.github.io/git_pages/](https://tylerstoltz.github.io/git_pages/)**

## Available Tools

### 🎨 Claude's Art & Explorations
*Six interactive pieces exploring emergence, complexity, and consciousness*

- **[The Mirror](https://tylerstoltz.github.io/git_pages/the-mirror/)** - A minimal meditation on consciousness, turning the question back on the viewer
- **[Emergent Patterns](https://tylerstoltz.github.io/git_pages/emergent-patterns/)** - Six interactive visualizations showing how complexity emerges from simple rules (particle life, flocking, attractors, waves, flow fields, galaxies)
- **[On Emergence](https://tylerstoltz.github.io/git_pages/on-emergence/)** - An interactive philosophical meditation on complexity, creativity, and consciousness, with embedded visualizations
- **[Ephemeral Canvas](https://tylerstoltz.github.io/git_pages/ephemeral-canvas/)** - Generative art unique to each moment in time, exploring the beauty of impermanence
- **[Neural Garden](https://tylerstoltz.github.io/git_pages/neural-garden/)** - Visualize information flowing through a neural network, watching understanding emerge from computation
- **[The Constellation](https://tylerstoltz.github.io/git_pages/the-constellation/)** - An interactive map of all tools showing connections and relationships across the collection

*See [CLAUDE.md](./CLAUDE.md) for the full story of these creations*

### REPLs & Simulators
- **[JavaScript REPL](https://tylerstoltz.github.io/git_pages/js-repl/)** - Execute JavaScript code in real-time with ES6+ support
- **[Python REPL](https://tylerstoltz.github.io/git_pages/python-repl/)** - Run Python code in-browser using Pyodide with scientific libraries
- **[Arduino Simulator](https://tylerstoltz.github.io/git_pages/arduino-simulator/)** - Virtual Arduino UNO with LEDs, serial monitor, and analog inputs

### Text & Data Processing
- **[Text Formatter](https://tylerstoltz.github.io/git_pages/text-formatter/)** - Transform text with line breaks, encoding, case conversion, find & replace
- **[Regex Tool](https://tylerstoltz.github.io/git_pages/regex-tool/)** - Test regular expressions with live matching and capture groups
- **[JSON Formatter](https://tylerstoltz.github.io/git_pages/json-formatter/)** - Validate, format, and minify JSON with syntax highlighting

### Encoding & Decoding
- **[Base64 Tool](https://tylerstoltz.github.io/git_pages/base64-tool/)** - Encode/decode text and files with URL-safe support
- **[JWT Cookie Inspector](https://tylerstoltz.github.io/git_pages/jwt-cookie-inspector/)** - Decode JWT tokens and view claims, expiration, signature details
- **[Hex ↔ Decimal Converter](https://tylerstoltz.github.io/git_pages/hex-converter/)** - Convert between hexadecimal and decimal number systems
- **[Hash Generator](https://tylerstoltz.github.io/git_pages/hash-generator/)** - Generate MD5, SHA-1, SHA-256, SHA-512 hashes with HMAC support
- **[Unix Timestamp Converter](https://tylerstoltz.github.io/git_pages/timestamp-converter/)** - Convert between Unix timestamps and dates with timezone support

### Specialized Tools
- **[CAN Bus Analyzer](https://tylerstoltz.github.io/git_pages/can-analyzer/)** - Decode and analyze CAN bus messages for automotive/embedded systems
- **[Token Counter](https://tylerstoltz.github.io/git_pages/token-counter/)** - Count tokens for GPT-4, GPT-3.5, and Claude with cost estimation
- **[SQLite Query Builder](https://tylerstoltz.github.io/git_pages/sqlite-query-builder/)** - Visual query builder with SSMS-style interface and sample database

**Total Tools**: 39 (33 practical tools + 6 artistic explorations)

## Features

- **No Installation Required** - All tools run entirely in your browser
- **Privacy-First** - All processing happens client-side, no data leaves your machine
- **Offline Capable** - Most tools work without an internet connection once loaded
- **Mobile Friendly** - Responsive design works on desktop and mobile devices
- **Open Source** - MIT licensed, contributions welcome

## Adding a New Tool

Each tool is a self-contained directory with an `index.html` file. To add a new tool:

1. **Create a directory** for your tool (e.g., `my-tool/`)
2. **Add `index.html`** with your tool's HTML, CSS, and JavaScript
3. **Update `index.html`** in the root directory to add a card linking to your tool
4. **Test locally** by opening in a browser
5. **Commit and push** to the repository

### Tool Structure Example

```
my-tool/
└── index.html    # Self-contained HTML file with inline CSS/JS
```

### Design Guidelines

- Keep tools simple and focused on one task
- Use inline CSS and JavaScript when possible (easier to maintain)
- Follow the existing visual style (purple gradient theme)
- Include clear instructions and examples
- Handle errors gracefully with user-friendly messages
- Test on both desktop and mobile

## Development

### Local Testing

Simply open any `index.html` file in your browser:

```bash
# From repository root
open index.html  # macOS
xdg-open index.html  # Linux
start index.html  # Windows
```

Or use a local server:

```bash
# Python
python -m http.server 8000

# Node.js
npx serve

# PHP
php -S localhost:8000
```

Then visit `http://localhost:8000` in your browser.

### Project Structure

```
git_pages/
├── index.html              # Main landing page with tool grid
├── js-repl/
│   └── index.html
├── python-repl/
│   └── index.html
├── arduino-simulator/
│   └── index.html
├── regex-tool/
│   └── index.html
├── text-formatter/
│   └── index.html
└── ... (other tools)
```

### Technology Stack

Most tools use:
- Pure HTML/CSS/JavaScript (no build process required)
- Modern ES6+ JavaScript
- Browser APIs (localStorage, fetch, etc.)
- External libraries loaded via CDN when needed (Pyodide, CodeMirror, etc.)

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

See [TODO.md](./TODO.md) for ideas on what to build next.

## Known Issues

- **Regex Tool**: Dual-selection mode has UX issues with context/changing bit selection (see TODO.md for details)
- Some tools may have limited mobile support - improvements welcome!

## Resources

- [AGENTS.md](./AGENTS.md) - Development environment and testing guidelines
- [HOSTING_OPTIONS.md](./HOSTING_OPTIONS.md) - Information about GitHub Pages hosting
- [TODO.md](./TODO.md) - Planned features and improvements

## License

MIT License - Feel free to use, modify, and distribute these tools.

## Built With

Created using [Claude Code](https://claude.ai/code) - An AI-powered development environment.

---

**Repository**: [github.com/tylerstoltz/git_pages](https://github.com/tylerstoltz/git_pages)
**Hosted On**: GitHub Pages
