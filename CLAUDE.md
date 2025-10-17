# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Fānyì (翻译) is a command-line Chinese-English translator powered by iciba.com and DeepSeek AI. It provides bidirectional translation between Chinese and English with colorful gradient output and search history functionality.

## Development Commands

```bash
# Run tests with 20s timeout for API calls
npm test
# or with specific timeout
vitest run --test-timeout=20000

# Run tests with coverage
npm run coverage

# Lint code
npm run lint

# Format code
npm run format

# Run lint-staged (used in pre-commit hooks)
npm run lint-staged
```

## Architecture

The project uses ES modules (.mjs) throughout and has a simple modular structure:

- **bin/fanyi.mjs** - CLI entry point using Commander.js, handles argument parsing and subcommands
- **index.mjs** - Main translation logic, orchestrates iciba and LLM API calls
- **lib/config.mjs** - Configuration management with JSON file storage in ~/.config/fanyi/.fanyirc
- **lib/iciba.mjs** - iciba.com API integration and formatted output
- **lib/searchHistory.mjs** - Search history storage and retrieval
- **lib/utils.mjs** - Utility functions

## Translation Sources

1. **iciba.com** - Traditional dictionary API with phonetic symbols, parts of speech, and example sentences
2. **DeepSeek AI** - LLM-based translation with customizable prompts (supports OpenAI-compatible APIs)

## Configuration

The app supports global configuration via `fanyi config set` commands:
- `color` - Enable/disable colorful gradient output
- `iciba` - Enable/disable iciba.com translations
- `llm` - Enable/disable LLM translations
- `LLM_API_KEY` - API key for LLM service
- `LLM_API_BASE_URL` - Custom API endpoint
- `LLM_MODEL_ID` - Model identifier

## Key Dependencies

- **commander** - CLI argument parsing
- **chalk** - Terminal colors
- **gradient-string** - Gradient text effects
- **ora** - Loading spinners
- **openai** - LLM API client
- **fast-xml-parser** - iciba XML response parsing
- **node-fetch** - HTTP requests

## Testing

Tests use Vitest and run CLI commands as child processes. Key test scenarios:
- Translation output validation
- Configuration management
- Help text snapshots
- Error handling for network failures

## Code Style

- Biome.js for linting and formatting
- 2-space indentation
- 100-character line width
- Single quotes for strings
- ES modules syntax throughout