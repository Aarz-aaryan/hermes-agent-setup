# Hermes Agent Setup Backup

This repository contains a complete backup of the Hermes Agent multi-agent setup from `~/.hermes/`.

## What is Hermes Agent?

Hermes Agent is a multi-agent AI system powered by the Hermes framework. It uses skill-based architecture where each capability is defined as a portable SKILL.md file. Multiple profiles allow different personalities and configurations.

## Repository Structure

```
hermes-agent-setup/
├── README.md                        # This file
├── config.yaml                      # Root Hermes configuration
├── profiles/
│   ├── aarz/                        # Primary profile (Aarz)
│   │   ├── config.yaml              # Profile configuration
│   │   ├── SOUL.md                  # Profile identity & values
│   │   └── AGENTS.md                # Agent definitions
│   ├── bymax/                       # Profile (Bymax)
│   │   ├── config.yaml
│   │   ├── SOUL.md
│   │   └── AGENTS.md
│   ├── jarvis/                      # Profile (Jarvis)
│   │   ├── config.yaml
│   │   ├── SOUL.md
│   │   └── AGENTS.md
│   └── nina/                        # Profile (Nina)
│       ├── config.yaml
│       ├── SOUL.md
│       └── AGENTS.md
└── skills/                          # 94 skill files across categories:
    ├── agent-delegation-protocol/   # Multi-agent coordination
    ├── autonomous-ai-agents/       # Agent frameworks
    ├── composio/                    # Composio integration
    ├── creative/                    # Image, video, design tools
    ├── data-science/                # Jupyter, data analysis
    ├── devops/                      # Kanban, webhooks, CI/CD
    ├── dogfood/                     # QA testing
    ├── email/                       # Email clients
    ├── embedded-linux/              # Linux kernel, buildroot
    ├── embedded-systems/            # Arduino, STM32, ESP32, etc.
    ├── gaming/                      # Minecraft, Pokemon emulators
    ├── github/                      # GitHub workflows
    ├── media/                       # YouTube, Spotify, GIFs
    ├── mcp/                         # MCP client
    ├── mlops/                       # Training, inference, evaluation
    ├── native-mcp/                  # MCP integration
    ├── note-taking/                 # Obsidian, notes
    ├── productivity/                # Airtable, Linear, maps
    ├── red-teaming/                # Security testing
    ├── research/                    # Arxiv, papers, wikis
    ├── security/                    # CodeQL, nmap, reverse eng.
    ├── social-media/               # Social tools
    └── software-development/       # Dev workflows
```

## What is Backed Up

- **Root config**: `~/.hermes/config.yaml` - global Hermes settings
- **Profile configs**: For each of 4 profiles (aarz, bymax, jarvis, nina):
  - `config.yaml` - profile settings
  - `SOUL.md` - identity, values, and personality
  - `AGENTS.md` - agent definitions
- **All 94 skills**: Every `SKILL.md` file under `~/.hermes/skills/`

## What is NOT Backed Up (by design)

The following are intentionally excluded - they contain user-specific, ephemeral, or sensitive data:

- `sessions/` - conversation histories
- `memories/` - persistent memory data
- `logs/` - runtime logs
- `state.db` - SQLite state database
- `auth.json` - authentication tokens
- `cache/` - cached data
- `images/` - generated images
- `sandboxes/` - sandbox state
- `kanban.db` - Kanban board state
- `checkpoints/` - runtime checkpoints
- `processes.json` - process state
- `.env` files - environment variables and secrets
- Any Composio API keys (redacted to `YOUR_COMPOSIO_API_KEY`)

## How to Restore

### 1. Clone this repository
```bash
git clone https://github.com/Aarz-aaryan/hermes-agent-setup.git ~/.hermes-backup
```

### 2. Restore configurations
```bash
# Restore root config
cp ~/.hermes-backup/config.yaml ~/.hermes/config.yaml

# Restore all profiles
for profile in aarz bymax jarvis nina; do
    mkdir -p ~/.hermes/profiles/$profile
    cp ~/.hermes-backup/profiles/$profile/config.yaml ~/.hermes/profiles/$profile/
    cp ~/.hermes-backup/profiles/$profile/SOUL.md ~/.hermes/profiles/$profile/
    cp ~/.hermes-backup/profiles/$profile/AGENTS.md ~/.hermes/profiles/$profile/
done

# Restore all skills
cp -r ~/.hermes-backup/skills/* ~/.hermes/skills/
```

### 3. Reconfigure credentials
After restoring, you will need to:
1. Add your Composio API key to `~/.hermes/profiles/aarz/config.yaml`
2. Re-authenticate any connected services (GitHub, Gmail, etc.)
3. Review `config.yaml` for any other API keys/secrets that need restoring

## Profile Descriptions

| Profile | Description |
|---------|-------------|
| `aarz` | Primary profile for user Aarz (main Composio connection) |
| `bymax` | Secondary profile |
| `jarvis` | Assistant-style profile |
| `nina` | Alternative profile |

## Skill Categories

- **Agent Frameworks**: agent-delegation-protocol, subagent-driven-development
- **Creative**: ComfyUI, architecture diagrams, slide decks, screenshot tools
- **Data Science**: Jupyter notebooks, data analysis
- **DevOps**: Kanban orchestration, webhook subscriptions
- **Embedded Systems**: Arduino, STM32, ESP32, Raspberry Pi Pico, baremetal C
- **Gaming**: Minecraft servers, Pokemon emulation
- **GitHub**: PR workflows, issue management, code review, repo management
- **LLM/MLOps**: llama.cpp, vllm, axolotl, unsloth, DSPy, HuggingFace
- **Media**: YouTube, Spotify, GIF search, audio analysis
- **MCP**: Native MCP client configuration
- **Productivity**: Airtable, Linear, maps, PDF tools, OCR
- **Research**: Arxiv papers, blog watching, wiki tools
- **Software Dev**: Systematic debugging, TDD, code review, spike investigations

## Notes

- This backup was created via the Hermes Agent Composio GitHub integration
- 94 skill files backed up preserving full directory structure
- All file contents are sourced directly from `~/.hermes/` on the host system
- API keys and secrets are redacted to placeholder values
