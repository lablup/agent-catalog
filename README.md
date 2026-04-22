# Agent Catalog

A curated collection of agent profiles for Backend.AI products (GO, WebUI, DOL, Studio).

## Structure

```
agent-catalog/
├── index.json                          # Master index of all profiles
├── code-assistants/                    # Code writing, review, and debugging
│   ├── python-expert.json
│   ├── rust-developer.json
│   ├── web-fullstack.json
│   ├── code-reviewer.json
│   └── sql-expert.json
├── research-analysts/                  # Research, analysis, and synthesis
│   ├── academic-researcher.json
│   └── market-analyst.json
├── document-creators/                  # Documentation and content creation
│   ├── technical-writer.json
│   └── blog-author.json
├── data-analysts/                      # Data analysis and visualization
│   └── data-scientist.json
├── utilities/                          # General-purpose utility agents
│   ├── shell-commander.json
│   └── file-organizer.json
└── custom-agents/                      # Specialized and domain-specific agents
    ├── socratic-tutor.json
    ├── interview-coach.json
    ├── product-manager.json
    └── architecture-advisor.json
```

## Profile Format

Each profile is a JSON file conforming to the `AgentProfile` schema:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier |
| `name` | string | Display name |
| `description` | string | Short description |
| `version` | string | Semver version |
| `author` | string | Profile author |
| `icon` | string | Emoji or icon |
| `category` | string | One of: `code_assistant`, `research_analyst`, `document_creator`, `data_analyst`, `custom_agent`, `utility` |
| `systemPrompt` | string | System prompt defining agent behavior |
| `instructions` | string | Standing instructions for every task |
| `toolConfig` | object | Tool permissions and configuration |
| `modelPreferences` | object | Model requirements (context window, capabilities) |
| `settingsOverrides` | object | Operational settings (max iterations, timeouts) |
| `translations` | object | Per-locale translation overlays (see below) |
| `tags` | string[] | Searchable tags |

## Index Format

`index.json` contains summary metadata for all profiles:

```json
{
  "version": 1,
  "updatedAt": "2026-02-23T00:00:00Z",
  "profiles": [
    {
      "path": "code-assistants/python-expert.json",
      "name": "Python Expert",
      "description": "...",
      "category": "code_assistant",
      "author": "Lablup",
      "icon": "🐍",
      "tags": ["python", "coding"],
      "version": "1.0.0"
    }
  ]
}
```

## Translations

Profiles support multilingual content via the `translations` field. Base fields (`name`, `description`, `systemPrompt`, `instructions`) remain in English, with per-locale overrides:

```json
{
  "translations": {
    "ko": {
      "name": "Python 전문가",
      "description": "관용적인 Python, 타입 힌트에 특화된 시니어 Python 개발자입니다."
    },
    "ja": {
      "name": "Pythonエキスパート"
    }
  }
}
```

- Locale keys use IETF BCP 47 format (`"ko"`, `"ja"`, `"zh-Hans"`)
- All translation fields are optional — missing fields fall back to the English base
- At minimum, provide `name` and `description` for each locale

## Contributing

1. Create a profile JSON file in the appropriate category directory
2. Add an entry to `index.json`
3. Submit a pull request

### Guidelines

- Profiles must validate against the `AgentProfile` schema
- System prompts should be comprehensive (200+ words)
- Include meaningful tags for discoverability
- Use `isCommunity: true` for community-contributed profiles
- Test your profile by importing it in Backend.AI GO

## License

Apache 2.0
