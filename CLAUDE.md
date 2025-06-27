# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Claude Chat Exporter is a browser-based JavaScript utility that exports Claude AI conversations to Markdown format. It's a single-file, dependency-free script that runs in the browser's developer console.

## Architecture

This is a simple, functional JavaScript application with no build process or external dependencies:

- **Main file**: `claude-chat-exporter.js` - Contains all functionality
- **Execution model**: Copy-paste into browser console for immediate execution
- **Output**: Downloads `claude_conversation.md` via browser's Blob API

### Core Functions

1. **`extractConversation()`** - Main orchestrator that scans DOM for messages using CSS selectors `.font-claude-message` and `.font-user-message`
2. **`processContent(element, depth)`** - Recursive HTML-to-Markdown converter handling paragraphs, lists, and code blocks
3. **`processList(listElement, listType, depth)`** - Handles nested list structures with proper indentation
4. **`processInlineElements(element)`** - Processes inline code and text formatting
5. **`downloadMarkdown(content, filename)`** - Creates downloadable file using Blob API

### DOM Dependencies

The script relies on specific CSS selectors from Claude's web interface:
- `.font-claude-message` - Claude's responses
- `.font-user-message` - Human messages
- `.grid-cols-1` - Content container for Claude messages
- `language-*` classes on code blocks for syntax highlighting

## Development Workflow

This project provides two deployment options:

### Console Script (`claude-chat-exporter.js`)
- **No package manager** - No `package.json`, dependencies, or node_modules
- **No build tools** - Direct JavaScript execution
- **Manual execution** - Copy-paste into browser console

### Userscript (`claude-chat-exporter.user.js`)
- **Browser extension required** - Tampermonkey, Greasemonkey, or similar
- **Automatic loading** - Runs on `claude.ai/*` pages
- **UI integration** - Adds floating export button to page
- **Error handling** - Includes try-catch and user feedback

## Installation

### Console Script
1. Open Claude conversation in browser
2. Open developer console
3. Paste the entire `claude-chat-exporter.js` content
4. Press Enter to execute

### Userscript
1. Install Tampermonkey or Greasemonkey browser extension
2. Click "Create new script" or drag `claude-chat-exporter.user.js` to extension
3. Save the script
4. Visit any Claude conversation page
5. Click the "📄 Export Chat" button in the top-right corner

## Testing

### Console Script
1. Open a Claude conversation in browser
2. Open developer console
3. Paste the script content
4. Verify the Markdown download contains properly formatted content

### Userscript
1. Install script in userscript manager
2. Navigate to claude.ai conversation
3. Verify export button appears
4. Click button and verify download

## Key Considerations

- **Interface fragility**: Script depends on Claude's current DOM structure and CSS classes
- **No error handling**: Will break silently if interface changes
- **Browser compatibility**: Uses modern JavaScript APIs (querySelectorAll, Blob, URL.createObjectURL)
- **Single execution**: Script runs once and downloads immediately

## Maintenance Notes

When Claude's interface changes, likely failure points:
- CSS selector changes for message identification
- DOM structure changes affecting content extraction
- Code block language detection via className patterns