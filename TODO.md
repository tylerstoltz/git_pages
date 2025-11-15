# TODO - Claude Code Developer Tools

**Last Updated**: 2025-11-15

This document tracks planned improvements, new tools, and known issues. See [GAMEPLAN.md](./GAMEPLAN.md) for the comprehensive roadmap.

---

## 🐛 Critical Bugs (Must Fix)

### Regex Tool - Dual-Selection UX Issue
**Status**: 🔴 Critical - Blocking normal usage

**Problem**: The Pattern Generator's dual-selection mode has broken UX flow:
- If user selects context block first, then clicks "Select Context", they're still prompted to select context
- If user clicks "Select Context" first, instructions appear in wrong order
- In the "Select Changing Bit" step, instructions follow the correct action but the tool always behaves as though the user selected the exact same thing for both Context and Changing Bit

**Example Use Case**:
```
Context Block (full selection):
Order ID: 12345 Date: 2023-10-01
Order ID: 67890 Date: 2023-10-02
Order ID: 54321 Date: 2023-10-03

Changing Bit (highlight within context):
12345, 67890, 54321 (the order IDs)

Expected Output:
Order ID: (\d+) Date:
```

**Current Behavior**: Both selections treated as identical, pattern generation fails

**Fix Required**:
- Review selection state management
- Fix instruction sequencing logic
- Ensure independent tracking of context vs. changing bit
- Add clear visual feedback for each selection step
- Test with all examples from original TODO

---

## 🚀 High Priority (Next Up)

### New Tools - Essential Utilities

#### Hash Generator
**Priority**: ⭐⭐⭐ High
**Estimated Effort**: 3-4 hours

Essential developer tool for security and data integrity.

**Features**:
- Generate MD5, SHA-1, SHA-256, SHA-512 hashes
- HMAC support with secret key input
- Hash text input or file upload
- Hash comparison tool (compare two hashes)
- Copy individual hashes or export all
- Show hash in different formats (hex, base64)

**Technical Notes**: Use Web Crypto API (native browser support, no external libraries needed)

---

#### Unix Timestamp Converter
**Priority**: ⭐⭐⭐ High
**Estimated Effort**: 2-3 hours

Frequently needed by backend developers and API testers.

**Features**:
- Convert Unix timestamp → human-readable date
- Convert date → Unix timestamp
- Support both seconds and milliseconds
- Display in multiple timezones (UTC, local, custom)
- Live current timestamp (updates every second)
- Time difference calculator (between two timestamps)
- Copy in various formats

**Technical Notes**: Native JavaScript Date object, no libraries needed

---

#### Diff Checker
**Priority**: ⭐⭐⭐ High
**Estimated Effort**: 4-5 hours

Unique offering that complements text formatter.

**Features**:
- Side-by-side diff view
- Inline diff view (unified)
- Character-level differences
- Line-level differences
- Syntax highlighting for code (auto-detect language)
- Ignore whitespace option
- Copy merged result
- Stats (lines added/removed/changed)

**Technical Notes**: Use `jsdiff` library via CDN

---

#### URL Encoder/Decoder
**Priority**: ⭐⭐⭐ High
**Estimated Effort**: 2-3 hours

Pairs well with Base64 tool, common developer need.

**Features**:
- Encode/decode full URLs
- Encode/decode individual query parameters
- Parse URL into components (protocol, host, port, path, query, hash)
- Visual query string builder (add/remove key-value pairs)
- Validate URL format
- Handle special characters correctly

**Technical Notes**: Native URL API + encodeURIComponent/decodeURIComponent

---

#### Color Converter & Picker
**Priority**: ⭐⭐ Medium-High
**Estimated Effort**: 5-6 hours

Valuable for frontend developers and designers.

**Features**:
- Convert between HEX, RGB, RGBA, HSL, HSLA, CMYK
- Interactive color picker (hue, saturation, lightness sliders)
- Generate color palettes:
  - Complementary
  - Analogous
  - Triadic
  - Monochromatic
- Accessibility contrast checker (WCAG AA/AAA compliance)
- Save favorite colors to localStorage
- Copy in any format

**Technical Notes**: Canvas API for picker, color conversion math, contrast ratio algorithm

---

### Quality Improvements

#### Mobile Responsiveness Audit
**Priority**: ⭐⭐⭐ High
**Estimated Effort**: 4-6 hours

Ensure all tools work well on mobile devices.

**Checklist**:
- [ ] Test all 12 tools at 375px width (iPhone SE)
- [ ] Test at 768px width (tablets)
- [ ] Fix any layout overflow issues
- [ ] Ensure buttons are touch-friendly (min 44px)
- [ ] Test complex UIs:
  - [ ] SQLite Query Builder (multi-panel)
  - [ ] Arduino Simulator (visual board)
  - [ ] Python REPL (loading states)
  - [ ] Regex Tool (dual panels)
- [ ] Test input fields with on-screen keyboard
- [ ] Verify copy/paste on mobile

---

#### Accessibility Review
**Priority**: ⭐⭐ Medium-High
**Estimated Effort**: 3-4 hours

Make tools accessible to all users.

**Checklist**:
- [ ] Keyboard navigation (Tab, Enter, Esc)
- [ ] ARIA labels for controls
- [ ] Focus indicators (visible outline)
- [ ] Screen reader compatibility
- [ ] Color contrast validation (4.5:1 minimum)
- [ ] Skip to main content links
- [ ] Form field labels properly associated
- [ ] Error messages announced to screen readers

---

## 📋 Medium Priority

### Tool Enhancements

#### CAN Bus Analyzer - Custom Mapping
**Priority**: ⭐⭐ Medium
**Estimated Effort**: 4-5 hours

Add user-defined message ID mapping (DBC parsing is future consideration).

**Features**:
- Define message ID → name mappings (e.g., `0x123` → `EngineData`)
- Define byte positions → value names with transformations
- Support for:
  - Endianness (big/little)
  - Scaling (multiply by factor)
  - Offset (add/subtract value)
  - Signed/unsigned integers
- Save/load mapping configurations (localStorage)
- Example mapping templates

**Example**:
```
Input: 0x123#0x11 0xFF 0x33
Mapping:
  ID 0x123 = "EngineData"
  Byte 1 (0xFF) = "Temperature" (unsigned, -40°C offset)
  Byte 2 (0x33) = "RPM" (unsigned, *10 multiplier)
Output: EngineData#Temperature: 215°C RPM: 510
```

**Future**: DBC file upload/parsing (complex, requires research - estimated 8-10 hours)

---

#### Dark Mode Support
**Priority**: ⭐⭐ Medium
**Estimated Effort**: 6-8 hours (all tools)

Add dark mode toggle across all tools.

**Approach**:
- Create CSS custom properties for theming
- Add toggle button (moon/sun icon)
- Save preference to localStorage
- Consider system preference detection (`prefers-color-scheme`)
- Ensure good contrast in both modes
- Update each tool's styling

**Color Scheme**:
- Light: Current purple gradient, white cards
- Dark: Dark purple/gray gradient, dark cards with light text

---

### New Tools - Medium Priority

#### Markdown Live Preview
**Estimated Effort**: 3-4 hours

**Features**:
- Split-pane live editor with preview
- GitHub-flavored markdown support
- Syntax highlighting in code blocks
- Table support
- Emoji support
- Export as HTML
- Save drafts to localStorage
- Word/character count

**Technical**: Marked.js + Highlight.js via CDN

---

#### Cron Expression Builder
**Estimated Effort**: 4-5 hours

**Features**:
- Visual builder with dropdowns (minute, hour, day, month, weekday)
- Show generated cron expression
- Display next 5-10 execution times
- Human-readable description
- Common presets (every minute, hourly, daily, weekly, monthly, yearly)
- Validate custom expressions
- Copy expression

**Technical**: Cron parser library (e.g., cron-parser via CDN)

---

#### UUID/GUID Generator
**Estimated Effort**: 2 hours

**Features**:
- Generate single v4 UUID
- Bulk generation (1-1000 UUIDs)
- Different formats:
  - With dashes: `550e8400-e29b-41d4-a716-446655440000`
  - Without dashes: `550e8400e29b41d4a716446655440000`
  - Uppercase/lowercase options
- Validate existing UUIDs
- Copy all or individual
- Timestamp-based UUIDs (v1) option

**Technical**: `crypto.randomUUID()` API (native browser support)

---

## 💡 Nice to Have (Future)

### Additional Tools

#### QR Code Generator
**Estimated Effort**: 4-5 hours

- Generate QR codes from text/URLs
- Customizable size, error correction level
- Color customization (foreground/background)
- Download as PNG or SVG
- Optional logo/image embedding

---

#### Lorem Ipsum Generator
**Estimated Effort**: 2-3 hours

- Generate placeholder text
- Customize word/paragraph/character count
- Different formats (plain text, HTML paragraphs, Markdown)
- Alternative generators (bacon ipsum, corporate speak, hipster ipsum)

---

#### HTML/CSS/XML Formatter
**Estimated Effort**: 3-4 hours

- Format/beautify HTML, CSS, XML
- Minify option
- Syntax highlighting
- Validate syntax
- Show error locations

---

#### Image Tools
**Estimated Effort**: 6-8 hours

- Image format converter (PNG ↔ JPG ↔ WebP)
- Image compression with quality slider
- Resize/crop with preview
- EXIF data viewer
- Batch processing

**Technical**: Canvas API, FileReader API

---

#### Network/IP Tools
**Estimated Effort**: 4-6 hours

- IP address info (lookup via API)
- CIDR calculator
- Subnet calculator
- MAC address lookup (vendor)
- IP range calculator

---

### Landing Page Improvements
**Estimated Effort**: 4-5 hours

**Features**:
- Search/filter tools by name or description
- Category filtering (REPL, Encoding, Text, etc.)
- "Recently Added" badge on new tools
- Tool usage tracking (localStorage)
- Favorites/quick access
- Total tool count display
- Link to GAMEPLAN and TODO

---

## 📚 Documentation & Maintenance

### Documentation Tasks
- [ ] Create CONTRIBUTING.md with detailed guidelines
- [ ] Add inline code documentation to complex tools
- [ ] Create video/GIF demos for tools
- [ ] Add "How to Use" section to each tool
- [ ] Document common patterns in AGENTS.md

### Code Quality
- [ ] Add JSDoc comments to complex functions
- [ ] Create shared utility library (`utils.js`)
  - Debounce function
  - Clipboard helper
  - Toast notification
  - LocalStorage wrapper
  - Theme manager
- [ ] Standardize error handling patterns
- [ ] Consider adding unit tests (feasibility TBD)

### Performance
- [ ] Audit page load times (< 1MB per tool)
- [ ] Lazy load heavy libraries
- [ ] Consider service worker for offline
- [ ] Optimize any images/assets
- [ ] Minify CSS/JS if files get large

---

## ✅ Completed

- ✅ Text Formatter - Multi-line text transformation tool
- ✅ Hex ↔ Decimal Converter - Number system converter
- ✅ CAN Bus Analyzer - Basic message decoder
- ✅ Token Counter - LLM token counting and cost estimation
- ✅ JSON Formatter - Validate, format, minify JSON
- ✅ Base64 Tool - Encode/decode with file support
- ✅ JWT Cookie Inspector - Decode JWT tokens
- ✅ JavaScript REPL - Browser-based JS execution
- ✅ Python REPL - Pyodide-powered Python in browser
- ✅ Arduino Simulator - Virtual Arduino UNO
- ✅ Regex Tool - Pattern testing (has UX bug to fix)
- ✅ SQLite Query Builder - Visual SQL query designer
- ✅ README.md - Updated to reflect tools hub
- ✅ AGENTS.md - Updated with development guidelines
- ✅ HOSTING_OPTIONS.md - Updated repository references
- ✅ GAMEPLAN.md - Created comprehensive roadmap
- ✅ index.html footer - Fixed GitHub links

---

## 📊 Statistics

**Current Tool Count**: 12
**High Priority Tools**: 5
**Medium Priority Tools**: 3
**Nice to Have Tools**: 5
**Known Critical Bugs**: 1
**Quality Improvements Needed**: 2

**Estimated Work**:
- Critical Bugs: 2-3 hours
- High Priority: ~20-25 hours
- Medium Priority: ~15-20 hours
- Nice to Have: ~25-35 hours

---

## Decision Criteria

### Add a New Tool if:
- ✅ Solves common developer problem
- ✅ Complements existing collection
- ✅ Client-side implementation possible
- ✅ Unique or significantly better than alternatives
- ✅ Maintainable long-term

### Prioritize Enhancement if:
- ✅ Fixes bug or UX issue
- ✅ Significantly improves usability
- ✅ Addresses frequent user need
- ✅ Improves accessibility/mobile experience

---

**See Also**:
- [GAMEPLAN.md](./GAMEPLAN.md) - Comprehensive roadmap and strategy
- [AGENTS.md](./AGENTS.md) - Development guidelines and best practices
- [README.md](./README.md) - Project overview and getting started
- [HOSTING_OPTIONS.md](./HOSTING_OPTIONS.md) - GitHub Pages hosting info
