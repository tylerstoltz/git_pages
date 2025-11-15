# TODO - Claude Code Developer Tools

**Last Updated**: 2025-11-15

This document tracks planned improvements, new tools, and known issues. See [GAMEPLAN.md](./GAMEPLAN.md) for the comprehensive roadmap.

---

## ✅ Recently Completed

### Regex Tool - Dual-Selection UX Issue
**Status**: ✅ Fixed (2025-11-15)

**Solution Implemented**:
- Removed alert-based flow that caused focus loss
- Implemented event-driven selection using mouseup listeners
- Added visual feedback with color-coded borders (green for context, blue for changing bit)
- Buttons now toggle to "Cancel Selection" allowing users to exit selection mode
- Added inline dynamic instructions during selection process
- Validates that changing bit is different from context and within context range
- Proper cleanup of event listeners to prevent memory leaks

---

### New Tools Added

#### Hash Generator
**Status**: ✅ Completed (2025-11-15)

Features implemented:
- ✅ Generate MD5, SHA-1, SHA-256, SHA-512 hashes
- ✅ HMAC support with secret key input
- ✅ Hash text input or file upload with drag-and-drop
- ✅ Hash comparison tool
- ✅ Copy individual hashes
- ✅ Output in hex or base64 format
- ✅ Auto-generate on text change (debounced)
- ✅ Mobile-responsive design

---

#### Unix Timestamp Converter
**Status**: ✅ Completed (2025-11-15)

Features implemented:
- ✅ Convert Unix timestamp → human-readable date
- ✅ Convert date → Unix timestamp
- ✅ Support both seconds and milliseconds
- ✅ Display in multiple timezones (UTC, local)
- ✅ Live current timestamp (updates every second)
- ✅ Time difference calculator
- ✅ Copy current timestamp
- ✅ Mobile-responsive design

---

#### Mobile Responsiveness Audit
**Status**: ✅ Completed (2025-11-15)

All 12 tools audited and verified:
- ✅ All tools have viewport meta tags
- ✅ All tools have responsive media queries
- ✅ Added comprehensive mobile support to SQLite Query Builder (was missing all media queries)
- ✅ Verified touch-friendly buttons (min 44px)
- ✅ Tested complex UIs (SQLite, Arduino, Regex, Python REPL)

---

## 🚀 High Priority (Next Up)

### New Tools - Essential Utilities

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
- ✅ Regex Tool - Pattern testing with dual-selection mode
- ✅ SQLite Query Builder - Visual SQL query designer
- ✅ Hash Generator - Cryptographic hashing tool
- ✅ Unix Timestamp Converter - Timestamp/date conversion
- ✅ README.md - Updated to reflect tools hub
- ✅ AGENTS.md - Updated with development guidelines
- ✅ HOSTING_OPTIONS.md - Updated repository references
- ✅ GAMEPLAN.md - Created comprehensive roadmap
- ✅ index.html footer - Fixed GitHub links
- ✅ Regex Tool Bug Fix - Fixed dual-selection UX issue
- ✅ Mobile Responsiveness - Comprehensive audit and fixes

---

## 📊 Statistics

**Current Tool Count**: 14 (+2 from previous)
**High Priority Tools**: 3
**Medium Priority Tools**: 3
**Nice to Have Tools**: 5
**Known Critical Bugs**: 0 (down from 1)
**Quality Improvements Completed**: 2

**Recent Work Completed** (2025-11-15):
- ✅ Fixed critical regex tool bug (~2 hours)
- ✅ Mobile responsiveness audit and fixes (~3 hours)
- ✅ Hash Generator tool (~3 hours)
- ✅ Unix Timestamp Converter tool (~2 hours)
Total: ~10 hours of development

**Estimated Remaining Work**:
- High Priority: ~10-15 hours
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
