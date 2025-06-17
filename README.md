# AI Idea CLI

[![PyPI version](https://badge.fury.io/py/ai-idea-cli.svg)](https://badge.fury.io/py/ai-idea-cli)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)

AI-powered project scaffolding CLI with demo mode for immediate usage.

## 🚀 Quick Start

```bash
# Install
pip install ai-idea-cli

# Use immediately (demo mode)
idea new "my awesome web app"
idea new "python data analysis tool"

# Initialize configuration for advanced features
idea init-config
```

## ✨ Features

- **🎭 Demo Mode**: Works immediately without any setup or API keys
- **🤖 AI Planning**: Generate detailed project plans with epics and stories
- **🏗️ Smart Scaffolding**: Create Python and Node.js projects with best practices
- **📝 Template System**: Customizable project templates using Copier
- **⚙️ Configurable**: Support for multiple LLM providers (Claude, OpenAI)

## 📦 Installation

```bash
pip install ai-idea-cli
```

## 🎯 Usage

### Demo Mode (No Setup Required)

```bash
# Create projects instantly
idea new "react dashboard app" --demo
idea new "python cli tool" --demo

# See what would be created
idea new "my app" --dry-run
```

### Full Mode (with AI Planning)

```bash
# Initialize configuration
idea init-config

# Edit ~/.idea-cli/config.json to add your API keys
# Set demoMode: false

# Create projects with AI-powered planning
idea new "e-commerce platform"
idea validate "social media analytics tool"
```

## 🔧 Configuration

Run `idea init-config` to create `~/.idea-cli/config.json`:

```json
{
  "demoMode": false,
  "models": {
    "plan": "claude-3-5-sonnet-20241022",
    "apiKeyEnv": "ANTHROPIC_API_KEY"
  },
  "validator": {
    "endpoint": "your-validator-endpoint",
    "apiKeyEnv": "VALIDATOR_API_KEY"
  }
}
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🐛 Bug Reports

Found a bug? Please [open an issue](https://github.com/oxygen-fragment/ai-idea-cli/issues) with details.
