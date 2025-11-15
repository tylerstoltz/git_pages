# Claude Code Developer Tools - Gameplan

**Last Updated**: 2025-11-15
**Repository**: tylerstoltz/git_pages
**Live Site**: https://tylerstoltz.github.io/git_pages/

## Project Vision

Create a comprehensive, privacy-focused collection of web-based developer tools that:
- Run entirely in the browser with no server dependencies
- Provide immediate value to developers, engineers, and data professionals
- Maintain high code quality and user experience standards
- Serve as a showcase of what can be built with Claude Code

## Current State (12 Tools)

### REPLs & Simulators (3)
- ✅ JavaScript REPL
- ✅ Python REPL (Pyodide)
- ✅ Arduino Simulator

### Text & Data Processing (3)
- ✅ Text Formatter
- ✅ Regex Tool (has known UX issue)
- ✅ JSON Formatter

### Encoding & Decoding (3)
- ✅ Base64 Tool
- ✅ JWT Cookie Inspector
- ✅ Hex ↔ Decimal Converter

### Specialized Tools (3)
- ✅ CAN Bus Analyzer
- ✅ Token Counter (LLM)
- ✅ SQLite Query Builder

## Immediate Priorities (Phase 1)

### 1. Bug Fixes - CRITICAL
**Priority**: Must fix before adding new tools

#### Regex Tool Dual-Selection Issue
**Problem**: UX flow is broken when selecting context blocks and changing bits
- If user selects context first, they're prompted to select context anyway
- If user clicks "Select Context" first, instructions appear in wrong order
- Context and Changing Bit selections always show as identical

**Solution Required**:
- Review selection state management
- Fix instruction sequencing
- Ensure selections are independently tracked
- Add visual feedback for each selection step

**Estimated Effort**: 2-3 hours

### 2. Quality Improvements - HIGH
**Priority**: Enhance existing tools before expansion

#### Mobile Responsiveness Audit
- Test all 12 tools on mobile devices (375px width minimum)
- Fix any layout issues, especially on:
  - SQLite Query Builder (complex multi-panel UI)
  - Arduino Simulator (visual components)
  - Python REPL (Pyodide loading states)
- Ensure touch-friendly buttons and inputs

**Estimated Effort**: 4-6 hours

#### Accessibility Review
- Keyboard navigation for all tools
- ARIA labels where appropriate
- Focus indicators
- Screen reader compatibility
- Color contrast validation

**Estimated Effort**: 3-4 hours

## Short-Term Roadmap (Phase 2)

### New Tools - HIGH VALUE

#### 1. Hash Generator
**Justification**: Core developer utility, complements existing encoding tools
**Features**:
- MD5, SHA-1, SHA-256, SHA-512 hash generation
- HMAC support with secret key input
- Text and file hashing
- Hash comparison tool
- Copy individual hashes or all at once

**Technical Approach**: Use Web Crypto API (native browser support)
**Estimated Effort**: 3-4 hours

#### 2. Unix Timestamp Converter
**Justification**: Frequently needed, simple to implement, high utility
**Features**:
- Convert Unix timestamp to human-readable date
- Convert date to Unix timestamp
- Multiple timezone displays (UTC, local, custom)
- Current timestamp display (live updating)
- Time difference calculator
- Support milliseconds and seconds

**Technical Approach**: Native JavaScript Date object
**Estimated Effort**: 2-3 hours

#### 3. Diff Checker
**Justification**: Complements text formatter, unique offering
**Features**:
- Side-by-side and inline diff views
- Character-level and line-level differences
- Syntax highlighting for code (detect language)
- Copy merged result
- Ignore whitespace option

**Technical Approach**: Use diff library (jsdiff via CDN)
**Estimated Effort**: 4-5 hours

#### 4. URL Encoder/Decoder
**Justification**: Common need, pairs well with Base64 tool
**Features**:
- Encode/decode full URLs
- Encode/decode query parameters individually
- Parse URL into components (protocol, host, path, query, hash)
- Build query strings visually (key-value pairs)
- Validate URLs

**Technical Approach**: Native URL API + encodeURIComponent
**Estimated Effort**: 2-3 hours

#### 5. Color Converter & Picker
**Justification**: Useful for frontend devs, visual tool
**Features**:
- Convert between HEX, RGB, HSL, CMYK
- Interactive color picker
- Generate color palettes (complementary, analogous, triadic)
- Accessibility contrast checker (WCAG AA/AAA)
- Save favorite colors to localStorage

**Technical Approach**: Canvas API for picker, color conversion algorithms
**Estimated Effort**: 5-6 hours

## Medium-Term Roadmap (Phase 3)

### Enhancement Projects

#### CAN Bus Analyzer - DBC File Support
**Current State**: Basic message decoding
**Enhancement**: Add custom message ID mapping
- User-defined mappings (ID → name, byte positions → values)
- Support for endianness, scaling, offsets
- **Future**: DBC file upload parsing (complex, needs library research)

**Estimated Effort**:
- Custom mappings: 4-5 hours
- DBC parsing: 8-10 hours (research + implementation)

#### Dark Mode Support
**Scope**: All tools
**Approach**:
- Add dark mode toggle (save preference to localStorage)
- Create dark theme CSS variables
- Update all tools to use theme variables
- Consider system preference detection (prefers-color-scheme)

**Estimated Effort**: 6-8 hours for all tools

#### Improved Landing Page
**Enhancements**:
- Add search/filter for tools
- Category filtering (REPL, Encoding, Text, etc.)
- "Recently Added" section
- Tool usage statistics (localStorage based)
- Quick access favorites

**Estimated Effort**: 4-5 hours

### Additional Tools - MEDIUM PRIORITY

#### Markdown Live Preview
**Features**:
- Live markdown editor with preview
- GitHub-flavored markdown support
- Syntax highlighting in code blocks
- Export as HTML
- Save drafts to localStorage

**Technical Approach**: Marked.js + Highlight.js
**Estimated Effort**: 3-4 hours

#### Cron Expression Builder
**Features**:
- Visual cron expression builder
- Show next 5-10 execution times
- Human-readable descriptions
- Common presets (daily, weekly, monthly, etc.)
- Validate expressions

**Technical Approach**: Cron parser library
**Estimated Effort**: 4-5 hours

#### UUID/GUID Generator
**Features**:
- Generate v4 UUIDs
- Bulk generation (up to 1000)
- Validate existing UUIDs
- Different formats (dashes, no dashes, uppercase)
- Copy all or individual

**Technical Approach**: Crypto.randomUUID() API
**Estimated Effort**: 2 hours

## Long-Term Ideas (Phase 4)

### Advanced Tools

#### QR Code Generator
- Generate QR codes from text/URLs
- Customizable size, colors, error correction
- Logo/image embedding
- Download as PNG/SVG

**Estimated Effort**: 4-5 hours

#### Lorem Ipsum Generator
- Generate placeholder text
- Word/paragraph/character count customization
- Different formats (plain, HTML, Markdown)
- Alternative generators (bacon ipsum, corporate ipsum)

**Estimated Effort**: 2-3 hours

#### HTML/CSS/XML Formatter
- Format and beautify code
- Minify options
- Syntax highlighting
- Validate syntax

**Estimated Effort**: 3-4 hours

#### Image Tools
- Image format converter (PNG, JPG, WebP)
- Image compression
- Resize/crop
- EXIF data viewer

**Estimated Effort**: 6-8 hours (requires canvas/image processing)

#### Network Tools
- IP address info lookup
- CIDR calculator
- MAC address lookup
- Subnet calculator

**Estimated Effort**: 4-6 hours

## Technical Debt & Maintenance

### Code Quality
- [ ] Add JSDoc comments to complex functions
- [ ] Create shared utility library for common functions (debounce, clipboard, etc.)
- [ ] Standardize error handling patterns
- [ ] Add unit tests for critical utilities (feasibility TBD)

### Performance
- [ ] Audit page load times (aim for < 1MB per tool)
- [ ] Lazy load heavy libraries (Pyodide, etc.)
- [ ] Consider service worker for offline functionality
- [ ] Optimize images/assets if any are added

### Documentation
- [x] Update README.md (COMPLETED)
- [x] Update AGENTS.md (COMPLETED)
- [x] Update HOSTING_OPTIONS.md (COMPLETED)
- [ ] Create CONTRIBUTING.md with detailed guidelines
- [ ] Add inline documentation to complex tools
- [ ] Create video/GIF demos for tools

## Success Metrics

### Usage Goals
- Target: Useful to developers and referenced in documentation
- Grow tool collection to 20+ tools
- Maintain high quality standards (no broken tools)

### Quality Standards
- All tools work on mobile (375px+)
- All tools accessible via keyboard
- No console errors on any tool
- < 2 second load time on 4G connection

### Community Goals
- Accept community contributions
- Respond to issues within 1 week
- Regular updates (monthly new tool or enhancement)

## Decision Framework

### When to Add a New Tool
✅ **Yes** if:
- Solves a common developer problem
- Complements existing tool collection
- Can be implemented client-side
- Unique or significantly better than existing tools
- Maintainable and testable

❌ **No** if:
- Requires server-side processing (unless using external API)
- Duplicates existing tool without improvement
- Too niche (< 1% of developers would use)
- Requires constant maintenance
- Security risks for users

### When to Enhance Existing Tools
**Prioritize if**:
- Fixes a bug or UX issue
- Significantly improves usability
- Adds frequently requested feature
- Improves accessibility or mobile experience

**Defer if**:
- Minor nice-to-have feature
- Adds complexity without clear benefit
- Better suited as separate tool

## Next Actions

### Immediate (This Week)
1. ✅ Fix documentation (README, AGENTS, HOSTING_OPTIONS)
2. 🔧 Fix regex tool dual-selection bug
3. 📱 Mobile responsiveness audit
4. ➕ Add Hash Generator tool
5. ➕ Add Unix Timestamp Converter tool

### Short-term (Next 2 Weeks)
1. Add Diff Checker tool
2. Add URL Encoder/Decoder tool
3. Add Color Converter & Picker
4. Accessibility review all tools
5. Update TODO.md with new items

### Medium-term (Next Month)
1. Implement dark mode across all tools
2. Enhance CAN Bus Analyzer with custom mappings
3. Improve landing page with search/filter
4. Add 3-5 more medium-priority tools
5. Create CONTRIBUTING.md

## Notes

- Keep tools simple and focused
- Prioritize quality over quantity
- Listen to user feedback (if GitHub issues are opened)
- Document decisions and patterns
- Maintain consistency across tools
- Test thoroughly before deploying

---

**Maintained by**: Claude Code
**Repository**: https://github.com/tylerstoltz/git_pages
**Live Site**: https://tylerstoltz.github.io/git_pages/
