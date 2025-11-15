# TODO List for New Tools and Features

~~Can we add a new tool to our repo that's a website hosted on GitHub pages for text / code formatting? It should be similar to our REPLs with a multiline text input box at the top and an output box below with several transform operations - i.e. "convert multiline to single line", "replace line breaks with newline characters", "remove spaces", "find and replace" (incl. delimieter" and any other useful tools for a coder who needs to quickly modify text or data!~~


## This one needs work!

### There is an issue with the dual selection! - The user selects the Context Block first, then clicks "Select Context" but is prompted with the instructions to select context.  If they click "Select Context" first, it instructs them to select context first.  Also in the "Select Changing Bit" step, the instructions follow the correct action in the same fashion, but always behaves as though the user selected the exact same thing for Context and Changing Bit.

Can we modify the existing regex tool in our repo (that's a website hosted on GitHub pages) "Pattern Generator" to have a dual-selection mode where the user can select a block of text for context (with both changing and unchanging bits) and then select a section of that text that is the changing bit (field they want to extract) and have the tool generate a regex pattern that captures just that changing bit based on the context of the full block of text? For example, if the user inputs:

```
Order ID: 12345 Date: 2023-10-01
Order ID: 67890 Date: 2023-10-02
Order ID: 54321 Date: 2023-10-03
```
They can select the entire lines as context and then select just the numbers as the changing bit, and the tool would generate a regex pattern like `Order ID: (\d+)` to capture just the order IDs. This would help users quickly create regex patterns for extracting specific data from structured text!

Or:

```
Order ID: 12345 Date: 2023-10-01
Order ID: 67890 Date: 2023-10-02
Order ID: 54321 Date: 2023-10-03
```
They can select the entire lines as context and then select just the dates as the changing bit, and the tool would generate a regex pattern like `Date: (\d{4}-\d{2}-\d{2})` to capture just the dates. This would help users quickly create regex patterns for extracting specific data from structured text!  

Or:

```
Order ID: 12345 Date: 2023-10-01
Order ID: 67890 Date: 2023-10-02
Order ID: 54321 Date: 2023-10-03
```
They can select the entire lines as context and then select just `Order ID: 12345 Date:` as the changing bit, and the tool would generate a regex pattern like `(Order ID: \d+ Date:)` to capture just that specific segment. This would help users quickly create regex patterns for extracting specific data from structured text!


---

Hex <-> >decimal converter tool: A simple web-based tool that allows users to input hexadecimal values and converts them to decimal format. This would be useful for developers and programmers who frequently work with different numeral systems.

---

~~CAN bus protocol analyzer: A web-based tool that can decode and analyze CAN bus messages. Users can input raw CAN bus data, and the tool will parse it to display meaningful information such as message IDs, data length, and payload content. This would be particularly useful for automotive engineers and developers working with embedded systems.~~

---

### File upload is not supported - site is hosted on github pages.

CAN bus message analyzer - add optional mapping functionality: Users can enter a mapping of message IDs to human-readable names and payload values such that when the user defines `0x123#0x11 0xF2 0x33` it shows `EngineData#Temperature: 242 RPM: 51` based on the mapping provided by the user. Mappings shoud support addition, endianness and be flexible enough such that: `0x123#0x11 0xFF 0x33` could alternatively be mapped to `EngineData#Temperature: 272 RPM: 51` all completelybased on user-defined mapping rules.
If possible, support upload /paste a DBC file and have it parse the DBC file to get the mapping automatically.

---



    ~~LLM Token Counter & Analyzer
        Count tokens for different models (OpenAI, Claude, Llama, etc.)
        Show character count, word count, token count
        Estimate API costs based on model pricing
        Highlight token boundaries visually
        Very relevant given the AI/Claude theme~~
        
    ~~JSON Formatter & Validator
        Format/minify JSON
        Validate syntax with error highlighting
        Tree view for exploring nested structures
        Convert to/from other formats (YAML, XML)~~

    ~~Base64 Encoder/Decoder
        Encode/decode text and files
        Support for URL-safe Base64
        Image preview for decoded images
        Common developer utility~~

    Hash Generator
        Generate MD5, SHA-1, SHA-256, SHA-512 hashes
        HMAC support
        File hashing capability
        Compare hashes

    ~~JWT Decoder & Debugger
        Decode JWT tokens
        Validate signatures
        Show header, payload, and signature clearly
        Highlight expiration time~~

Medium Priority

    Unix Timestamp Converter
        Convert between Unix timestamps and human-readable dates
        Show multiple timezone conversions
        Calculate time differences

    Color Converter & Picker
        Convert between HEX, RGB, HSL, CMYK
        Color picker with live preview
        Generate color palettes
        Accessibility contrast checker

    Diff Checker
        Side-by-side or inline diff view
        Syntax highlighting for code
        Character-level and line-level diffs

    Markdown Live Preview
        Live markdown editor with preview
        Support GitHub-flavored markdown
        Export as HTML
        Syntax highlighting for code blocks

    URL Encoder/Decoder
        Encode/decode URLs and query parameters
        Parse URLs into components
        Build query strings visually

Nice to Have

    Cron Expression Builder
        Visual cron expression builder
        Show next execution times
        Human-readable descriptions

    Lorem Ipsum Generator
        Generate placeholder text
        Customizable word/paragraph counts
        Different formats (HTML, Markdown)

    QR Code Generator
        Generate QR codes from text/URLs
        Customizable size and colors
        Download as PNG/SVG

    UUID/GUID Generator
        Generate v4 UUIDs
        Bulk generation
        Validate existing UUIDs

    HTML/CSS/XML Formatter
        Format and beautify code
        Minify options
        Syntax highlighting

