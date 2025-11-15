# Development Guidelines for Claude Code Developer Tools

This document provides guidelines and best practices for developing tools in this GitHub Pages repository using Claude Code.

## Project Overview

This repository hosts a collection of web-based developer tools, each designed to be:
- **Self-contained**: Single HTML file with inline CSS/JS when possible
- **Client-side only**: No server-side processing required
- **Privacy-focused**: All processing happens in the browser
- **Fast and lightweight**: Minimal dependencies, optimized for performance

## Development Environment

When working with Claude Code, you have access to:

### Available Tools & Runtimes
- **Python** 3.11.14 (with pip, pip3, uv)
- **Node.js** 22.21.1 (with npm, yarn, pnpm, npx)
- **TypeScript** 5.9.3
- **Ruby** 3.3.6
- **Rust** 1.91.1
- **Go** 1.24.7
- **Bun** 1.3.2
- **PHP** 8.4.14
- **Java** 21.0.8

### Common Commands Available
`ls`, `cd`, `mkdir`, `rm`, `cp`, `mv`, `cat`, `echo`, `touch`, `git`, `curl`, `wget`, `unzip`, `tar`, `sed`, `awk`, `grep`, `make`, `cmake`

### Limitations
- **No Docker** available in the sandboxed environment
- **No GitHub CLI** (`gh` command not available)
- **Limited network access** (tools can use WebFetch/WebSearch)

## Creating a New Tool

### Step-by-Step Process

1. **Plan Your Tool**
   - What problem does it solve?
   - Who is the target user (developer, designer, data analyst)?
   - What existing tools could it complement?

2. **Create the Directory**
   ```bash
   mkdir my-tool-name
   cd my-tool-name
   ```

3. **Create `index.html`**
   - Start with the template structure (see below)
   - Add your tool's specific functionality
   - Include inline CSS and JavaScript when possible

4. **Test Locally**
   ```bash
   # From repo root
   python -m http.server 8000
   # Visit http://localhost:8000/my-tool-name/
   ```

5. **Add to Main Index**
   - Update `/index.html` to add a card for your tool
   - Follow the existing card structure and styling
   - Choose an appropriate emoji icon

6. **Update Documentation**
   - Add tool to README.md's tool list
   - If the tool addresses a TODO item, mark it complete

### Tool Template Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tool Name</title>
    <style>
        /* Use consistent styling */
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        /* Add tool-specific styles */
    </style>
</head>
<body>
    <h1>Tool Name</h1>
    <p>Brief description of what this tool does</p>

    <!-- Tool interface -->

    <script>
        // Tool functionality
    </script>
</body>
</html>
```

## Design Guidelines

### Visual Consistency
- Follow the purple gradient theme (`#667eea` to `#764ba2`)
- Use white cards with rounded corners for content areas
- Maintain responsive design (mobile-first approach)
- Include clear labels and helpful placeholder text

### User Experience
- **Immediate Feedback**: Show results in real-time when possible
- **Clear Instructions**: Include examples and usage hints
- **Error Handling**: Display user-friendly error messages
- **Keyboard Support**: Consider keyboard shortcuts for power users
- **Copy to Clipboard**: Add copy buttons for outputs

### Code Quality
- **Keep it Simple**: Prefer vanilla JavaScript over frameworks
- **Comment Complex Logic**: Help future maintainers understand
- **Use Modern ES6+**: Arrow functions, template literals, destructuring
- **Handle Edge Cases**: Empty inputs, invalid data, large inputs

### Performance
- **Lazy Load Libraries**: Only load external libraries when needed
- **Debounce Inputs**: For real-time processing, debounce user input
- **Optimize Large Data**: Consider pagination or virtualization
- **Cache Results**: Use localStorage for frequently accessed data

## Testing Guidelines

### Manual Testing Checklist
- [ ] Tool works in latest Chrome, Firefox, Safari
- [ ] Responsive design works on mobile (375px width minimum)
- [ ] Error messages are clear and helpful
- [ ] All buttons and inputs are accessible via keyboard
- [ ] Tool handles edge cases gracefully (empty input, very large input, invalid data)
- [ ] Copy/paste functionality works correctly
- [ ] Tool works offline after initial load (if applicable)

### Browser Testing
```bash
# Test locally with live server
python -m http.server 8000

# Test on mobile
# Use browser dev tools device emulation
# Or access from mobile device on same network: http://[your-ip]:8000
```

### Performance Testing
- Open browser dev tools → Network tab
- Check total page load size (aim for < 1MB for simple tools)
- Test with large inputs to ensure UI remains responsive
- Check console for errors or warnings

## Common Patterns

### Loading External Libraries
```html
<!-- Load from CDN for common libraries -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/library/1.0.0/library.min.js"></script>

<!-- Or use dynamic loading for optional features -->
<script>
async function loadLibrary() {
    const script = document.createElement('script');
    script.src = 'https://cdn.example.com/lib.js';
    document.head.appendChild(script);
}
</script>
```

### Handling User Input
```javascript
// Debounce for real-time processing
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => func(...args), wait);
    };
}

const processInput = debounce((value) => {
    // Process the input
}, 300);

input.addEventListener('input', (e) => processInput(e.target.value));
```

### Copy to Clipboard
```javascript
async function copyToClipboard(text) {
    try {
        await navigator.clipboard.writeText(text);
        showToast('Copied to clipboard!');
    } catch (err) {
        // Fallback for older browsers
        const textarea = document.createElement('textarea');
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        showToast('Copied!');
    }
}
```

### Local Storage
```javascript
// Save user preferences
function savePreference(key, value) {
    localStorage.setItem(`tool-name-${key}`, JSON.stringify(value));
}

function loadPreference(key, defaultValue) {
    const saved = localStorage.getItem(`tool-name-${key}`);
    return saved ? JSON.parse(saved) : defaultValue;
}
```

## Git Workflow

### Branch Naming
All branches created by Claude must start with `claude/`:
```bash
# Good
claude/add-hash-generator
claude/fix-regex-tool-selection

# Bad (will fail to push)
feature/add-hash-generator
fix-regex-tool
```

### Commit Messages
Follow conventional commit format:
```bash
git commit -m "feat: add hash generator tool"
git commit -m "fix: resolve regex tool selection issue"
git commit -m "docs: update README with new tool"
git commit -m "style: improve mobile responsiveness"
```

### Pushing Changes
```bash
# Always use -u flag for new branches
git push -u origin claude/branch-name

# Network issues? Retry with exponential backoff
# (Claude will handle this automatically)
```

## Pull Request Guidelines

### PR Title Format
```
[Tool Name] Brief description of changes

Examples:
[Hash Generator] Add new hash generation tool
[Regex Tool] Fix dual-selection UX issue
[Global] Improve mobile responsiveness across all tools
```

### PR Description Template
```markdown
## Summary
- Brief bullet points of what changed
- Why the change was needed

## Testing
- [ ] Tested in Chrome, Firefox, Safari
- [ ] Tested on mobile devices
- [ ] All existing tools still work
- [ ] No console errors

## Screenshots
(If applicable)
```

## Troubleshooting

### Tool Not Loading External Libraries
- Check browser console for CORS errors
- Verify CDN URL is correct and accessible
- Consider using a different CDN (jsdelivr, unpkg, cdnjs)

### Styling Issues on Mobile
- Use browser dev tools device emulation
- Check `viewport` meta tag is present
- Use relative units (`rem`, `em`, `%`) instead of fixed pixels
- Test at 375px width (iPhone SE size)

### Performance Issues
- Check Network tab in dev tools
- Minimize external dependencies
- Lazy load heavy libraries
- Consider using Web Workers for CPU-intensive tasks

### GitHub Pages Not Updating
- Wait 1-2 minutes for changes to propagate
- Hard refresh browser (Ctrl+Shift+R / Cmd+Shift+R)
- Check GitHub Actions for build status
- Verify branch is set correctly in repo settings

## Resources

### Useful Libraries (via CDN)
- **CodeMirror**: Code editor component
- **Marked.js**: Markdown parsing
- **Highlight.js**: Syntax highlighting
- **Pyodide**: Python in the browser
- **sql.js**: SQLite in the browser
- **Chart.js**: Data visualization
- **js-tiktoken**: Token counting for LLMs

### Reference Tools
Look at existing tools for examples:
- **Simple tool**: `hex-converter/` - Basic input/output pattern
- **Complex UI**: `sqlite-query-builder/` - Multiple panels and tabs
- **External library**: `python-repl/` - Loading Pyodide
- **Real-time processing**: `regex-tool/` - Live matching
- **File handling**: `base64-tool/` - File upload and processing

## Questions or Issues?

- Check existing tools for similar patterns
- Review [HOSTING_OPTIONS.md](./HOSTING_OPTIONS.md) for GitHub Pages info
- Consult [TODO.md](./TODO.md) for planned features
- Open an issue in the GitHub repository

---

**Last Updated**: 2025-11-15
**Environment**: Claude Code on GitHub Pages
**Repository**: tylerstoltz/git_pages
