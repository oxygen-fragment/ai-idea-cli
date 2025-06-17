# idea-cli: AI-Driven SDLC Engine

Transform project ideas into production-ready codebases through intelligent validation, planning, and automated implementation with comprehensive demo mode for immediate usage.

## 🚀 Key Features

- **🎭 Demo Mode**: Immediate usage without API keys - try all features with fallback implementations
- **🔍 Idea Validation**: Critical idea validation with external API integration and business viability scoring
- **🎯 Enhanced Planning**: AI-powered feature breakdown into epics and implementable stories
- **🏗️ Smart Scaffolding**: Language-aware project generation (Python/Node.js) with comprehensive templates
- **🔄 Micro-Prompt Queue**: Test-driven development automation with multi-provider LLM support
- **📊 Experience Learning**: Automatic failure analysis and guard-rail generation from development experiences
- **🐛 Issue Reporting**: Automated GitHub issue creation with system diagnostics and log collection
- **🔧 Configuration Management**: JSON schema validation with user-friendly setup

## Quick Start (Zero Configuration Required)

### 1. Installation

```bash
git clone https://github.com/anthropics/idea-cli.git
cd idea-cli
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -e .
```

### 2. Try Demo Mode Immediately

```bash
# Initialize configuration (enables demo mode by default)
idea init-config

# Validate an idea (demo mode)
idea validate "AI-powered task management CLI"

# Create a project (demo mode)
idea new "AI-powered task management CLI" --dry-run
```

✅ **Success check**: All commands work immediately with demo responses and guidance

### 3. Upgrade to Full Features (Optional)

```bash
# Edit configuration file
nano ~/.idea-cli/config.json

# Set your API keys and disable demo mode:
{
  "demoMode": false,
  "validator": {
    "apiKeyEnv": "VALIDATOR_API_KEY"
  },
  "models": {
    "apiKeyEnv": "ANTHROPIC_API_KEY"
  }
}

# Set environment variables
export ANTHROPIC_API_KEY="your_claude_key"
export VALIDATOR_API_KEY="your_validator_key"
```

## Command Reference

### Essential Commands

| Command | Purpose | Demo Mode | Full Mode |
|---------|---------|-----------|-----------|
| `idea init-config` | Initialize user configuration | ✅ Always works | ✅ Creates config file |
| `idea validate` | Validate project idea | ✅ Demo validation | ✅ Real API validation |
| `idea new` | Create scaffolded project | ✅ Basic template | ✅ AI-enhanced planning |
| `idea report-issue` | Report bugs automatically | ✅ Manual instructions | ✅ GitHub CLI integration |

### Advanced Commands (Full Mode Only)

| Command | Purpose | Requirements |
|---------|---------|--------------|
| `idea run-queue` | Execute implementation queue | LLM API key |
| `idea queue-status` | Show queue progress | Project with queue |
| `idea experience collect` | Log development failure | Project directory |
| `idea experience summarise` | Generate lessons from failures | LLM API key |
| `idea upgrade` | Apply lessons as guard-rails | Project directory |

### Command Options

| Option | Purpose | Example |
|--------|---------|---------|
| `--dry-run` | Preview without execution | `idea new "test" --dry-run` |
| `--demo` | Force demo mode | `idea new "test" --demo` |
| `--skip-validation` | Bypass idea validation | `idea new "test" --skip-validation` |
| `--project-dir` | Specify project directory | `idea run-queue --project-dir ./my-project` |

## Architecture Overview

### Demo Mode vs Full Mode

**Demo Mode** (Default - No API keys required):
- ✅ Immediate usage for testing and exploration
- ✅ All CLI commands functional with fallback responses
- ✅ Basic project scaffolding with "hello world" templates
- ✅ Clear upgrade paths and configuration guidance
- ✅ Issue reporting with manual instructions

**Full Mode** (API keys configured):
- 🚀 Real idea validation with business scoring
- 🚀 AI-enhanced planning with detailed breakdowns
- 🚀 Complete TDD implementation cycle
- 🚀 Automatic lesson generation and guard-rail updates
- 🚀 Automated GitHub issue reporting

### How It Works

#### 1. **Configuration Stage**
- JSON schema validation ensures configuration integrity
- User config stored in `~/.idea-cli/config.json`
- Auto-detection of demo mode vs full mode based on API key availability

#### 2. **Validation Stage**
- **Demo Mode**: Provides neutral scoring with upgrade guidance
- **Full Mode**: Real validation using external validator API with business viability scoring
- Configurable score thresholds and acceptance criteria

#### 3. **Planning Stage**
- **Demo Mode**: Basic project structure with common patterns
- **Full Mode**: AI-powered breakdown into epics and implementable stories
- Technology stack recommendations based on idea analysis

#### 4. **Implementation Stage**
- **Demo Mode**: Static templates with development guidance
- **Full Mode**: Micro-prompt queue drives TDD implementation
- Support for multiple LLM providers (Anthropic Claude, OpenAI GPT)

#### 5. **Learning Stage**
- Experience collection from development failures
- AI summarization into actionable lessons
- Auto-generated guard-rails from lessons

## Configuration

### User Configuration (`~/.idea-cli/config.json`)

```json
{
  "validator": {
    "endpoint": "https://api.example.com/validate",
    "apiKeyEnv": "VALIDATOR_API_KEY",
    "acceptField": "accepted",
    "scoreField": "score",
    "minScore": 0.7
  },
  "models": {
    "plan": "claude-3-5-sonnet-20241022",
    "queue": "claude-3-5-sonnet-20241022",
    "summarise": "claude-3-5-sonnet-20241022",
    "apiKeyEnv": "ANTHROPIC_API_KEY"
  },
  "scaffold": {
    "templateVersion": "main"
  },
  "retentionDays": 30,
  "demoMode": true
}
```

### Environment Variables

| Variable | Purpose | Required For |
|----------|---------|--------------|
| `ANTHROPIC_API_KEY` | Claude API access | Planning, queue execution, summarization |
| `OPENAI_API_KEY` | OpenAI API access | Alternative to Claude |
| `VALIDATOR_API_KEY` | Custom validator API | Real idea validation |

### Supported LLM Providers

**Anthropic Claude:**
- Models: `claude-3-5-sonnet-20241022`, `claude-3-haiku-20240307`
- Install: `pip install anthropic`

**OpenAI GPT:**
- Models: `gpt-4`, `gpt-3.5-turbo`
- Install: `pip install openai`

## Project Structure

```
idea-cli/
├── idea/                          # Core package
│   ├── cli.py                     # Main CLI with global error handling
│   ├── config.py                  # Configuration management with JSON schema
│   ├── demo.py                    # Demo mode implementations
│   ├── validator.py               # Idea validation with demo support
│   ├── llm.py                     # Multi-provider LLM integration
│   ├── issue_reporter.py          # GitHub issue reporting
│   ├── planner.py                 # AI-powered planning
│   ├── queue.py                   # Queue management
│   ├── runner.py                  # Story implementation engine
│   ├── experience.py              # Learning system
│   └── scaffold/                  # Project scaffolding
│       ├── python.py              # Python project scaffolder
│       └── node.py                # Node.js project scaffolder
├── config/                        # Configuration schema and defaults
│   ├── schema.json                # JSON schema for validation
│   └── default.json               # Default configuration template
├── templates/                     # Copier templates
├── .github/workflows/             # CI/CD pipelines
└── scripts/                       # Development scripts
```

## Generated Project Structure

```
my-project/
├── .idea/                        # Project metadata
│   ├── plan.json                 # Enhanced plan with epics/stories
│   ├── queue.json                # Implementation queue
│   └── _logs/                    # Development logs and failures
├── src/                          # Source code
├── tests/                        # Test files
├── lessons/                      # Project-specific lessons
├── .github/workflows/            # CI/CD for the project
└── README.md                     # ADHD-friendly instructions
```

## Error Handling & Issue Reporting

### Automatic Issue Reporting

When errors occur, idea-cli can automatically create GitHub issues with:
- System information (OS, Python version, architecture)
- Configuration summary (sanitized, no secrets)
- Recent log files from `.idea/_logs/`
- Steps to reproduce template

```bash
# Report an issue manually
idea report-issue "CLI command failed" --dry-run

# Automatic issue reporting on unexpected errors
# (triggered automatically with user confirmation)
```

### Manual Issue Creation

If GitHub CLI is not available, idea-cli provides:
- Pre-formatted issue content
- System diagnostics
- Copy-paste ready templates

## Troubleshooting

### Common Issues

**"No such command 'validate'"**
- Fix: Ensure package is installed with `pip install -e .`
- Check: `pip show idea-cli` should show installation

**"Configuration error: API key environment variable not configured"**
- Demo Mode: Ensure `demoMode: true` in `~/.idea-cli/config.json`
- Full Mode: Set environment variables for your API keys

**"Failed to initialize config"**
- Fix: Check permissions for `~/.idea-cli/` directory
- Try: `mkdir -p ~/.idea-cli && idea init-config`

**Import errors for LLM packages**
- Fix: `pip install anthropic` or `pip install openai`
- Note: Only install packages for LLM providers you plan to use

### Performance Tips

- Use `--dry-run` for testing without API calls
- Use `--demo` flag to force demo mode temporarily
- Set appropriate model choices in config (haiku for speed, sonnet for quality)

### Debug Mode

```bash
# Enable verbose logging
export IDEA_CLI_DEBUG=1
idea validate "test idea"

# Check configuration
idea init-config  # Shows current config path and status
```

## Contributing

1. **Setup development environment**: `pip install -e .`
2. **Run tests**: `pytest -v`
3. **Check linting**: `ruff check . && ruff format --check .`
4. **Test in demo mode**: All commands should work without API keys
5. **Test error handling**: Verify issue reporting functionality

### Development Workflow

1. Test demo mode functionality
2. Test full mode with API keys
3. Test error scenarios and issue reporting
4. Run pre-commit hooks
5. Update documentation if needed

## License

MIT License - see LICENSE file for details.

---

**🎭 Start in demo mode, upgrade when ready!**
